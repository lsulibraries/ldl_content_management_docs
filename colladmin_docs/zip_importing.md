# Zip importing items #
## Single-item Content Models ##

*****

_Note: You must already have both your collection container and your .zip archive(s) created. Please refer to additional documentation:_
- [Adding a new collection](create_collection.md)
- [Structuring ingest packages](structuring_ingest_packages.md)

*****

1.	From the Islandora Repository ("All Collections"), navigate to the appropriate collection page (`{namespace}:collection`).

1.	Click the `Manage` tab.

1. 	In the Manage window, click the `Collection` button.

1.	In `Manage collection policy`, select the appropriate Content Model(s) for the collection items; for this import method, applicable Content Models are:  

*	Islandora PDF Content Model
*	Islandora Audio Content Model
*	Islandora Large Image Content Model
*	Islandora Video Content Model
*	_Be sure to click `Update collection policy`._

1.	At the top of the Collection window, click `+ Batch Import Objects.`

1. 	In the Importer drop-down, select `ZIP File Importer.`

1.	In the Zip Batch Importer window:
	*	Click `Choose File`.
	*	Browse to the .zip file containing the XML metadata files and paired object files for the collection, select, and click `Open`.
	*	Click `Upload`.
	*	In the Content Model block, check the box by the content model for the type of object in the zip file.
	*	In the Object Namespace drop-down, select the collection namespace.
	*	Click `Import`.

1.	When the import process completes, view the queue to check for errors; in the Islandora Batch Queue page, select "Error" in the Item State drop-down.
