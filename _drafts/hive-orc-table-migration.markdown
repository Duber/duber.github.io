---
layout:     post
title:      "Migrate Hive ORC tables between Hadoop Clusters"
subtitle:   ""
date:       2016-12-25 22:00:00
author:     "Miguel Cruz"
---
When working with hive databases on top of Hadoop clusters, the recommended data format is ORC.

ORC is a binary format and unlike plain text formats (such as CSV or JSON), if you want to transfer data between different clusters you cannot simply move its data files between storages.

## How to migrate ORC tables between Hadoop clusters ?
As far as I know there are two strategies:

### 1. Export/Import table commands
With the following command

    <\ INSERT EXPORT COMMAND HERE \>

we would export data from the table into the specified storage location. Alternatively you can also create a export of a single partition with

    <\ INSERT EXPORT PARTITION COMMAND HERE \>

Afterwards we would have to import it into the destination cluster (we might also have to move the export data to a storage accesible by the destionation cluster)

    <\ INSERT IMPORT COMMAND HERE \>

PROS


CONS
* Slower since export/import commands take some time.
* You effectively duplicate data in storage when you create export files.
* Both source and destination Hadoop clusters must be up and running to run export/import command respectively.

### 2. Moving data files and recreating partitions
Another possibility consists of moving binary data files between storages and recreating partitions into destination cluster.

PROS

CONS
