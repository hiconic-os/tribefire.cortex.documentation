# Java installation

## JDK Installation

It is recommended to install one of the two following Java JDK versions:

### OpenJDK

This is the preferred JDK. See also [additional information](#additional-information).

Navigate to [https://jdk.java.net/](https://jdk.java.net/), download, and install the latest OpenJDK package.

### OracleJDK

Navigate to [https://java.com/en/download/](https://java.com/en/download/), download, and install the JDK. We advice the latest LTS version. 

## Additional preparation

Make sure that the `JAVA_HOME` system environment variable is set to the root of your JDK installation.

Make sure that the `PATH` system environment variable contains the `$JAVA_HOME/bin` (Windows: `%JAVA_HOME%\bin`) directory.

You can check it by opening a command prompt and running the `javac -version` command.

## Additional information

There are various java implementations around. The most prominent ones are OracleJDK and OpenJDK. The former is the enterprise-ready version developed and released by Oracle. The latter is an open reference implementation developed by Oracle, OpenJDK, the Community, and other companies (e.g. IBM, Apple, RedHad, SAP, ...). 

Both versions provide full implementation of the java standard. It might be (verify, for concrete cases if needed) that the OracleJDK provides slight edge in GC and runtime performance on production systems. 

One of the important differences between any java JDK version is licensing. Make sure you understand the consequences. 
- OracleJDK, in particular the [NFTC](https://www.oracle.com/java/technologies/javase/jdk-faqs.html) and [OTN](https://www.oracle.com/downloads/licenses/javase-license1.html) versions. **Be careful**: production use of OracleJDK quickly requires a paid license.  
- OpenJDK uses a free open source *GNU General Public License, version 2, with the Classpath Exception*, see [here](https://openjdk.org/legal/). It is free for development, distribution and production.

Many Linux systems automatically provide OpenJDK installations and in almost all cases this will serve as a very robust and safe java development environment. 