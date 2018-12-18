# Updating Metadata Web Forms

## Preparation

It is highly recommended that you create, edit, and test web forms and their updates in an LDL development environment. The "Dora Box" is ideal for this purpose. Dora can be cloned from https://github.com/lsulibraries/dora.

To access the LDL Dev user interface: from the Dora directory, vagrant up, then in a web browser go to localhost:8000 and login with admin/admin.

The GitHub repository for the metadata forms is located at https://github.com/lsulibraries/islandora_ingest_forms.

*Note:* When working in a development environment, you'll want to make sure you're starting from the most current version of the form(s). Because the form is edited through the site and not directly in the build, the surest way to do this is to export the form from Production and import it to your dev system. Of course, best practice is to commit to GitHub whenever an update is made -- so, the version of the form in GitHub *should* match the Production version.

## About LDL Custom Forms

Custom forms provided by LSU Libraries for the LDL are:

- *LDL Default MODS Form* - Includes all fields covered in the LDL Guidelines for Descriptive Metadata except (where noted) and should be associated with all content models in use by the LDL except Collection CM.
- *LDL Collection MODS Form* - Built specifically for collection-level metadata and should only be associated with the Collection CM.
- *LDL Core MODS Form* - Can be used to build minimal records; especially useful for compound child objects. Should be associated with all content models in use by the LDL except Collection CM. Contains only the following fields:
    - Title
    - Parent Item Title
    - Identifier (Item Number)
    - Contributing Repository
    - Date
    - Type of Resource
    - Internet Media Type
    - Digital Origin
    - Digital Collection
    - Relation
    - Rights
    - Contact Information
    - Record Info
- LDL Basic Form, Training Version - Specifically designed for in-person training in 2017 and 2018. This form is designed with deliberate flaws (specifically in Subject field) for one of the example training exercises.

## Process  

1. To navigate to the metadata forms at the Form Builder page: From the top menu, select `Islandora`, then `Form Builder`. You should see a long list of existing forms, most of which are built in to Islandora. The custom LDL forms will appear at the bottom of the list.

1. For new forms, use the `Create Form` or `Import Form` options at the top. To update an existing form, locate the form in the list and click the `Edit` option.

1. **For help with the form building/editing process itself,** please refer to the Islandora Wiki's documentation, [Creating and Working With XML Forms](https://github.com/Islandora/islandora/wiki/Creating-and-Working-With-XML-Forms). As the wiki says, "XML Form builder is quite possibly the most intimidating part of Islandora" -- and as such, those mechanics are not covered here!

1. When your edits are done, for a new form, you'll need to associate the form with one or more Content Models. Note that you cannot add multiple Content Models at once, but will need to repeat the

- Return to the Form Builder page
- Locate the line for the form you've worked on
- Click `Associate`
- Add an association:
    - For Content Model, begin typing the name of the content model and it should autocomplete
    - For Metadata Datastream ID, enter MODS
    - For Title Field, use the first instance of ['titleInfo']['title']`
    - For XSL Transform, use `[...]/mods_to_dc.xsl`
    - For Self XSL Transform, use `[...]/blankNodes.xsl`

1. When finished, test the form thoroughly. It is recommended that you test at least two ways:

- By creating a new item with the form (ensures that XML is written as expected and doesn't create encoding errors)
- By editing an existing item with the form (ensures that XML is read and updated as expected)

1. Once you are satisfied that your form is functioning correctly, export it and commit it to the GitHub [Islandora Ingest Forms](https://github.com/lsulibraries/islandora_ingest_forms) repository.

1. Import the form in the Test site at test.louisianadigitallibrary.org/admin/islandora/xmlform/forms. If you are replacing an existing form, you will need to delete it from Test first, then Import using the same name. Add Content Model association(s) as above. Repeat the testing procedure in the Test site.

1. _With clearance from Site Admins_, import the form in the Production site at louisianadigitallibrary.org/admin/islandora/xmlform/forms. Again, if you are replacing an existing form, you will need to delete it from Test first, then Import with the same name. Add Content Model association(s) as above.
