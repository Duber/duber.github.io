---
layout:     post
title:      "Migrate Hive ORC tables between Hadoop Clusters"
subtitle:   ""
date:       2016-12-27 08:30:00
author:     "Miguel Cruz"
---
When working with hive databases on top of Hadoop clusters, the recommended data format is ORC.

ORC is a binary format and unlike plain text formats (such as CSV or JSON), if you want to transfer data between different clusters you cannot simply move its data files between storages.

## How to migrate ORC tables between Hadoop clusters ?
As far as I know there are two strategies:

### 1. Export/Import table commands
With the following command

    export table sourceDb.sourceTable to 'wasb://<EXPORT_STORAGE_PATH>';

we would export data from the table into the specified storage location. Alternatively you can also create a export of a single partition with

    export table sourceDb.sourceTable PARTITION (part_column="value") to 'wasb://<EXPORT_STORAGE_PATH>';

Afterwards we would have to import it into the destination cluster (we might also have to move the export data to a storage accesible by the destionation cluster)

    import table destDb.destTable from 'wasb://<EXPORT_STORAGE_PATH>' location 'wasb://<STORAGE_TABLE_LOCATION>';

PROS
* You don't have to deal with recreating partitions as with the next strategy.

CONS
* Slower since export/import commands take some time.
* You effectively duplicate data in storage when you create export files.
* Both source and destination Hadoop clusters must be up and running to run export/import command respectively.

### 2. Moving data files and recreating partitions
Another possibility consists of moving binary data files between storages and recreating partitions into destination cluster.

This strategy requires you to create the empty table in advance. After moving binary data files you have to recreate partitions pointing to those data files with:

    ALTER TABLE <TABLE_NAME_HERE> ADD PARTITION (<PARTITION_FIELD>='<PARTITION_VALUE>');

PROS
* Faster since you only have to move data files and you don't have to create export/import files.
* Only destination cluster needs to be running in order to recreate partitions.

CONS
* There are prerequisites (table must exists) and you have to build all these partition recreation scripts.

## Conclusion
In my opinion the second strategy (moving data files and recreating partitions) is far superior and simpler.
