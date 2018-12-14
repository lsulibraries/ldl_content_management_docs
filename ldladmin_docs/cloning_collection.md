# Islandora Collection Clone

- _Using the 'Change Namespace Collection' module to clone a collection in a new namespace._

### Before Beginning
- Identify the collection to be cloned and the new namespace to be assigned.
- The collection container _does not need to be made_ prior to beginning ingest.

### SSH in to Production server and change to web root directory.  
    `ssh XXXX@IP -i XXXX.pem`  
    `cd /var/www/ldl`  

### Preprocess based on category of content model.  
    - `drush islandora_change_namespace_collection --user={userName} --pid={oldNamespace}:collection --new_pid={newNamespace}:collection`  
    - Get the batch set ID number.

### Ingest the batch set
    `drush -v ibi --user={userName} --ingest_set={setID}`

### Perform quality control  
    - Visual check that numbers match  
    - Update collection policy -- change default namespace for content models used in the collection
    - Update the collection mods identifier field
    - Update any collection- or item- referencing links in the collection description
    - Run automated QA Checker utility:
      `drush islandora_change_namespace_collection_qa --clone={newNamespace}:collection --origin={oldNamespace}:collection --icns_verbose`
    - Investigate any error reports  
    
### Publish the collection  
    `drush islandora-collection-toggle-publish-set publish --pid={newNamespace}:collection`

### Clear Cache  
    `drush cc all`

### Delete original collection  
    `cd /var/www/ldl/sites/all`
    `drush iChainsaw --user={userName} --namespace={oldNamespace}`
