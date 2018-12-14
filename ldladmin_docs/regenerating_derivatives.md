# Regenerating Derivatives with Drush

The module "Islandora Batch Derivative Trigger" can be used to regenerate all object derivatives for a set of items.

For help, use `drush deriv-regen -h`.

Most often, this is used when something goes wrong and derivatives fail to generate on a batch ingest. The most common workflows used by the metadata librarian are (1) regenerate derivatives for a whole collection, if the problem affects an entire collection or multiple items in a small collection; or, (2) regenerate derivatives for a list of PIDs when the affected items are from a set that constitutes only part of a large collection.

For scenario (1), use:

`drush deriv-regen --user={username} --collection={namespace}:collection`

For scenario (2), use:

`drush deriv-regen --user={username} --pids={PIDlist}`

Where {PIDlist} is a comma-delimited list of PID numbers whose derivatives will be regenerated, such as "state-lhp:10786,state-lhp:10787,state-lhp:10788,state-lhp:10789". See [Creating a PID List](create_pid_list.md).

- - - - -

## Ref  
[Islandora Batch Derivative Trigger](https://github.com/lsulibraries/islandora_batch_derivative_trigger)
