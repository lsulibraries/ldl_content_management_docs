# Structuring Ingest Packages

## About

An ingest package consists of digital object files (such as images and documents) and corresponding metadata files (MODS XML files). Supplemental files such as OCR or transcriptions, thumbnails, etc. may be included in an ingest package as well, depending on the content type.  

The following guidance is used to prepare collections of items for ingest into Islandora. The resulting zipped ingest package may be uploaded either through the GUI or using Drush.

If the collection contains different types of objects - meaning different Content Model types - (PDFs, images, audio files, etc.) then you will need separate .zip files for each object type - they cannot be mixed in the same .zip file. In the .zip, each object file should have a corresponding XML metadata file with an identical filename (except the extension)

The practical size limit for a single zip file for ingest in the GUI is 4GB. Larger collections should be separated into multiple zip files or ingested using Drush.

## Simple Objects

### Preparing Simple Objects for Ingest 

Structuring an ingest package for simple objects is straightforward. This applies to content types: large image, PDF, audio, and video.

The ingest package should consist of a single flat directory, where each object has one object file and one MODS metadata file. The pair of files should match exactly except for the extension; capitalization does count. Example:

```
{top_level_directory}/
    image01.jp2
    image01.mods
    image02.jp2
    image02.mods
    image03.jp2
    image03.mods
```    



## Compound Objects  

### Preparing Compounds for Ingest  

The required directory for the compound object LDL ingest package is thus:  

- A single top-level directory, which can be named anything.
    - Under the top level, one subdirectory for each compound parent, which can be named anything.
        - Under the compound parent directory level:
            - There must be one MODS file named "MODS.xml" (which describes the whole compound);
            - And, there must be one subdirectory per child object, named using the child's sequence number only.
                - In each child directory, there must be one object file named "OBJ" plus the file extension -- "OBJ.jp2", "OBJ.pdf", "OBJ.mp3", or "OBJ.mp4".
                - In each child directory, there must be one MODS file named "MODS.xml" (which describes the child item).
```
{top_level_directory}/  
    {compounddobject1}/  
        01/
            MODS.xml  
            OBJ.jp2   
        02/
            MODS.xml  
            OBJ.jp2   
    {compounddobject2}/  
        01/
            MODS.xml  
            OBJ.jp2   
        02/
            MODS.xml  
            OBJ.jp2   
        03/
            MODS.xml  
            OBJ.jp2   
        04/
            MODS.xml  
            OBJ.jp2   
    ...  
```                

### Preparing Compounds For MIK  

The required structure for MIK processing requires only that the object files be placed into a parent folder; MIK will create the child-level folders.

The compound parent directories as well as the child objects may have any file name (as long as they are recorded in the appropriate column in the metadata spreadsheet). However, the child object filenames must all end with a delimiter followed by the child object's sequence number. Example:

```
{top_level_directory}/  
    {compounddobject1}/  
        image_01.jp2  
        image_02.jp2  
    {compounddobject2}/  
        image_01.jp2  
        image_02.jp2  
        image_03.jp2  
        image_04.jp2  
    ...  
```

## Books  

The required directory for the LDL ingest package is thus:

- A single top-level directory, which can be named anything.
    - Under the top level, one subdirectory for each book, which can be named anything
        - Under the book directory level:
            - There must be one MODS file named "MODS.xml" (which describes the whole book);
            - Optionally, there may be one PDF file named "PDF.pdf";
            - And, there must be one subdirectory per page, named using the page number only.
                - In each page directory, there must be one JP2 image file named "OBJ.jp2"; optionally, there may be one OCR TXT file named "OCR.txt".

```
{top_level_directory}/
    {book_001}/
        MODS.xml
        PDF.pdf *
        001/
            OBJ.jp2
            OCR.txt *
        002/
            OBJ.jp2
            OCR.txt *
        ...
    {book_002}/
        MODS.xml
        PDF.pdf *
        001/
            OBJ.jp2
            OCR.txt *
        002/
            OBJ.jp2
            OCR.txt *
        ...
    {book_003}/
        MODS.xml
        PDF.pdf *
        001/
            OBJ.jp2
            OCR.txt *
        002/
            OBJ.jp2
            OCR.txt *
        ...
    ...
```

## Newspapers  

The required directory for the LDL ingest package is thus:

- A single top-level directory, which can be named anything.
    - Under the top level, one subdirectory for each issue, which can be named anything.
        - _Issues are the equivalent of books, above._ Therefore, under the issue directory level:
            - There must be one MODS file named "MODS.xml" (which describes the whole issue);
            - Optionally, there may be one PDF file named "PDF.pdf";
            - And, there must be one subdirectory per page, named using the page number only.
                - In each page directory, there must be one JP2 image file named "OBJ.jp2"; optionally, there may be one OCR TXT file named "OCR.txt".

- To illustrate:
```
{publication_001}/
    {issue_001}/
        MODS.xml
        PDF.pdf *
        001/
            OBJ.jp2
            OCR.txt *
        002/
            OBJ.jp2
            OCR.txt *
        ...
    {issue_002}/
        MODS.xml
        PDF.pdf *
        001/
            OBJ.jp2
            OCR.txt *
        002/
            OBJ.jp2
            OCR.txt *
        ...
    {issue_003}/
        MODS.xml
        PDF.pdf *
        001/
            OBJ.jp2
            OCR.txt *
        002/
            OBJ.jp2
            OCR.txt *
        ...
    ...
```
