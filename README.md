# MySQL JDBC Connector

This project packages multiple MySQL JDBC driver versions into a single JAR that could be used in Stratio modules.

Some dependencies have been relocated to avoid conflicts with Spark/Crossdata dependencies, but all of them are included in the JAR.

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