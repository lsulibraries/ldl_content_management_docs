# Islandora Command-Line (Drush) Ingest

- _The full process of ingesting a collection to Production at the command line._
- If using Test, replace '/tmp' with '/upload' throughout.
- Commands listed here may have additional options; the most commonly used are given. Use `drush {commandName} -h` for help.


## Before Beginning
Before starting the ingest process, the ingest package(s) should be ready and zipped locally. Remember that each different content model requires a different ingest package, and that different categories of content types have different requirements for their directory structure.  

Refer to documentation on [structuring ingest packages](../colladmin_docs/structuring_ingest_packages.md) for more information on preparing zip files.  

The collection container must also be made prior to beginning ingest. Refer to documentation on creating a collection container.



## Stage for Ingest

### Secure copy ingest package zip file(s) from local computer to Production  

`scp -i XXXX.pem {path/to/zip}.zip XXXX@IP:/tmp/`  
    - Alternately, upload compounds directly without zipping. Use the `-r` flag before `-i`.

### SSH in to Production server and change to Temp directory.  

`ssh XXXX@IP -i XXXX.pem`  
`cd /tmp`  

### Check that sufficient space is available.  

`df -h`  

### Unzip the file to a collection directory under Temp.  

- Directory naming convention: Match the zip file naming convention. Use the namespace prefix for the collection (institution, hyphen, collection code), followed by underscore, followed by an abbreviation for the content type.  

`mkdir {directoryName}/`  
`unzip -o {fileName}.zip -d {directoryName}/`  

### _Compounds only:_ Create structure files.  

- The structure file command must point to the directory that is the immediate container of the compound parent folders. Each compound parent folder should have a structure file, as opposed to a single structure.xml for the collection.  

`cd /var/www/ldl/sites/all/modules/islandora_compound_batch/extras/scripts`  
`php create_structure_files.php /tmp/{directoryName}/`  


## Batch Ingest

### Preprocess based on category of content model.  

`cd /var/www/ldl`  

- Simple preprocess { islandora:sp_large_image_cmodel | islandora:sp-audioCModel | islandora:sp_pdf | islandora:sp_videoCModel }  

`drush -v ibsp --user={userName} --namespace={namespace} --parent={namespace}:collection --content_models={contentModelName} --type=directory --scan_target=/tmp/{directoryName}/`  

- Book preprocess islandora_book_batch_preprocess { islandora:bookCModel }

`drush -v ibbp --user={userName} --namespace={namespace} --parent={namespace}:collection --type=directory --scan_target=/tmp/{directoryName}/ --output_set_id`
    - optional: --do_not_generate_ocr

- Newspaper preprocess { islandora:newspaperIssueCModel }
    - Before drush ingesting newspaper issue objects, you must create the parent-level newspaper object as a child of the collection object. Make note of the newspaper object's PID.

`drush -v inbp --user={userName} --namespace={namespace} --parent={namespace:newspaperPID} --type=directory --scan_target=/tmp/{directoryName}/`

- Compound preprocess { islandora:compoundCModel }

`drush -v icbp --user={userName} --namespace={namespace} --parent={namespace}:collection --content_models={contentModelName FOR CHILDREN} --scan_target=/tmp/{directoryName}/`  

- Remote Resource { islandora:sp_remote_resource }

`drush -v --user={userName} islandora_remote_resource_ingest_remote_oai_collection --namespace={namespace} --oai_endpoint=/oai/oai.php --oai_remote_platform=cdm --parent={namespace}:collection --oai_host={host url, eg: cdm16340.contentdm.oclc.org} --oai_set={set id, eg: p15196coll8}`

- Get the batch set ID number.

### Ingest the batch set

`drush -v ibi --user={userName} --ingest_set={setID}`


## Post Ingest  

### Delete the collection files from the Production server

`cd /tmp`  
`rm {fileName}.zip`  
`rm -rf {directoryName}/`  

### Publish the collection

`drush islandora-collection-toggle-publish-set publish --pid={namespace}:collection`

### Clear Cache  

`drush cc all`
