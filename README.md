# Playmate

Asynchronously scrapes and parses application data from the Google Play Store.
(Fork of play-scraper, a synchronous Google Play Store scraper, https://github.com/danieliu/play-scraper)

### Installation

Install with pip.

```
pip install playmate
```

#### details

Fetch an application's details.

```python
async with PlayMate() as mate:
    app_info = await mate.get_app_details(app_id)
```
* `app_id` the app id to get, e.g. `com.android.chrome` for Google Chrome.


#### collection

Fetch a list of applications from a collection, optionally filtered by category.

```python
async with PlayMate() as mate:
    collection = await mate.get_apps(
        coln_id, catg_id, max_page=max_page
    )
```
* `coln_id` a [collection](https://github.com/Gulats/playmate/blob/master/playmate/lists.py#L3) to fetch.
* `catg_id` a [category](https://github.com/Gulats/playmate/blob/master/playmate/lists.py#L12) to filter by.
* `max_page` (default 1, max 5) the number of pages to fetch with each page containing 120 records.


#### search

Fetch a list of applications matching a search query. Retrieves `20` apps at a time.

```python
async with PlayMate() as mate:
    search_results = await mate.search_apps(
        term, max_page=max_page
    )
```
* `term` query term(s) to search for.
* `max_page` (default 1, max 5) the number of pages to fetch with each page containing 48 records.


#### similar

Fetch a list of similar applications.

```python
async with PlayMate() as mate:
    similar_apps = await mate.get_similar_apps(app_id)
```
* `app_id` the app id to get, e.g. `com.supercell.clashofclans` for Clash of Clans.


#### custom settings

Add customisation to the request

```python
async with PlayMate(
    headers=dict(Origin='https://play.google.com'), 
    timeout=180, 
    hl='en', gl='us') as mate:
    app_info = await mate.get_app_details(app_id)
```
* `headers` the headers to be sent for each request
* `timeout` the total timeout for each request in seconds
* `hl` (default `en` for English) the language code to receive results in a specific language
* `gl` (default `us` for United States) the country code to receive results based from a specific country


#### manually close session

Manually close a persisted session

```python
mate = PlayMate()
app_info = await mate.get_app_details(app_id)
await mate.close()
```


### Tests

Run test:
```
make test
```