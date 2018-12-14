# Searching the Louisiana Digital Library  

### Contents
* __[Search Essentials](#search-essentials)__
    * ["Search the LDL" Search Box](#search-the-ldl-search-box)  
    * [Searching from the Home Page](#searching-from-the-home-page)
    * [Searching within an Institution](#searching-within-an-institution)
    * [Searching within a Collection](#searching-within-a-collection)
* __[Understanding Search Results](#understanding-search-results)__  
    * [Viewing Search Results](#viewing-search-results)
    * [Refining Search Results](#refining-search-results)
* __[Search Strategies](#search-strategies)__  
    * [Default Behavior](#default-behavior)
    * [Search Query Syntax](#search-query-syntax)
    * [Advanced Search](#advanced-search)

- - - - -

## Search Essentials  

- - - - -

### "Search the LDL" Search Box

A search box appears on all pages in the Louisiana Digital Library at the top right corner (or top center, in small-screen view). A search from this search box will find items across the entire LDL, no matter what page you are currently on.  

![alt text][ldl_search]

To search from here:  

* Click inside the search box.  
* Type in your search terms.  
* Press Enter or click the search icon.  

- - - - -

### Searching from the Home Page  

The Louisiana Digital Library home page has a large search box in the center of the page. The box has the text prompt "Let's Discover Louisiana Together." A search from here will find items across the entire LDL.  

![alt text][home_page]  

To search from here:  

* Click inside the search box.  
* Type in your search terms.  
* Press Enter.  

- - - - -

### Searching within an Institution

Each LDL member institution's landing page features a large search box below the institution description. The box has the text prompt “Search these collections.” A search from here will find items in all the collections belonging to this institution.

![alt text][institution_search]

To search from here:  

* Click inside the search box.  
* Type in your search terms.  
* Press Enter or click the search icon.

- - - - -

### Searching within a Collection

Each LDL collection's landing page features a large search box below the collection description. The box has the text prompt “Search this collection.” A search from here will find items in this collection only.

![alt text][collection_search]

To search from here:  

* Click inside the search box.  
* Type in your search terms.  
* Press Enter or click the search icon.

- - - - -

## Understanding Search Results

- - - - -

![alt text][search_results]

### Viewing Search Results

The number of search results is shown at the top of the page.  

Each search result listed includes, where available, a thumbnail preview of the item, its title, subject terms, and other details. To view an item, click on either the thumbnail or the title. From an item, click the browser's back button to return to search results list.

- - - - -

### Refining Search Results

Search results are initially ordered by relevance. To change the order of the search results list:

* Locate the sorting options above the results list, by Title, by Name/Creator, or by Date
* Click one of these options to re-sort the results list (e.g. A-Z).
* Click the same option again to reverse the order (e.g. Z-A).
* Return to the original sort order by clicking the browser’s back button.

Search results can be filtered using several facets. To filter the search results list:

* Locate the list of facets to the left of the results list under "Refine Facets" (or top center, in small-screen view).
* Click a term or the plus sign next to it to only see results that include that term.
* Click the minus sign next to a term to eliminate all results that include that term.
* Click "Show More" for additional terms.

- - - - -

## Search Strategies

- - - - -

### Default Behavior  

The following tips about how the search engine works may help you understand your results better.

* The top search box as well as the home page, institution, and collection search boxes do basic keyword searching. This means that by default, they search in items' __entire descriptive records__ as well as any available __full text__ (OCR) for those items for a match of the search term(s) provided.
    * To search particular fields for a term, see [Advanced Search](#advanced-search) section.
* Multiple terms in a search box will be treated as an "OR" search, meaning that search results may match on any of the terms given. In relevancy order, results including all of the terms will be ranked higher, and results where terms appear in the same field will be ranked highest.
    * To search for all terms together, see [Search Syntax](#search-syntax) section.
* Common word endings, such as __-ing__ and __-s__, are generally ignored by the search engine.
    * For example, results should be exactly the same for _"musicians perform"_ as for _"musician performing"_.

- - - - -

### Search Syntax

The following strategies can be used for more powerful searches in the LDL.

#### Boolean search:  

Use __AND/OR/NOT__ to connect keywords.  

* To use this syntax, enter AND, OR, or NOT in all caps between terms in any search box.
* __AND__ will find items that include __all__ of the terms.
    * _magnolia AND tree_
* __OR__ will find items that include __any__ of the terms.
    * _magnolia OR live-oak_
* __NOT__ will omit any items that include a term.
    * _magnolia NOT flower_

#### Phrased search:  

Use quotation marks __""__ to search for multiple terms in sequence.

* _"magnolia street"_

![alt text][phrase_search]

Note the difference between a phrased search and an AND Boolean search.  

* With a phrased search, multiple words must appear within the item record as in the search query, together and in the same order.
* With an AND search, all words must appear in the item record, but do not have to be in the same field and can be in any order.

#### Wildcard search:

Use an asterisk __*__ as a wildcard to stand in for one or more letters or numbers.  

* This strategy is useful for variant spellings or word endings, uncertain spelling

#### Empty search:

Get a list of all the items within a particular context (i.e. a collection, an institution, or the entire LDL) by performing an empty search at that location.

* Navigate to the home page, the institution landing page, or the collection landing page you are interested in. Leave the search box blank and click the search icon (or click inside the search box to get your cursor there, and press Enter).
* This is useful for using the filtering and sorting options available on search results to browse a large set of items.

- - - - -

### Advanced Search

The Advanced Search panel works based on exact matches only, even if quotation marks are not included. Therefore, to search for two or more terms that don't necessarily need to be adjacent, use a Boolean in between terms or add a separate field choosing __AND__ from the drop-down menu.

  * The wildcard option may be especially useful in searching for dates.
    * _196*_ will find results from 1960-1969.


[ldl_search]: search_essentials_images/ldl_search.jpg "Top right search box"
[home_page]: search_essentials_images/home_page.jpg "Home page search box"
[search_results]: search_essentials_images/search_results.jpg "Search results for 'magnolia'"
[institution_search]: search_essentials_images/institution_search.jpg "Institution search box"
[collection_search]: search_essentials_images/collection_search.jpg "Collection search box"
[phrase_search]: search_essentials_images/phrase_search.jpg "Phrase search for 'magnolia' in search box"
