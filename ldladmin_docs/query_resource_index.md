# Querying the Resource Index

The LDL Resource Index can be accessed at (http://louisianadigitallibrary.org//fedora/risearch)[http://louisianadigitallibrary.org//fedora/risearch].

Get the username and password for the resource index from a site administrator.

## Example Queries

Some basic sorts of things you can do with SPARQL queries include:

- Find all objects in the collection 'lsuhsc-p15140coll49':
```
SELECT ?pid
FROM <#ri>
WHERE {
?pid <fedora-rels-ext:isMemberOfCollection> <info:fedora/lsuhsc-p15140coll49:collection>
}
ORDER BY ?pid
```

- Find all objects in the repository with the 'Book' content model:

```
SELECT ?pid
FROM <#ri>
WHERE {
?pid <fedora-model:hasModel> <info:fedora/islandora:bookCModel>
}
ORDER BY ?pid
```

- Find all objects in the collection 'lsuhsc-p15140coll49' with the 'Book' content model:
```
SELECT ?pid
FROM <#ri>
WHERE {
?pid <fedora-rels-ext:isMemberOfCollection> <info:fedora/lsuhsc-p15140coll49:collection> .
?pid <fedora-model:hasModel> <info:fedora/islandora:bookCModel>
}
ORDER BY ?pid
```

More complex queries can be found at these links; you'll need permissions in GitHub to access.

- Sample SPARQL Queries: https://github.com/lsulibraries/internal-docs/blob/master/source/sparql.rst
- Removing Orphaned Pages (and other things): https://github.com/lsulibraries/internal-docs/blob/master/replace_datastreams.rst
