Overview
--------

See The Spark's Sales Map shows website sales as they happen. It can pick up sales directly from a tag on the order confirmation page of your website or from a real-time order processing database mirror, depending on your infrastructure.

Once data is received the exact location of the postcode is obscured by several hundred metres to protect customers' identities.

There are many configurable options on a management screen.

Configuring
-----------

There are many elements of Sales Map you may wish to configure. The text or map displayed, for example. The Admin Console allows you to do this easily.

[admin console]

Setting up the Data Harvester
-----------------------------

Data can be collected via a website tag or from a backend database server. If using a database server then Sales Map needs a way to get the data from that database. The Data Harvester runs on the same network as the database and extracts, encrypts and sends data to Sales Map. [Salesmap: data harvester setting up]

Setting up the server
---------------------

Sales Map runs Node.js for scalability. If you are running Sales Map on your own network then it needs to be setup on one of your servers.

[setting up][1]

Ongoing
-------

[data retention]

Technical notes
---------------

[tech notes]

[error codes]

  [admin console]: Sales_Map:admin_console "wikilink"
  [setting up]: Sales_Map:setting_up "wikilink"
  [1]: Sales_Map:setting_up_server "wikilink"
  [data retention]: Sales_Map:data_retention "wikilink"
  [tech notes]: Sales_Map:tech_notes "wikilink"
  [error codes]: Sales_Map:error_codes "wikilink"