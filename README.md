# RecordSearch Data Scraper
> Tools for extracting data from the National Archives of Australia's online database, RecordSearch.


The National Archives of Australia's online database, RecordSearch, contains lots of rich, historical data. Unfortunately there's no API, so we have to resort to screen scrapers to get it out in reusable form. This is a library of scrapers to extract data about the main entities in RecordSearch – Items, Series, and Agencies – from both individual records, and search results.

The main classes are:

* `RSItem()` – an individual item
* `RSItemSearch()` – an advanced search for items
* `RSSeries()` – an individual series
* `RSSeriesSearch()` – an advanced search for series
* `RSAgency()` – an individual agency
* `RSAgencySearch()` – an advanced search for agencies

RecordSearch makes use of an odd assortment of sessions, redirects, and hidden forms, which make scraping a challenge. Please let me know if something isn't working as expected, as problems can be difficult to pin down!

This is a replacement for the original Recordsearch_tools library. The main changes are:

* Requirements have been updated (dropping RoboBrowser which seems to be no longer maintained)
* The full range of search parameters are now supported for Items, Series, and Agencies
* There's a built-in cache for improved efficiency and speed

See the [documentation](https://wragge.github.io/recordsearch_data_scraper/) for more details. And check out the [RecordSearch section](https://glam-workbench.net/recordsearch/) of the GLAM Workbench for examples of what's possible.

## Install

`pip install recordsearch-data-scraper`

## How to use

Retrieve an item using its Item ID.

```python
from recordsearch_data_scraper.scrapers import *

item = RSItem('3445411')
```

View the item data.

```python
item.data
```




    {'title': 'WRAGGE Clement Lionel Egerton : SERN 647 : POB Cheadle England : POE Enoggera QLD : NOK  (Father) WRAGGE Clement Lindley',
     'identifier': '3445411',
     'series': 'B2455',
     'control_symbol': 'WRAGGE C L E',
     'digitised_status': True,
     'digitised_pages': 47,
     'access_status': 'Open',
     'access_decision_reasons': [],
     'location': 'Canberra',
     'retrieved': '2021-04-25T21:12:22.620414+10:00',
     'contents_date_str': '1914 - 1920',
     'contents_start_date': '1914',
     'contents_end_date': '1920',
     'access_decision_date_str': '12 Apr 2001',
     'access_decision_date': '2001-04-12'}



Search for items.

```python
search = RSItemSearch(kw='wragge')
```

View the total number of items in the results set.

```python
search.total_results
```




    209



Access the first page of results.

```python
items = search.get_results()
```

View the first result.

```python
items['results'][0]
```




    {'series': 'A2479',
     'control_symbol': '17/1306',
     'title': 'The Wragge Estate. Property for sale.',
     'identifier': '149309',
     'access_status': 'Open',
     'location': 'Canberra',
     'contents_date_str': '1917 - 1917',
     'contents_start_date': '1917',
     'contents_end_date': '1917',
     'digitised_status': True}



The Series and Agency classes follow exactly the same pattern. See the [docs](https://wragge.github.io/recordsearch_data_scraper/) for more examples.
