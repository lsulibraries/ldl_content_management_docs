# Converting Spreadsheet Metadata to MODS

The MIK Wiki on GitHub is very thorough and useful, and should be consulted wherever the following instructions are insufficient.

- CSV to MODS Simple -- [Single file objects](https://github.com/MarcusBarnes/mik/wiki/Toolchain:-CSV-single-file-objects)
- CSV to MODS Compounds -- [Compound objects](https://github.com/MarcusBarnes/mik/wiki/Toolchain:-CSV-compound-objects)

### Prepare the Metadata Spreadsheet

An LDL Descriptive Metadata spreadsheet template is available, which has a corresponding mapping file to use when converting from spreadsheet to MODS using the Move-to-Islandora Kit (MIK).

LSU and LDL collection administrators / catalogers should follow the LDL Guidelines for Descriptive Metadata when completing their metadata spreadsheet. One spreadsheet should be completed for each collection.

Object files may be transmitted to LSU staff for inclusion in the MIK process to build a complete ingest package. The preferred method is to zip the directory of files (or directory of directories of files, for compound objects) and upload it to AWS. See [AWS for Collection Administrators](aws_for_colladmins.md)

### Set Up MIK

Follow the instructions for [Setting up MIK](setting_up_mik.md) to install the software.

### Review the Metadata Spreadsheet

- Verify that fields are filled out correctly
- Verify that filenames are present and point to files in the source directory
- Ensure that only either simple or compound items are present (otherwise, split into two files)
- Make note of customized field labels / column headers
- Make note of additional transforms (XSLT) that will be needed
- Scan for problematic characters

###  Convert Spreadsheet to CSV

- Save it as {filename}_md.csv with type Comma Separated Values
- Save in the project folder under the MIK directory

### Copy the Source Files

- Copy the directory of object files into the project folder under the MIK directory
- Create a directory in the project folder called "output"

### Update Helper Files

- MAPPING FILE:
    - Check that field names match those in LDL_masterModsMap.csv
    - If customizations are needed, save the updated mapping file with a new filename -- DO NOT OVERWRITE LDL_masterModsMap.csv
- CONFIG FILE:
    - Select either cpd_config.ini for compound objects or simple_config.ini for simple objects
    - Update paths and directory/file names for the current project; typically, update:
        - *config_id* - use the collection namespace  
        - *last_updated_on* - enter the date
        - *last_update_by* - enter your initials  
        - *input_file* - the path to the metadata csv file
        - *temp_directory* - (enter twice) the path to a directory where processing files will be added
        - *mapping_csv_path* - the path to the mapping file
        - *input_directory* - the path to the directory containing the object files
        - *output_directory* - the path to the directory where the output will be created  
        - *working_dir* - the path to a directory where XSLT processing files will be added
    - Include/exclude XSLT transforms (as "shutdownhooks") as needed; the most commonly used are:
        - *titleNonSort.xsl* - moves leading articles in the title to a nonSort subelement
        - *multiNamePart.xsl* - divides multiple names, if separated by semicolons, into separate name elements
        - *dateCreatedSplit.xsl* and *dateIssuedSplit.xsl* - converts specific natural language formatting of dateCreated or dateIssued fields into machine-readable format
        - *subjectSplit.xsl* - divides subject terms into separate subelements and wrapper elements
        - *locationMerge.xsl* - combines the subelements of multiple location elements into a single location element (ALWAYS INCLUDE)
        - *blankNodes.xsl* - removes empty elements and attributes (ALWAYS INCLUDE)
        - *OrderedTemplates.xsl* - puts elements in a designated order (ALWAYS INCLUDE)

- XSLT FILES:
    - Update / create as needed; these are found in the extras/lsu/xsl folder

### Run MIK

At vagrant box location,

```
vagrant up
vagrant ssh
cd /vagrant/mik
sudo su
php mik --config {filename}.ini
```

### Verify Output

- If there are errors, you will see a report of "problem files"; check the logs for details
    - Troubleshoot and re-run as needed, manually emptying the contents of the output directory, temp directory, and xslt working directory before re-processing.
- Spot check the MODS output
- ZIP and proceed to ingest

### Delete tiles from temp folder

- Delete the contents of the temp folder specified in the config file (otherwise you can get unintended results the next time you run MIK).


### Common Pitfalls

- Mismatches between column headers and mapping file values
- Mismatches between filenames in the directory vs. the spreadsheet
- Missing leading zeroes for compound child sequence numbers, or missing trailing sequence numbers in filenames
- Must manually delete files from /temp folder for metadata-related changes to take effect

- - - - -

## Ref  

- [Move to Islandora Kit](https://github.com/MarcusBarnes/mik)  
- Support files from some past MIK processes have been saved to the LSU Libraries U drive at ContentDMData/mik_csv-to-mods (use discerningly; some MODS field mappings are outdated per current guidelines)
