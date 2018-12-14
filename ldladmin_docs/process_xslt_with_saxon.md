# Processing XSL Transformations using Saxon

## About

XSL(T) is a powerful tool for making precise changes to batches of XML metadata records. Regular use cases for the LDL include making revisions to existing records (such as MODS records exported using [Datastream CRUD](batch_edit_with_crud.md)), conversion of metadata between XML schemas (such as harvesting DC records with OAH-PMH), and cleanup of XML metadata that originated in spreadsheets before platform ingest.

A transformation can be applied on a batch of files using [Oxygen's "Project" option](https://www.oxygenxml.com/doc/versions/18/ug-author/tasks/apply-batch-transformation.html). However, running it from the command line using Saxon can be a simpler approach.

## Setting Up Saxon

First, be sure to have downloaded Saxon to your local machine. Saxon HE can be downloaded from [SourceForge](https://sourceforge.net/projects/saxon/files/Saxon-HE/9.8/).

If you regularly run XSLT in a particular directory location on your computer, it may be useful to make a symbolic link/shortcut from the downloaded unzipped .jar location (shown as /opt/saxon) to this directory -- otherwise, you'll need to enter the full path to the .jar file when you use the command. To create a shortcut, from the destination directory, use:

`ln -s /opt/saxon/saxon9he.jar saxon9he.jar`

## Process

1. Place source XML files into a single directory.

1. Create XSLT stylesheet to effect the desired transformation.  
		- Testing the transformation on a sample XML file in Oxygen is recommended.

1. Create an output directory to hold the results of the transformation.

1. Run the following command:  
`java -jar {path_to/}saxon9he.jar -s:{path_to/source_directory} -xsl:{XSLT_filename}.xsl -o:{path_to/destination_directory}`  

1. As an example:
`java -jar /g/saxon9he.jar -s:lsu-sc-act/ -xsl:subcrud.xsl -o:revised/`  
		- In this example, the Saxon .jar file is in the G: directory; the source directory is named 'lsu-sc-act'; the output directory is named 'revised'; the XSLT stylesheet is named 'subcrud.xsl'; the XSLT stylesheet is in the same parent directory as both the source and output directories; and the command is run from that parent directory location.

1. If the XSLT stylesheet includes parameters, those may be passed in from the command as well; in the following command, the transformation takes a parameter called 'contributor' for which we pass the value 'lsu-sc'; and it takes a parameter called 'alias' for which we pass the value 'lsu-sc-act':  
`java -jar /g/saxon9he.jar -s:lsu-sc-act/ -xsl:subcrud.xsl -o:revised/ contributor=lsu-sc  alias=lsu-sc-act`

1. Review the output. The output directory should now be populated with modified files with the same names as the original source files.  
		- Since the source files have not been altered, you can make adjustments to the XSLT stylesheet if needed and run the command again.
		- Once the output is satisfactory, proceed as appropriate with upload, datastream replacement, etc.

- - - - -

## Ref  

- [Transforming XML with XSLT](http://dh.obdurodon.org/transformation-scenario.xhtml)

_Note:_ This document does not provide instructions for creating XSLT stylesheets. Some helpful resources for learning XSLT include:

- W3Schools, starting with [XSLT Introduction](https://www.w3schools.com/xml/xsl_intro.asp)
- Digital Humanities, starting with [Introduction to XSLT](http://dh.obdurodon.org/xslt-basics.xhtml)
- [Stack Overflow](https://stackoverflow.com/) for point-of-need help
- Professional Development Courses, such as [Library Juice Academy's XSLT Fundamentals](http://libraryjuiceacademy.com/189-XSLT.php)
- [Numerous books](https://whatpixel.com/10-best-xslt-books/)
