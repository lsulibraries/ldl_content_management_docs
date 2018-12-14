# Manually Indexing a Collection

## About  

SOLR automatically adds new or updated items to the LDL index. However, in the past, there have been issues with an indexing "bottleneck," causing long delays before changes would appear in the index. This impacts search results, and also can affect administrative processes.  

LDL Administrators can manually index / reindex collections, bypassing the automatic indexing, using the following process. There is a timeout limit; using the `--outfile` option sends any failed items to a list which can be processed in a subsequent batch. The admin should rerun the list of failures until all items are successfully indexed.  

Basic instructions follow for manually indexing a collection. Use `drush islandora-utils-reindex-collection -h` to get the full options list.

Note that if you start out with a PID file from another source, you can skip ahead to the `islandora-utils-index-list` step. For instance, if you have added a large batch of items to an existing collection, you can view the batch set to identify the PIDs that were created, and generate a list (using the List PIDS Python script, for example).

- - - - -

## Process

1. Connect to server and navigate to web root:

    `ssh {name}@{IP} -i {filename}.pem`  
    `cd /var/www/ldl`  

1. Index the collection at _{namespace}_, specifying a file where any skipped items will be stored for later processing:

    `drush islandora-utils-reindex-collection -u {username} --collection={namespace}:collection --outfile=/tmp/{namespace}-index`

1. Index the files that failed, specifying a file where any skipped items will be stored for later processing; the outfile name may be the same as the infile name, and the file will be overwritten:

    `drush islandora-utils-index-list --infile=/tmp/{namespace}-index --outfile=/tmp/{namespace}-index`

1. Repeat the previous step until no failures / all items are indexed.

1. Delete the _{namespace}-index_ file from the Temp directory.

    `cd /tmp`  
    `rm {namespace}-index`  

- - - - -

## Ref  

[lsulibraries islandora_utils](https://github.com/lsulibraries/islandora_utils)
