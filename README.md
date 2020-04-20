## An App to load STIX-2.0 objects

**StixLoader** is a desktop application that loads [STIX-2.0](https://oasis-open.github.io/cti-documentation/) 
objects from various source storage systems to destination output systems. The aim of **StixLoader** is to convert STIX-2
domain objects (SDO) and relationships (SRO) from and to; files, MongoDB, Neo4j, PostgreSQL and ElasticSearch. 
**StixLoader** runs on the Java Virtual Machine and provides a graphical user interface 
for choosing the STIX-2 data source and destination systems.
    
### Installation and packaging
Download this repo, and install the latest [SBT](http://www.scala-sbt.org/). 

Brew is broken for Scala, instead install scala using: 

curl -s "https://get.sdkman.io" | bash   
source ".sdkman/bin/sdkman-init.sh" 
sdk install sbt

You will also need to install Oracle JDK 8 (has javafx bundled)

Also, change the version in the build.sbt file to the right version of SBT

To compile the source code and assemble the application and all its dependencies into a single fat jar file, use [SBT](http://www.scala-sbt.org/) and type:

    sbt assembly

This will produce a big jar file called *stixloader-1.1.jar* in the *./target/scala-2.12* directory. 
    
### Usage

Using [SBT](http://www.scala-sbt.org/) directly (without having to generate a jar file) type:

    sbt run
 
Using Java to launch **StixLoader**, type at a command prompt:
 
    java -jar stixloader-1.1.jar

Or in most systems, double click on the *stixloader-1.1.jar* file.

This will display the main user interface of the application.

![Alt text](/stixloader.png?raw=true "StixLoader")

Select the data source from the **From** list, then select a destination from the **To** list.
**StixLoader** will convert and load the data as per the selections when the **Load** button is clicked. 
Some basic chronological log information can be read in the *Log info* tab.

Selecting *File* will popup a file dialog to choose the file to convert to or from. The file types can be 
a file (.json or .stix) containing a STIX-2 bundle in json format, 
or a zip file containing one or more bundle files, i.e. with extension .json or .stix, all other files types 
are ignored. 

Selecting *MongoDB* will try to connect to a *MongoDB* server. If no server is running a message 
to that effect will be displayed at the bottom of the App. Ensure that the *MongoDB* server has 
 finished connecting before clicking on the **Load** button.

Selecting *Neo4j* will pop-up a dialog to choose the Neo4j database directory to load the data to. 
Currently *Neo4j* can only be selected as a destination.  

Selecting *PostgreSQL* is not yet implemented. 

The experimental *ElasticSearch* is only implemented as a destination from a *File* source, see also *application.conf* file 
for *ElasticSearch* required settings.

The selection of one data source or destination disables the opposite system. For example; 
if *MongoDB* is selected in the *From* section, the *MongoDB* is deselected in the *To* section.

To deselect a currently selected item, simply click on it again. If the selection pops-up a dialog, 
for example when choosing *File*, select *Cancel* and the selection will be removed.

The *application.conf* file in the resource directory contains settings for the *MongoDB* server, 
*Neo4j* default database directory and *Elasticsearch* server. Adjust these entries to suit your system.

Note: a full debugging log can be found in the *application.log* file in the *logs* directory. 
To tune the loggin process, edit the *logback.xml* file.

A large STIX-2 dataset can be found from MITRE 
[Cyber Threat Intelligence Repository expressed in STIX 2.0](https://github.com/mitre/cti).
Download the whole github repository as a **.zip** file, then select this **cti-master.zip** 
as the source **File** and **Neo4j** as the destination. Launch the **Neo4j app** and select the Neo4j directory as the database location and click start. 
Once the status is "started", open a browser on "http://localhost:7474". The data can then displayed as a graph.

### Dependencies and requirements

Depends specifically on the [ScalaStix](https://github.com/workingDog/scalastix) and 
[StixToNeoLib](https://github.com/workingDog/StixToNeoLib).

See also the *build.sbt* file.

Java 8 is required.
                       
### References
 
1) [Neo4j](https://neo4j.com/)

2) [Java Neo4j API](https://neo4j.com/docs/java-reference/current/javadocs/)

3) [ScalaStix](https://github.com/workingDog/scalastix)

4) [StixToNeoLib](https://github.com/workingDog/StixToNeoLib)

5) [STIX-2](https://oasis-open.github.io/cti-documentation/)

6) [MongoDB](https://www.mongodb.com/)

7) [PostgreSQL](https://www.postgresql.org/)

8) [Elasticsearch](https://www.elastic.co/)

9) [Elastic4s](https://github.com/sksamuel/elastic4s)

### Status

work in progress.

Currently, only converts and loads STIX-2 

from: file to: MongoDB, Neo4j and Elasticsearch, and

from: MongoDB to: file and Neo4j

