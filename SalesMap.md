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

Data can be collected via a website tag or from a backend database server. If using a database server then Sales Map needs a way to get the data from that database. The Data Harvester runs on the same network as the database and extracts, encrypts and sends data to Sales Map. [[Salesmap: data harvester setting up]]

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

Licencing
---------

This software is provided by See The Spark Ltd and it retains the copyright. Any modification or copying must first be agreed in writing from See The Spark. The licence allows for internal use on a single site. See The Spark reserve the right to revoke this licence at any time.

jQuery is licenced for use and distribution under the MIT licence.

Test images are surced from <http://pixabay.com/>

The detailed map is licensed under the Creative Commons Attribution-Share Alike 3.0 license. You are free to use and change it but it requires to remain under the same or similar license.

<http://commons.wikimedia.org/wiki/File:United_Kingdom_map.png>

The outline and physical maps are licenced under the GNU licence and provided by Wikipedia.

<http://en.wikipedia.org/wiki/File:United_Kingdom_location_map.svg>

Google maps are licenced for testing only on the demo version. If access is restricted then Google require a separate licence..

The mainland postcode information is provided by the ONS under the Open Government Licence. Northern Ireland data is from the Northern Ireland Statistics and Research Agency in 2008. <http://www.doogal.co.uk/PostcodeFAQ.php>

Some postcode amendments were taken from <http://www.postcode-info.co.uk/counties.html> and <http://www.ukpostcodes.org/postcode-database-api-downloads>

No responsibility is taken for the correctness of this information.

  [admin console]: Sales_Map:admin_console "wikilink"
  [setting up]: Sales_Map:setting_up "wikilink"
  [1]: Sales_Map:setting_up_server "wikilink"
  [data retention]: Sales_Map:data_retention "wikilink"
  [tech notes]: Sales_Map:tech_notes "wikilink"
  [error codes]: Sales_Map:error_codes "wikilink"