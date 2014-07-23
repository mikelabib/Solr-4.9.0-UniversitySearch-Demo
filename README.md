Solr-4.9.0-UniversitySearch-Demo
================================

This is a demo application on how to setup a Solr Search engine using Solr-4.9.0. Being part of the Solr user group and have contributed to the solr wiki page, I'm a huge advocate of this technology. This demo illustrates how to search against a list of universities along with how to load data from a csv file. It by no means, illustrates all the different types of searches or features that Solr provides. For that I recommend the Solr Wiki as a good reference. https://wiki.apache.org/solr/
The university data that I used was provided free under a Creative Commons Attribution-ShareAlike 3.0 Unported License: http://seanlahman.com/baseball-archive/statistics/ . This data was used for the sole purpose demo the Search engine. If you intend to learn Solr, I would recommend experimenting with various types of data and joining the developer user group.

Author: Michael Labib . 

##Getting Started
Clone Solr-4.9.0-UniversitySearch-Demo

##Start Solr
After installing locally on your machine, launch Solr from the command prompt. Be sure to execute the following command on the directory where start.jar is located.

java -jar -Dsolr.solr.home=solr start.jar

##Search All Records
The below URL shows how to query all records. Equivalant to searching on *.*
http://localhost:8983/solr/universities/select?q=:

##Load CSV File
There are many ways to load data into Solr. One method is to stream data from a csv file. The below file is located within the directory structure. Notice the syntax used indicate the file is delimited by a "|" and the names of the fields indicated. The field names match those provided in the schema.xml file located within \Solr-4.9.0-UniversitySearch\solr\universities\conf directory.

http://localhost:8983/solr/universities/update?commit=true&separator=|&escape=&stream.file=C:\solr-4.9.0-UniversitySearch\UniversitySearch-Solr-4.9.0\external-data\Universities.txt&fieldnames=id,university_name,city,state,university_nickname&optimize=true&stream.contentType=application/csv

##Delete All Records
As your experimenting with this engine, the below command illustrates how to delete all records within the index. http://localhost:8983/solr/universities/update?stream.body=%3Cdelete%3E%3Cquery%3E*:*%3C/query%3E%3C/delete%3E&commit=true

##Facet on Name
A simple example on how to create a facet. http://localhost:8983/solr/universities/select?q=:&facet=on&facet.field=university_name&rows=0&facet.mincount=1&facet.sort=index&facet.limit=-1

##Filtered Query on Name (Search all filter on U*)
A simple example on how to filter on a particular field value "U*" for field name university_name. http://localhost:8983/solr/universities/select?q=:&fq=university_name:U*
Now that you got your feet wet, its time to dive deeper into the API and understand all the features.
