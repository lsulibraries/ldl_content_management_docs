# Structuring Ingest Packages

## About

An ingest package consists of digital object files (such as images and documents) and corresponding metadata files (MODS XML files). Supplemental files such as OCR or transcriptions, thumbnails, etc. may be included in an ingest package as well, depending on the content type.  

The following guidance is used to prepare collections of items for ingest into Islandora. The resulting zipped ingest package may be uploaded either through the GUI or using Drush.

Guidance is also provided for structuring source file directories for processing with MIK, which combines object files with metadata. The output of MIK will be structured as described for the ingest package.

If the collection contains different types of objects - meaning different Content Model types - (PDFs, images, audio files, etc.) then you will need separate .zip files for each object type - they cannot be mixed in the same .zip file. In the .zip, each object file should have a corresponding XML metadata file with an identical filename (except the extension)

The practical size limit for a single zip file for ingest in the GUI is 4GB. Larger collections should be separated into multiple zip files or ingested using Drush.

## Simple Objects



## Compound Objects  

The required structure for MIK processing requires only that the object files be placed into a parent folder; MIK will create the child-level folders. Thus:

{top_level_directory}/
├── compounddobject1
│   ├── image-01.tif
│   └── image-02.tif
├── compounddobject2
│   ├── image-01.tif
│   ├── image-02.tif
│   ├── image-03.tif
│   └── image-04.tif
└── compounddobject3
    ├── image_this_is_ok-01.tif
    └── this_too-02.tif

## Books  

The required directory for the LDL ingest package is thus:

- A single top-level directory, which can be named anything.
    - Under the top level, one subdirectory for each book, which can be named anything
        - Under the book directory level:
            - There must be one MODS file named "MODS.xml";
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
            - There must be one MODS file named "MODS.xml";
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
