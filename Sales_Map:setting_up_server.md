## Web server ##
Copy the application code to the relevant server.  It runs on Windows or Linux as long as Node.JS and NPM is installed.  

Run npm install

Amend settings.js with relevant connection string and setting values.

Test on <nowiki>http://</nowiki><server name>:3000

== Database ==
Currently tested with PostgreSQL (9.1).  The application SQL code is standards compliant so should run on any modern, fast relational database system.  The setup script contains some PostgreSQL specific code which should be removed.

[[Sales Map:Setting up: SQL|SQL Script]]

to    
Web server
----------

Copy the application code to the relevant server. It runs on Windows or Linux as long as Node.JS and NPM is installed.

Run npm install

Amend settings.js with relevant connection string and setting values.

Test on http://<server name>:3000

Database
--------

Currently tested with PostgreSQL (9.1). The application SQL code is standards compliant so should run on any modern, fast relational database system. The setup script contains some PostgreSQL specific code which should be removed.

[SQL Script]

  [SQL Script]: Sales_Map:Setting_up:_SQL "wikilink"