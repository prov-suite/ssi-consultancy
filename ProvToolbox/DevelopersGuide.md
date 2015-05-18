# ProvToolbox Developer's Guide

How to set up a development enviroment for ProvToolbox.

You should be familiar with the [User's Guide](./UsersGuide.md) and have installed the software listed in it.

---

## Install Java 7 JDK

Java is a popular object-oriented programming language. The JDK (Java Development Kit) allows Java code to be created and compiled. It comes with the JRE. There are numerous versions of Java available. Two popular ones are:

* [OpenJDK](http://openjdk.java.net/)
* [Oracle Java](https://www.java.com/en/)

Ubuntu [recommend](https://help.ubuntu.com/community/Java) OpenJDK.

Install:

    $ sudo apt-get install openjdk-7-jdk
    $ javac -version
    javac 1.7.0_79
    
---

## Install Git

[Git](http://git-scm.com/) is a popular distributed version control system. It can be used to get the ProvToolbox source code repository.

Install:

    $ sudo apt-get -y install git
    $ git --version

---

## Install Maven

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

---

## Get ProvToolbox source code

Source code is hoted on [GitHub](https://github.com/lucmoreau/ProvToolbox).

Get source code:

    $ git clone https://github.com/lucmoreau/ProvToolbox.git ProvToolboxSource
    $ cd ProvToolboxSource/

Build ProvToolbox:

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