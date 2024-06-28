Thank you very much for taking the time to report a bug to us, we greatly
appreciate it. Even more so, since you are about to take the time to create an
[MCVE (Minimal Complete Verifiable Example)](https://stackoverflow.com/help/minimal-reproducible-example). Thanks to you, we can make jOOQ an
even better product!

## How to use this project to prepare your MCVE

Create a fork from this project and then

```
git clone https://github.com/<your-user-name>/jOOQ-mcve
cd jOOQ-mcve
cd <relevant module>
mvn verify
```

It will, for each supported language (java, kotlin, scala) and example SQL dialect (H2, MySQL, Oracle, PostgreSQL, SQL Server):

- Use testcontainers (for MySQL, Oracle, PostgreSQL, SQL Server) to set up a database instance, and make it available to jOOQ and JUnit
- Install a sample schema located in `src/main/resources/db/migration` into an file-based H2 database or testcontainers managed MySQL, Oracle, PostgreSQL, SQL Server database
- Run jOOQ's code generator on it
- Run a simple integration test

This should work without any additional setup on your side, other than having a JDK, Maven, and Docker available, as well as the commercial distribution of jOOQ installed, if you need that for Oracle or SQL Server. If you do not have Docker, you can still run the H2 based examples directly, ignoring the MySQL, Oracle, PostgreSQL, SQL Server based ones.

## How to prepare your MCVE

For your MCVE, you will have to adapt a few things, probably. All likely locations that may need adaptation are marked with "TODO". This includes:

- The Java / kotlin / scala version: 
  - Go to the relevant `pom.xml` file, search for `java.version`, `kotlin.version`, `scala.version`, and adapt the version there.
- The jOOQ edition and version: 
  - Go to the relevant `pom.xml` file, search for `org.jooq.groupId` and `org.jooq.version`, and adapt the version there.
- The JDBC driver: 
  - Go to the relevant `pom.xml` file, replace the H2, MySQL, Oracle, PostgreSQL, or SQL Server driver `<dependency>` by yours, and adapt `${jooq.codegen.jdbc.url}`, `${jooq.codegen.jdbc.username}`, and `${jooq.codegen.jdbc.password}`
  - Go to the relevant `pom.xml` file, replace the testcontainers integration, if applicable.
  - Go to the relevant test class (`org.jooq.mcve.test.java.JavaTest`, `org.jooq.mcve.test.kotlin.KotlinTest`, or `org.jooq.mcve.test.scala.ScalaTest`) and replace URL, username, and password there as well, if applicable
  
In addition to the above, you probably need to adapt also:

- The SQL script
- The code generator configuration in the `pom.xml`
- The actual test that is being run in any of (depending on what you're using):
  - `org.jooq.mcve.test.java.h2.JavaTest`
  - `org.jooq.mcve.test.java.mysql.JavaTest`
  - `org.jooq.mcve.test.java.oracle.JavaTest`
  - `org.jooq.mcve.test.java.postgres.JavaTest`
  - `org.jooq.mcve.test.java.sqlserver.JavaTest`
  - `org.jooq.mcve.test.kotlin.h2.KotlinTest`
  - `org.jooq.mcve.test.kotlin.mysql.KotlinTest`
  - `org.jooq.mcve.test.kotlin.oracle.KotlinTest`
  - `org.jooq.mcve.test.kotlin.postgres.KotlinTest`
  - `org.jooq.mcve.test.kotlin.sqlserver.KotlinTest`
  - `org.jooq.mcve.test.scala.h2.ScalaTest`
  - `org.jooq.mcve.test.scala.mysql.ScalaTest`
  - `org.jooq.mcve.test.scala.oracle.ScalaTest`
  - `org.jooq.mcve.test.scala.postgres.ScalaTest`
  - `org.jooq.mcve.test.scala.sqlserver.ScalaTest`

When you've set up your MCVE, run these statements again:

```
mvn clean verify
```

## How to submit your MCVE

Found a way to reproduce the issue using the above procedure? Excellent! Now, either commit the change to your fork:

```
git add .
git commit -m "MCVE for issue #1234"
git push
```

And include a link to your repository `https://github.com/<your-user-name>/jOOQ-mcve` in your issue report. Or, just attach a zip file of the project to the issue. Done!

Thanks again for taking the time to do this. Looking forward to your MCVE
