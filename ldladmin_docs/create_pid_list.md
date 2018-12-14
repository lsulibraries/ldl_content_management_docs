# Creating a PID List

Many Islandora batch processes using Drush can take a list of item PIDs (i.e. "institution-collection:123"), in addition to the usual "collection" and/or "namespace" parameters. This may either be in the form of a "PID File" or a "PID List."

- A _PID File_ is a text file containing one PID per line, where the command takes the filename
- A _PID List_ is a comma-delimited list of PIDs, where the command takes the actual list

A common use case: If the targeted items are from a particular batch ingest, you can locate the batch set from the [Batch Sets list](http://louisianadigitallibrary.org/admin/reports/islandora_batch_sets?page=1), find the first and last PID number in the set, and generate a list of PIDs within that range.

## Using ListPIDs Python Script

The Python helper script [_listpids.py_](create_pid_list/listpids.py) (copied below) can be used to generate a text list of PIDs in a defined namespace with a defined range, writing PIDs in sequential order.

_Note:_ You'll need to [download and install Python](https://www.python.org/downloads/) if you don't have it.

To use the Python script:

- Update the script as follows:
    - Substitute the collection namespace in `collection`
    - Enter the number of the first PID in the range in `pidStart`
    - Enter the number of the last PID in the range in `pidEnd`
    - For a PID File, use as written below, with the newline character `\n` in the second `outFile.write` string
    - For a comma delimited list, substitute the `\n` character with a comma in the second `outFile.write` string
    - Save your changes
- Run with the command `python listpids.py`
    - A text file will be created using the namespace provided in `collection` above: `collection_pids.txt`
- For a PID File, use the filename in the Drush command
- For a PID List, copy and paste the contents of the file into the Drush command

```
collection = 'state-lhp'
pidStart = 10786
pidEnd = 10856
pids = range(pidStart, pidEnd)

outFile = open(collection + '_pids.txt' , 'w')

outFile.write(collection + ':')
outFile.write(('\n' + collection + ':').join(str(pid) for pid in pids))

outFile.close()
```

- - - - -

## Ref
[carakey/metadata_utils](https://github.com/carakey/metadata_utils
