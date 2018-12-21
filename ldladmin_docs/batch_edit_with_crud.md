# Batch Editing with CRUD

## About

In order to do offline batch operations on datastreams, we use the utility [Islandora Datastream CRUD](https://github.com/SFULibrary/islandora_datastream_crud). The documentation from the original repository is excellent, and describes additional options and use cases for the utility.

The instructions below pertain to our most common use case, which is as a metadata batch editing tool that is more powerful than Islandora Find and Replace.

## Process

_Note: For use on Test, remember to use /upload in place of /tmp_

### Prep Work

- Identify the needed revisions
- Note the collection namespace, such as 'lsu-12345'
- Note the number of expected objects for the datastream export
- Identify the destination location on your local machine

### Fetch PIDS

1. Connect to server and navigate to web root:  
`ssh {name}@{IP} -i {filename}.pem`  
`cd /var/www/ldl`  

1. Create a PID file  
`drush islandora_datastream_crud_fetch_pids --user={username} --namespace={namespace} --pid_file=/tmp/{namespace}-pids.txt`  
	- (optional: `--content_model={contentmodel}`)  

- Note: This relies on the SOLR index to retrive PIDS. If the collection has been indexed only partially or not at all, then your PID list will be incomplete.
- As an alternative to the fetch_pids command, you may use the resource index to query for PIDS and create a PID list that way. See [Querying the Resource Index](query_resource_index.md); you'll have to edit the resulting list to have exactly one pid (without the 'info:fedora/' prefix) per line, save as a .txt file, then scp the file to Production for use in the following steps. 

### Fetch and Zip Datastreams

1. Fetch datastreams using the PID file:  
`drush islandora_datastream_crud_fetch_datastreams --user={username} --pid_file=/tmp/{namespace}-pids.txt --dsid=MODS --datastreams_directory=/tmp/{namespace}-crud/`  
	- `--dsid` could be any datastream ID, such as OBJ, DC, etc.

1. Zip the datastream directory into a zip file:  
`cd /tmp`  
`zip -r -0 {namespace}-crud.zip {namespace}-crud/`

1. Copy datastreams to your computer:  
`cd {local destination directory}\`  
`scp -i {filename}.pem {name}@{IP}:/tmp/{namespace}-crud.zip .`

### Make Revisions to Exported Files

Modifying the files depends on the circumstances. For metadata changes, you might transform the files with XSLT (using either Oxygen or Saxon -- see [Processing XSLT with Saxon](process_xslt_with_saxon.md)), you might use targeted scripts, or you might use a text editor or other program to find and replace or manually edit the XML files. If you are modifying object files instead of MODS, you might use an image or media editor to make changes.

1. Unzip the datastream zip file on your computer

1. Make the necessary revisions using the method of your choosing

1. Check to make sure the new MODS files validate

1. Perform general QA before importing the new files
	- Datastream CRUD does provide a mechanism for reverting datastreams to a previous version, but it's best not to rely on that!

1. When satisfied, zip the updated datastreams back into a zip file, `{namespace}-crud.zip`

### Copy and Replace the Datastreams in LDL

1. Copy the zip file back to the server:  
`cd {local destination directory}\`  
`scp -i {filename}.pem {namespace}-crud.zip {name}@{IP}:/tmp/`

1. Connect to server and navigate to the Temp directory:  
`ssh {name}@{IP} -i {filename}.pem`    
`cd /var/www/ldl`  

1. Unzip the files in the Temp directory:  
`unzip {namespace}-crud.zip -d {namespace}-crud/`  
	- _This will overwrite the existing files; no need to delete them._

1. Replace the datastreams in the collection:  
`cd /var/www/ldl/sites/all`  
`drush islandora_datastream_crud_push_datastreams --user={username} --datastreams_source_directory=/tmp/{namespace}-crud/ --pid_file=/tmp/{namespace}-pids.txt`  

### Review the Changes

1. Assuming the process completes without error, go to the collection on louisianadigitallibrary.org and check to see that the datastream replace was successful.

- You should see your desired changes, and you should also see that there is a new version of the MODS (and derivative DC) datastream(s).

### Clean Up the Server  

1. Remove the PID file, zip files, and the datastream directory from the Temp directory:  
`cd /tmp`  
`rm {namespace}-pids.txt`  
`rm {namespace}-crud.zip`  
`rm -rf {namespace}-crud/`  

- - - - -

## Ref

- [Islandora Datastream CRUD](https://github.com/SFULibrary/islandora_datastream_crud)
- [LSULib TI CRUD documentation](https://github.com/lsulibraries/internal-docs/blob/master/source/Islandora_CRUD.rst)
- [Transforming XML with XSLT](http://dh.obdurodon.org/transformation-scenario.xhtml)
- [Using Saxon at the command line](http://www.saxonica.com/documentation/index.html#!using-xsl/commandline)
