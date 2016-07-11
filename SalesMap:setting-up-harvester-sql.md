Below is an example script to build a cache table.  It is written for SQL Server but gives an approach which would work for other RDBMS.

The table:
```sql
 CREATE TABLE sparkSales (
  Postcode varchar(9),
  SaleValue money,
  DisplayText varchar(50),
  ProductImageUrl varchar(150),
  OrderDateTime timestamp,
  OrderID varchar(100),
  MeasureID int,
  OrderDetail varchar(2000),
  ProductUrl varchar(500)
 )
```
The code to populate it:
```sql
 SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
 /***********************************************************************
 Build a CTE with customer orders and get the image path, oder info and URL for 
 the two highest value products in the order.
 ***********************************************************************/
 WITH ProductsS_CTE (CustomerOrderID, ImagePath, OrderDetail, ProductUrl) as ( 
 SELECT o.CustomerOrderID, ( 
   SELECT STUFF( 
   ( SELECT TOP 2 ',' + psd.MainImagePath
   FROM CustomerOrderItem coi
   JOIN ProductSku ps ON ps.SKU = coi.SKU
   JOIN ProductSkuDetail psd ON psd.SKU = ps.SKU
   WHERE coi.CustomerOrderID = co.CustomerOrderID
   ORDER BY oi.PriceIncVat DESC
   FOR XML PATH('')),1,1,'') 
  ) AS ImagePath,
  ( 
   SELECT STUFF( 
   ( SELECT TOP 2 '~' + psd.SkuName
   FROM CustomerOrderItem coi 
   JOIN ProductSku ps ON ps.SKU = ri.sku
   JOIN ProductSkuDetail psd ON psd.SKU = ps.SKU
   WHERE coi.CustomerOrderID = co.CustomerOrderID
   ORDER BY ri.PriceIncVat DESC
   FOR XML PATH('')),1,1,'') 
  ) AS ProductDescription
  , ( 
   SELECT STUFF( 
   ( SELECT TOP 2 ',' + CAST(ps.PimProdID as varchar)
   FROM CustomerOrderItem coi 
   JOIN ProductSku ps ON ps.SKU = coi.SKU
   JOIN ProductSkuDetail psd ON psd.SKU = ps.SKU
   WHERE coi.CustomerOrderID = co.CustomerOrderID
   ORDER BY ri.PriceIncVat DESC
   FOR XML PATH('')),1,1,'') 
  ) AS ProductUrl  
 FROM CustomerOrder co
 )
 ,
 /***********************************************************************
 Build a CTE with customer returns and get the image path, oder info and URL for 
 the two highest value products in the order.
 ***********************************************************************/
 ProductsR_CTE (CustomerReturnID, ImagePath, OrderDetail, ProductUrl) as ( 
 SELECT r.CustomerReturnID, ( 
   SELECT STUFF( 
    (SELECT TOP 2 ',' + psd.MainImagePath
    FROM CustomerReturnItem cri    
    JOIN ProductSku ps ON ps.SKU = cri.SKU
    JOIN ProductSkuDetail psd ON psd.SKU = ps.SKU
    WHERE cri.CustomerReturnID = cr.CustomerReturnID
    ORDER BY cri.OriginalPriceIncVAT DESC
    FOR XML PATH(''))
    ,1,1,'') 
   ) AS ImagePath , ( 
   SELECT STUFF( 
    (SELECT TOP 2 '~' + psd.SkuName
    FROM CustomerReturnItem ri    
    JOIN ProductSku ps ON ps.SKU = ri.OriginalSku
    JOIN ProductSkuDetail psd ON psd.SKU = ps.SKU
    WHERE cri.CustomerReturnID = cr.CustomerReturnID
    ORDER BY cri.OriginalPriceIncVAT DESC
    FOR XML PATH(''))
    ,1,1,'') 
   ) AS ProductDescription , ( 
   SELECT STUFF( 
    (SELECT TOP 2 ',' + CAST(ps.PimProdID as varchar)
    FROM CustomerReturnItem cri    
    JOIN ProductSku ps ON ps.SKU = ri.SKU
    JOIN ProductSkuDetail psd ON psd.SKU = ps.SKU
    WHERE cri.CustomerReturnID = cr.CustomerReturnID
    ORDER BY cri.OriginalPriceIncVAT DESC
    FOR XML PATH(''))
    ,1,1,'') 
   ) AS ProductUrl 
 FROM CustomerReturn cr 
 )
 , 
 /***********************************************************************
 Build a CTE with all customer orders and the value.
 ***********************************************************************/
 Sales_CTE (CustomerOrderID, SaleValue) as (     
  SELECT co.CustomerOrderID, SUM(oi.PriceIncVat*oi.Quantity) as SalesValue
  FROM CustomerOrderItem coi
  JOIN CustomerOrder o ON co.CustomerOrderID = coi.CustomerOrderID
  WHERE ri.Status != 'cancelled'
  AND r.status != 'cancelled'
  AND r.Channel = 'customer order'
  GROUP BY co.CustomerOrderID
 ) 
 , 
 /***********************************************************************
 Build a CTE with all customer returns and the value.
 ***********************************************************************/
 Returns_CTE (CustomerReturnID, ReturnValue, ReturnReason, Postcode) as (     
  SELECT cr.CustomerReturnID, SUM(cri.OriginalPriceIncVAT*cri.QtyExpected) as SalesValue,
   MAX(rr.ShortDescription), MAX(co.Postcode)
  FROM CustomerReturnItem cri
  JOIN CustomerReturn cr ON cr.CustomerReturnID = cri.CustomerReturnID
  JOIN CustomerOrder co ON oe.CustomerOrderID = cr.OriginalCustomerOrderID
  JOIN ReturnReason rr ON rr.ReturnReasonID = cri.ReturnReasonID
  GROUP BY cr.CustomerReturnID
 ) 
 /***********************************************************************
 Combine the CTEs to get a flat list of orders/returns with the two highest value products
 and the value of the order/return for the last 5 minutes.
 ***********************************************************************/
 SELECT o.Postcode, s.SaleValue, 
   CASE WHEN m.IsMobileSite = 1 THEN 'Mobile Site' ELSE 'Desktop Site' END AS DisplayText, 
  p.ImagePath, o.DateEntered,
  co.CustomerOrderID as OrderID, 
  1 as Measure, p.OrderDetail, p.ProductUrl
 INTO #sparkSales
 FROM CustomerOrder o 
 CROSS APPLY udfIsMobile(co.CustomerOrderID) m
 JOIN ProductsS_CTE p ON p.CustomerOrderID = co.CustomerOrderID 
 JOIN Sales_CTE s ON s.CustomerOrderID = co.CustomerOrderID 
 WHERE o.DateEntered > DATEADD(minute, -5, getdate())
 UNION
 SELECT s.Postcode, s.ReturnValue, s.ReturnReason AS DisplayText, 
  p.ImagePath, cr.DateEntered , 
  cr.CustomerReturnID as OrderID, 
  2, OrderDetail, p.ProductUrl
 FROM CustomerReturn cr
 JOIN ProductsR_CTE p ON p.CustomerReturnID = cr.CustomerReturnID
 JOIN Returns_CTE s ON s.CustomerReturnID = cr.CustomerReturnID 
 WHERE cr.DateEntered > DATEADD(minute, -5, getdate())
 AND p.ProductUrl IS NOT NULL
 BEGIN TRAN
 DELETE sparkSales
 INSERT INTO sparkSales
 SELECT * FROM #sparkSales
 COMMIT
 DROP TABLE #sparkSales
```