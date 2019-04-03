Since this repository contains the SQLs which I personally felt handy and the Wiki in itself is an explanation of the database table designs, it only follows naturally that we use an SQL interfacing tool for executing our queries. I personally prefer SQL Developer for its ease of use, but there are several other clients that are available like Tora or Toad. 

* SQL Developer can be installed from [Oracle](https://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html) download page.
* TORA can be downloaded from [sourceforge](https://sourceforge.net/projects/tora/) page.
* TOAD can be downloaded from [Toad](http://www.toadworld.com/downloads) site.

Configuring SQL Developer with Teamcenter database

You basically launch the SQL Developer executable and start by adding a new database configuration as shown below.

![SQL Developer Database Configuration](https://i.imgur.com/089YI0G.png)

The mandatory information that is to be filled are shown in the image above. One point to note is that the values of the strings 'Hostname' and 'Service Name' can be found either in the `tc_profilevars.bat` file or by looking up the `TC_DB_SERVER` and `ORACLE_SID` environment variables defined on the Teamcenter shell for that environment. Finally, if everything is entered, the 'Test' button can determine if the connection settings are Ok, with a status message as shown in green.

If the status is `SUCCESS`, we are good to go!. Otherwise, it could be wrong credentials or wrong hostname / database name combinations.