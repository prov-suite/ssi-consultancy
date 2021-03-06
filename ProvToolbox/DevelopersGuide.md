# ProvToolbox Developer's Guide

This page describes how to set up a development enviroment for ProvToolbox and other useful information for developers.

You should be familiar with the [User's Guide](./UsersGuide.md) and have installed the software listed in it.

---

## Set up development environment

### Install Java 7 JDK

Java is a popular object-oriented programming language. The JDK (Java Development Kit) allows Java code to be created and compiled. It comes with the JRE. There are numerous versions of Java available. Two popular ones are:

* [OpenJDK](http://openjdk.java.net/)
* [Oracle Java](https://www.java.com/en/)

Ubuntu [recommend](https://help.ubuntu.com/community/Java) OpenJDK.

Install:

    $ sudo apt-get install openjdk-7-jdk
    $ javac -version
    javac 1.7.0_79

### Install Git

[Git](http://git-scm.com/) is a popular distributed version control system. It can be used to get the ProvToolbox source code repository.

Install:

    $ sudo apt-get -y install git
    $ git --version
    git version 1.9.1

### Install Maven

Apache [Maven](https://maven.apache.org/) is a software project management and automated project build tool.

Install:

    $ sudo apt-get -y install maven
    $ mvn -v
    Apache Maven 3.0.5
    Maven home: /usr/share/maven
    Java version: 1.7.0_79, vendor: Oracle Corporation
    Java home: /usr/lib/jvm/java-7-openjdk-amd64/jre
    Default locale: en_US, platform encoding: UTF-8
    OS name: "linux", version: "3.16.0-30-generic", arch: "amd64", family: "unix"

If using MacOSX then configure Maven for MacOSX:

    $ export MAVEN_OPTS=-Xmx512m

Thanks to Satra (see [issue 44 comment](https://github.com/lucmoreau/ProvToolbox/issues/44#issuecomment-11319862))

### Get ProvToolbox source code

Source code is hoted on [GitHub](https://github.com/lucmoreau/ProvToolbox).

Either, download and unpack a source release:

    $ curl -L -o master.zip -O https://github.com/lucmoreau/ProvToolbox/zipball/master
    $ unzip master.zip
    $ cd lucmoreau-ProvToolbox-f602c0f/

Or, clone the source code repository:

    $ git clone https://github.com/lucmoreau/ProvToolbox.git ProvToolboxSource
    $ cd ProvToolboxSource/

---

## Build ProvToolbox

Run:

    $ mvn clean install

If all goes well, the build should complete with a status report:

    [INFO] ------------------------------------------------------------------------
    [INFO] Reactor Summary:
    [INFO] 
    [INFO] ProvToolbox: Java for W3C PROV .................... SUCCESS [0.632s]
    [INFO] PROV-MODEL ........................................ SUCCESS [10.022s]
    [INFO] PROV-XML .......................................... SUCCESS [26.620s]
    [INFO] PROV-N ............................................ SUCCESS [18.762s]
    [INFO] PROV-DOT .......................................... SUCCESS [5.050s]
    [INFO] PROV-JSON ......................................... SUCCESS [20.823s]
    [INFO] PROV-RDF .......................................... SUCCESS [18.752s]
    [INFO] PROV-TEMPLATE ..................................... SUCCESS [3.045s]
    [INFO] PROV-GENERATOR .................................... SUCCESS [4.330s]
    [INFO] PROV-INTEROP ...................................... SUCCESS [2.651s]
    [INFO] PROV Toolbox ...................................... SUCCESS [7.471s]
    [INFO] PROV-SQL .......................................... SUCCESS [1:09.727s]
    [INFO] ProvToolbox Tutorial 1 ............................ SUCCESS [6.432s]
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD SUCCESS
    [INFO] ------------------------------------------------------------------------
    [INFO] Total time: 3:15.601s
    [INFO] Finished at: Tue May 12 07:23:18 PDT 2015
    [INFO] Final Memory: 99M/253M
    [INFO] ------------------------------------------------------------------------

provconvert is available in the directory:

    $ ./toolbox/target/appassembler/toolbox/target/appassembler/bin/provconvert -version
    prov-convert:  version x.y.z

### Troubleshooting: 'Warning: JAVA_HOME environment variable is not set.'

If you get:

    $ mvn clean install
    Warning: JAVA_HOME environment variable is not set.
    ...
    [ERROR] Failed to execute goal org.apache.maven.plugins:maven-compiler-plugin:2.0.2:compile (default-compile) on project prov-model: Compilation failure
    [ERROR] Unable to locate the Javac Compiler in:
    [ERROR] /usr/lib/jvm/java-7-openjdk-amd64/jre/../lib/tools.jar
    [ERROR] Please ensure you are using JDK 1.4 or above and
    [ERROR] not a JRE (the com.sun.tools.javac.Main class is required).
    [ERROR] In most cases you can change the location of your Java
    [ERROR] installation by setting the JAVA_HOME environment variable.
    [ERROR] -> [Help 1]

Then install the Java JDK.

### Troubleshooting: 'Warning: JAVA_HOME environment variable is not set.'

If you get:

    [ERROR] Failed to execute goal
    org.codehaus.mojo:rpm-maven-plugin:2.1-alpha-4:attached-rpm
    (attach-rpm) on project toolbox: RPM build execution returned:
    '127' executing '/bin/sh -c cd
    /home/user/ProvToolbox/toolbox/target/rpm/toolbox/SPECS &&
    rpmbuild -bb --target noarch-redhat-linux --buildroot
    /home/user/ProvToolbox/toolbox/target/rpm/toolbox/buildroot
    --define '_topdir
    /home/user/ProvToolbox/toolbox/target/rpm/toolbox' toolbox.spec'
    -> [Help 1] 

Then install the rpm package using apt-get.

---

## Javadoc

0.6.0 JavaDoc is hosted at [openprovenance.org](http://openprovenance.org/java/site/0_6_0/apidocs/).

### Create JavaDoc

To create JavaDoc, run:

    $ mvn javadoc:javadoc

JavaDoc will be created for each module, located at:

    ./prov-n/target/site/apidocs/
    ./prov-xml/target/site/apidocs/
    ./prov-sql/target/site/apidocs/
    ./prov-json/target/site/apidocs/
    ./prov-template/target/site/apidocs/
    ./prov-model/target/site/apidocs/
    ./prov-generator/target/site/apidocs/
    ./prov-dot/target/site/apidocs/
    ./prov-rdf/target/site/apidocs/
    ./prov-interop/target/site/apidocs/
    ./tutorial/tutorial1/target/site/apidocs/

---

## Maven repository

ProvToolbox is now deployed on the [Maven Central Repository](http://search.maven.org/). There is no need to configure repositories.

---

## Key Dependencies

Key dependencies automatically downloaded by Maven:

* For the XML representation, ProvToolbox relies on [JAXB](https://jaxb.java.net/) converting beans to XML and vice-versa.
* For the RDF representation, ProvToolbox relies on [Sesame](http://rdf4j.org/).
* For the PROV-N representation, ProvToolbox relies on [ANTLR](http://www.antlr.org/), a parser generator used to convert a [Grammar for PROV-N](https://github.com/lucmoreau/ProvToolbox/blob/master/prov-n/src/main/antlr3/org/openprovenance/prov/notation/PROV_N.g) into a Java parser.
* For the JSON conversion, ProvToolbox relies on [GSON](https://github.com/google/gson) to convert Java to PROV-JSON, conformant to a [JSON Schema](https://github.com/lucmoreau/ProvToolbox/blob/master/prov-json/schema/prov-json-schema-v4.js) which has been developed.
