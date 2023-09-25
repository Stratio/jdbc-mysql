# MySQL JDBC Connector

This project packages MySQL JDBC driver into a single JAR that could be used as dependency.
It adds the MySQL JDBC connector version to class qualified names, so you can use several jdbc versions simultaneously:

```xml
<dependency>
    <groupId>com.stratio.connectors</groupId>
    <artifactId>mysql-jdbc-8.0.30</artifactId>
    <version>${mysql.stratio.version}</version>
</dependency>
<dependency>
    <groupId>com.stratio.connectors</groupId>
    <artifactId>mysql-jdbc-5.1.42</artifactId>
    <version>${mysql.stratio.old.version}</version>
</dependency>
``` 

And then you can do programmatically:

```scala
import java.sql.{Connection, DriverManager => SQLDriverManager}
import scala.jdk.CollectionConverters.enumerationAsScalaIteratorConverter

// register driver for mysql jdbc version 8.0.30
SQLDriverManager.registerDriver(new com.mysql8030.cj.jdbc.Driver())
// use driver 8.0.30
// Unregister driver for jdbc:mysql://
SQLDriverManager.getDrivers.asScala
  .filter(_.acceptsURL("jdbc:mysql://"))
  .toList
  .foreach(SQLDriverManager.deregisterDriver)
// register driver for mysql jdbc version 5.1.42
SQLDriverManager.registerDriver(new com.mysql5142.jdbc.Driver())
// use driver 5.1.42
```

Some dependencies have been relocated to avoid conflicts with other modules used in Stratio, but all of them are included in the final fatjar.

## Artifacts

Releases can be found in [Stratio Nexus](http://niquel.stratio.com/#browse/search/maven=attributes.maven2.groupId%3Dcom.stratio.mysql).

Compatibility matrix:

| Branch            | MySQL | Driver Class                       | Notes     |
|-------------------|-------|------------------------------------|-----------|
| branch-5.1.42-1.0 | <5.7  | com.mysql.jdbc.Driver              |           |
| branch-8.0.30-1.0 | ≥5.7  | com.mysql.cj.jdbc.Driver           |           |

## Developers

Modify the following line in the `pom.xml` file with the desired version:

```xml
<mysql.version>5.1.42</mysql.version>
```

Check the relocations in the file `pom.xml`. They are at the end of the file, in the Shade plugin. It is important to test the final JAR in Crossdata to make sure there are no conflicts.

To build the JAR run:
```bash
mvn package 
```
