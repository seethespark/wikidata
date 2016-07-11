```sql
DROP TABLE IF EXISTS Customer;
CREATE TABLE Customer ( CustomerID serial NOT NULL PRIMARY KEY, CustomerName varchar(100) NOT NULL, AllowedIPs varchar(15)[], DateEntered timestamp NOT NULL, DateUpdated timestamp NOT NULL );

INSERT INTO Customer VALUES (1, 'See The Spark', null , now(), now());

DROP TABLE IF EXISTS Apps;
CREATE TABLE Apps ( AppID serial NOT NULL PRIMARY KEY, AppName varchar(100) NOT NULL, DateEntered timestamp NOT NULL, DateUpdated timestamp NOT NULL );

INSERT Apps VALUES (1, 'Sales Map', now(), now());

DROP TABLE IF EXISTS Users;
CREATE TABLE Users ( UserID serial NOT NULL PRIMARY KEY, CustomerID int NOT NULL, Username varchar(50) NOT NULL, Password varchar(60) NOT NULL, Forename varchar(50) NOT NULL, Surname varchar(50) NOT NULL, EmailAddress varchar(100) NOT NULL, Enabled bool NOT NULL, AESKey varchar(50) NOT NULL, Apps varchar(100)[], IsSysAdmin boolean, DateEntered timestamp NOT NULL, DateUpdated timestamp NOT NULL );

DROP TABLE IF EXISTS Sales;
CREATE TABLE Sales( SalesID serial NOT NULL PRIMARY KEY, CustomerID int, Postcode varchar(9) NULL, SaleValue numeric(8,2) NULL, DisplayText varchar(50) NULL, ProductImageUrl varchar(150) NULL, OrderDateEntered timestamp NULL, OrderID varchar(100), MeasureID smallint, OrderDetail varchar(2000), ProductUrl varchar(500), Latitude real, Longitude real, District varchar(100), DateEntered timestamp NOT NULL, DateUpdated timestamp NOT NULL ) ;

DROP TABLE IF EXISTS SalesUnmatched CREATE TABLE SalesUnmatched( SalesID serial NOT NULL PRIMARY KEY, CustomerID int, Postcode varchar(9) NULL, SaleValue numeric(8,2) NULL, DisplayText varchar(50) NULL, ProductImageUrl varchar(150) NULL, OrderDateEntered timestamp NULL, OrderID varchar(100), MeasureID smallint, OrderDetail varchar(2000), ProductUrl varchar(500), DateEntered timestamp NOT NULL, DateUpdated timestamp NOT NULL ) ;

DROP TABLE IF EXISTS Tracking;
CREATE TABLE Tracking ( SiteID varchar(50), TrackingCookieID char(36), SessionID char(36), RequestID char(36), PageName varchar(100), Duration int, IPAddress varchar(15), UserAgent varchar(500), PageLoadUrl boolean, ResponseStatus smallint, DateEntered timestamp, Event varchar(150), TrackingServerName varchar(30), Supplemental varchar(5000) );


DROP TABLE IF EXISTS lutTrackingLogSource;
CREATE TABLE lutTrackingLogSource ( TrackingLogSourceID smallint NOT NULL PRIMARY KEY, Description varchar(50), DateEntered timestamp NOT NULL, DateUpdated timestamp NOT NULL ); INSERT INTO lutTrackingLogSource VALUES (1, 'Client JS page view', now(), now()); INSERT INTO lutTrackingLogSource VALUES (2, 'Server page view', now(), now());

DROP TABLE IF EXISTS Errors;
CREATE TABLE Errors ( RequestID char(36), Action varchar(50), Server varchar(50), ErrorMessage varchar(2000), ErrorTypeID smallint, DateEntered timestamp );

DROP TABLE IF EXISTS lutMeasure;
CREATE TABLE lutMeasure ( MeasureID smallint NOT NULL PRIMARY KEY, Description varchar(50) NOT NULL, DateEntered timestamp NOT NULL, DateUpdated timestamp NOT NULL );

INSERT INTO lutMeasure VALUES(1, 'Sales', now(), now());
INSERT INTO lutMeasure VALUES(2, 'Returns', now(), now());

DROP TABLE IF EXISTS lutErrorType;
CREATE TABLE lutErrorType ( ErrorTypeID smallint NOT NULL PRIMARY KEY, Description varchar(50) NOT NULL, DateEntered timestamp NOT NULL, DateUpdated timestamp NOT NULL );

INSERT INTO lutErrorType VALUES(1, 'Client error', now(), now());
INSERT INTO lutErrorType VALUES(2, 'Server error', now(), now());
INSERT INTO lutErrorType VALUES(3, 'Connection info', now(), now());
INSERT INTO lutErrorType VALUES(4, 'Other', now(), now());

DROP TABLE IF EXISTS SystemInfo;
CREATE TABLE SystemInfo ( SystemInfoID serial NOT NULL PRIMARY KEY, AppID int NOT NULL, CustomerID int NOT NULL, Name varchar(50) NOT NULL, Value varchar(8000), DateEntered timestamp NOT NULL, DateUpdated timestamp NOT NULL );

INSERT INTO SystemInfo (AppID, CustomerID, Name, Value, DateEntered, DateUpdated) VALUES (1, 1, 'operationMode', 'dev', now(), now());
INSERT INTO SystemInfo (AppID, CustomerID, Name, Value, DateEntered, DateUpdated) VALUES (1, 1, 'previousSalesListsToKeep', '0', now(), now());
INSERT INTO SystemInfo (AppID, CustomerID, Name, Value, DateEntered, DateUpdated) VALUES (1, 1, 'pollInterval', '7', now(), now());
INSERT INTO SystemInfo (AppID, CustomerID, Name, Value, DateEntered, DateUpdated) VALUES (1, 1, 'displayTextSource1', 'district', now(), now());
INSERT INTO SystemInfo (AppID, CustomerID, Name, Value, DateEntered, DateUpdated) VALUES (1, 1, 'imagePathBase', '%image_name%', now(), now());
INSERT INTO SystemInfo (AppID, CustomerID, Name, Value, DateEntered, DateUpdated) VALUES (1, 1, 'clickthroughUrlBase', , now(), now());
INSERT INTO SystemInfo (AppID, CustomerID, Name, Value, DateEntered, DateUpdated) VALUES (1, 1, 'logClientErrors', 'true', now(), now());
INSERT INTO SystemInfo (AppID, CustomerID, Name, Value, DateEntered, DateUpdated) VALUES (1, 1, 'errorServer', , now(), now());
INSERT INTO SystemInfo (AppID, CustomerID, Name, Value, DateEntered, DateUpdated) VALUES (1, 1, 'systemMessage', , now(), now());
INSERT INTO SystemInfo (AppID, CustomerID, Name, Value, DateEntered, DateUpdated) VALUES (1, 1, 'mapMarkerDetailCallToAction', , now(), now());
INSERT INTO SystemInfo (AppID, CustomerID, Name, Value, DateEntered, DateUpdated) VALUES (1, 1, 'leftPanelHeadingText', 'Moo and foo', now(), now());
INSERT INTO SystemInfo (AppID, CustomerID, Name, Value, DateEntered, DateUpdated) VALUES (1, 1, 'leftPanelBodyText', 'Moo and Foo', now(), now());

DROP TABLE IF EXISTS Postcodes;
CREATE TABLE Postcodes ( Postcode varchar(9) NOT NULL UNIQUE, Latitude real NOT NULL, Longitude real NOT NULL, District varchar(100), DateEntered timestamp NOT NULL, DateUpdated timestamp NOT NULL );

DROP TABLE IF EXISTS PostcodesImport;
CREATE TABLE PostcodesImport ( Postcode varchar(9) NOT NULL UNIQUE, Latitude real NOT NULL, Longitude real NOT NULL, District varchar(100) );

COPY PostcodesImport FROM '/home/nick/pc.csv' DELIMITER ',' CSV HEADER;
SELECT * FROM PostcodesImport LIMIT 50;
INSERT INTO Postcodes SELECT *, now(), now() FROM PostcodesImport; TRUNCATE TABLE PostcodesImport;

SELECT * FROM Postcodes LIMIT 50;

DROP TABLE IF EXISTS Reports; CREATE TABLE Reports ( ReportID serial NOT NULL PRIMARY KEY, CustomerID int NOT NULL, AppID int NOT NULL, UserID int NOT NULL, ReportName varchar(50), SQL varchar(6000) NOT NULL, ReportTypeID smallint NOT NULL,	DateEntered timestamp NOT NULL, DateUpdated timestamp NOT NULL );

DROP TABLE IF EXISTS lutReportType; 
CREATE TABLE lutReportType ( ReportTypeID serial NOT NULL PRIMARY KEY, Description varchar(50), DateEntered timestamp NOT NULL, DateUpdated timestamp NOT NULL );

INSERT INTO lutReportType VALUES(1, 'Table', now(), now());
INSERT INTO lutReportType VALUES(2, 'Line graph', now(), now());
INSERT INTO lutReportType VALUES(3, 'Table with line graph', now(), now());


DROP TABLE IF EXISTS QueryHistory;
CREATE TABLE QueryHistory ( QueryHistoryID serial NOT NULL PRIMARY KEY, UserID int NOT NULL, SQL varchar(6000), DateUpdated timestamp NOT NULL,	DateEntered timestamp NOT NULL );
```