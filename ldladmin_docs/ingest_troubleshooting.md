# Troubleshooting Ingest Failures  

## About

Sometimes one or more items in a batch ingest fails. When this happens, the error message gives only the PID that the item would have had -- which, of course, doesn't exist. And typically, the batch process does not go in ingest-package-filename order, which means that the failed PID is not useful for identification. Especially in a large collection, it can be a challenge to track down the small number that are missing.   

In order to find the item(s) for troubleshooting, an LDL Admin can use Datastream CRUD to export the metadata files, then use XQuery to extract data to compare with the prepared ingest package.

## Process  

#### Find out how many items failed to ingest.

1. While logged in, go to your Batch Ingest Set (list of sets available at http://www.louisianadigitallibrary.org/admin/reports/islandora_batch_sets)
1. In the Item State drop-down, select `Error` and click `Apply`.
1. The number of failed items will be shown at the top of the page.

![alt text][error_report]

#### Use Islandora Datastream CRUD to export the MODS datastreams for the collection.

Follow the instructions from [Batch Editing with CRUD](batch_edit_with_crud.md) to create the PID file, fetch MODS (use `--dsid=MODS`), and copy the MODS files to a local directory, unzipping them into the destination folder.  

_Note: If you do not get the number of PIDs you expected, especially if you ingested the items very recently, the collection may not have finished indexing. See [Manually Indexing a Collection](indexing)._

#### Use XQuery to get a list of identifiers present in the ingested items in the collection.

For this step, any field where every record in the collection has exactly one unique instance of that field will work. Typically this will be an Identifier field. If the field contents are the same as the file names, it can make things easier.

This example ([downloadable HERE](ingest_troubleshooting/get_idetifier.xquery)) has the exported MODS records in a directory called `troubleshooting/`, with the full path as shown. The XQuery uses a `mods:identifier` element that has `@displayLabel='Call Number`; the files in the ingest package use the call number field value for their file names. The '&#xa;' entity is a newline character.

```
declare namespace mods = "http://www.loc.gov/mods/v3";

for $mods in collection('file:///g:/ldl/lsu-music/troubleshooting/')
    let $identifier := $mods//mods:identifier[@displayLabel='Call Number']/text()
    order by $identifier
return concat('&#xa;',$identifier)
```

1. Update the XQuery file as needed, based on your data and filepaths.

1. To run the XQuery in Oxygen:
    * Open the XQuery file in Oxygen and go to the XQuery Debugger.
    * Set the XML drop-down to ( None ) and set the XQuery drop-down to the XQuery file.
    * Execute the XQuery with the Run button.

1. The output should be a single identifier value per line, with the same number of lines as MODS files.

#### Reconcile the XQuery output identifiers with the source identifiers in the prepared ingest package.

There are a number of ways to go about reconciling; this method uses a spreadsheet application.

1. If you already have the source metadata in a spreadsheet, you can simply insert two columns next to the appropriate identifier column in the existing sheet. Alternatively, copy and paste the identifier column into a new sheet. __Be sure to sort the sheet by the identifier column.__

1. If you only have the source metadata in XML files, then you can tweak the above XQuery to fetch the list of original source identifiers.
    * This example has the exported MODS records in a directory called `processed/`, with the full path as shown. In this case, the directory also contains the object files for the ingest package; the `?select=*.xml` is used to select only the XML files.

    ```
    declare namespace mods = "http://www.loc.gov/mods/v3";

    for $mods in collection('file:///g:/ldl/lsu-music/processed/?select=*.xml')
        let $identifier := $mods//mods:identifier[@displayLabel='Call Number']/text()
        order by $identifier
    return concat('&#xa;',$identifier)
    ```
    * Run this XQuery in Oxygen as above; the output should be a single identifier value per line, with the same number of lines as MODS files.
    * Copy the output of the *source* identifier XQuery into a blank spreadsheet, in the A column.

1. Copy the output of the *ingested* identifier XQuery into the B column.
    * This column should have the number of rows in the A column minus the number of failed ingest items.

1. In the C column, enter the following formula: `=A1=B1`
    * Substitute the column letters and row numbers as needed, particularly if reusing your original source metadata spreadsheet instead of starting with a blank one.
    * Unless the first row was an error row, the cell should evaluate to `TRUE`.
    * Copy this formula down the C column to the end.

1. Use conditional formatting to find the `FALSE` cells. The first FALSE cell should be the first missing item. On the missing item row, insert a cell in the B column (the ingested identifier column), shifting the following cells in the B column down.

![alt text][conditional_formatting]

1. Record the identifiers of all of the `FALSE` rows. These are the identifiers of the missing items.


[error_report]: ingest_troubleshooting/error_report.jpg "Error report for Batch Set 491"
[conditional_formatting]: ingest_troubleshooting/conditional_formatting.jpg "Spreadsheet with conditional formatting"
