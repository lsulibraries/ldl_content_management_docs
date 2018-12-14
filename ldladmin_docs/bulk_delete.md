# Bulk Deleting Objects (aka iChainsaw)

## About  

Repository objects can be deleted from the user interface, but options are limited. LDL Administrators can use the "iChainsaw" tool to permanently remove objects from the repository by collection, namespace, or a list of PIDs provided in a PID file. __There is no "undo," so be careful.__  

- You can "preview" what objects will be deleted by using the `--list` option.
- PID files should be prepared with one PID per row and placed in the Temp directory at /tmp.  
- For newspaper issues and book objects, all associated page objects are deleted.
- Warning about use of the `--collection` option: Compound child objects will not be deleted (because they do not have the RDF property making them a member of their collection). Furthermore, the top level _collection_ or _newspaper_ object is not deleted with `--collection` but is deleted with `--namespace`. __In most cases, `--namespace` is preferable.__

Use `drush iChainsaw -h` for further information.  

- - - - -

## Process  

1. Connect to server and navigate to web root:  
`ssh {name}@{IP} -i {filename}.pem`  
`cd /var/www/ldl/sites/all`  

1. To delete all objects in a collection:  
  - Preview only: `drush iChainsaw --user={username} --namespace={namespace} --list`  
  - Delete: `drush iChainsaw --user={username} --namespace={namespace}`  

1. Additional options:  
`drush iChainsaw --user={username} --collection={namespace}:collection`  
`drush iChainsaw --user={username} --pid_file=/tmp/{filename}.txt`  
`drush iChainsaw --user={username} --collection={namespace}:collection --content_model={contentmodel}`  
`drush iChainsaw --user={username} --newspaper={namespace}:{PID}`  

- - - - -

## Ref

[mjordan islandora_bulk_delete](https://github.com/mjordan/islandora_bulk_delete)
