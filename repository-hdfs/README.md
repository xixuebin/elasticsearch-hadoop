#Hadoop HDFS Snapshot/Restore plugin

The `elasticsearch-hadoop-repository-hdfs` plugin allows Elasticsearch 1.0 to use ``hdfs`` file-system as a repository for [snapshot/restore](http://www.elasticsearch.org/guide/en/elasticsearch/reference/master/modules-snapshots.html).

# Requirements
- Elasticsearch (version __1.0__ or higher)
- hdfs accessible file-system (from the Elasticsearch classpath)

# Installation
As with any other plugin, simply run:
``bin/plugin -install elasticsearch/elasticsearch-hadoop-repository-hdfs/1.3.0.M2``

__NOTE__: 1.3.0 M2 has not been released yet, please build and install the plugin manually

## Development Snapshot
Grab the latest nightly build from the [repository](http://oss.sonatype.org/content/repositories/snapshots/org/elasticsearch/elasticsearch-hadoop-repository-hdfs/) again through Maven:

```xml
<dependency>
  <groupId>org.elasticsearch</groupId>
  <artifactId>elasticsearch-hadoop-repository-hdfs</artifactId>
  <version>1.3.0.BUILD-SNAPSHOT</version>
</dependency>
```

```xml
<repositories>
  <repository>
    <id>sonatype-oss</id>
    <url>http://oss.sonatype.org/content/repositories/snapshots</url>
	<snapshots><enabled>true</enabled></snapshots>
  </repository>
</repositories>
```

or [build](#building-the-source) the project yourself. 

# Usage

## Configuration Properties

Once installed, define the configuration for the `hdfs` repository through `elasticsearch.yml`:
```
repositories
	hdfs:
		uri: "hdfs://<host>:<port>/"  	# optional - Hadoop file-system URI
		path: "some/path"			  	# required - path with the file-system where data is stored/loaded
		load_defaults: "true"		  	# optional - whether to load the default Hadoop configuration (default) or not
		conf_location: "extra-cfg.xml"	# optional - Hadoop configuration XML to be loaded
		conf.<key> : "<value>"			# optional - 'inlined' key=value added to the Hadoop configuration
		concurrent_streams: 5			# optional - the number of concurrent streams (defaults to 5)
		compress: "false"				# optional - whether to compress the data or not (default)
		chunk_size: "10mb"				# optional - chunk size (disabled by default)
```

## Plugging other file-systems

Any HDFS-compatible file-systems (like Amazon `s3://` or Google `gs://`) can be used as long as the proper Hadoop configuration is passed to the Elasticsearch plugin. In practice, this means making sure the correct Hadoop configuration files (`core-site.xml` and `hdfs-site.xml`) and its jars are available in plugin classpath, just as you would with any other Hadoop client or job.
Otherwise, the plugin will only read the _default_, vanilla configuration of Hadoop and will not be able to recognized the plugged in file-system.

# Feedback / Q&A
We're interested in your feedback! You can find us on the User [mailing list](https://groups.google.com/forum/?fromgroups#!forum/elasticsearch) - please append `[Hadoop]` to the post subject to filter it out. For more details, see the [community](http://www.elasticsearch.org/community/) page.

# License
This project is released under version 2.0 of the [Apache License][]

```
Licensed to Elasticsearch under one or more contributor
license agreements. See the NOTICE file distributed with
this work for additional information regarding copyright
ownership. Elasticsearch licenses this file to you under
the Apache License, Version 2.0 (the "License"); you may
not use this file except in compliance with the License.
You may obtain a copy of the License at
 
   http://www.apache.org/licenses/LICENSE-2.0
 
Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
```

[Apache License]: http://www.apache.org/licenses/LICENSE-2.0