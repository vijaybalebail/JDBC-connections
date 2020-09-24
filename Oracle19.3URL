## ORACLE JDBC 19c pass parameters in JDBC URL


In 19.3 version of Oracle database, The JDBC url now accepts some connection properties as well.
This is great news. This can overcome some default parameters in the JDBC programs that are not tuned properly.
Now we can connect to any application where JDBC url is configurable. (which most applications are).
Connect to Oracle using JDBC URL and pass the properties parameters to
- improve performance
-  pass Security parameters
- Pass Transparent Application Continuity parameters

The most common change we do to jdbc default connection  is the Fetchsize, Buffer or ArraySize for getting the query result set. 

Now with 19c, We can pass this properties in the jdbc url.  The default fetch size is 10. This size appears to be tuned for oltp transactions. However, for Data warehouse applications and ETLs,  getting large amount of data across the network is slow  using the default size.

You can change default fetch size by setting connection property “defaultRowPrefetch”.
 In the following example  URL syntax with properties.

```
jdbc:oracle:thin:@(description= (address=(protocol=tcps)(port=1521)(host=example1.com)) (connect_data=(service_name=example2.com)))?oracle.jdbc.defaultRowPrefetch=1000
```

Oracle19c, easy connect syntax also support adding properties.

```
jdbc:oracle:thin:@hostname:1523/pdb1?oracle.jdbc.defaultRowPrefetch=1000&oracle.jdbc.defaultExecuteBatch=1000
```

If you have more than one property to set, the syntax is to start with a ? and any additional parameters with a & sign.
For more Detailed information, check out this [Doc.](https://www.oracle.com/a/tech/docs/java-programming-with-oracle-database-19c.pdf)

### Previous versions

This fetch size could however be set at the driver level or with the application code to improve performance.

The methods  to set at Driver level by setting the property defaultRowPrefetch
1.	 This parameter could be set in ojdbc.properties (18c and higher)
2.	Pass as parameters at run time. (until 12.2.)  .(e.g. java -Doracle.jdbc.defaultRowPrefetch='1000 '   JDBCTest )

Prior to 12.2, the only way to set this property used to be from within the java application.
Within a JAVA program, you can use setFetchSize as a connection method or at a statement level.
 From within the java application the usual ways to set row fetch size are:

1.	 java.sql.Connection vendor implementation class custom method (e.g. OracleConnection.setDefaultRowPrefetch)
2.	Via java.sql.Statement.setFetchSize(int): gives a hint to the driver as to the row fetch size for all ResultSets obtained from this Statement. This method is inherited by PreparedStatement and CallableStatement. Most JDBC drivers support it.
3.	Via java.sql.ResultSet.setFetchSize(int): gives a hint to the driver as to the row fetch size for all this ResultSet.
