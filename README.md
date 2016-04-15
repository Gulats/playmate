# Play Store Scraper

Scrapes and parses application data from the Google Play Store.

### Installation

```
pip install -r requirements.txt
```

### Usage

* [details](#details): Fetches the details of an application.
* [collection](#collection): Fetches a list of applications and their details.
* [developer](#developer): Fetches applications offered by a developer.
* [suggestion](#suggestion): Fetches a list of query string suggestions.
* [search](#search): Fetches applications matching a search query.

#### details

Fetch an application's details by its `app_id`, e.g. `com.android.chrome` for Google Chrome.

```python
>>> import play_scraper
>>> print(play_scraper.details('com.android.chrome'))
{   
    'app_id': 'com.android.chrome',
    'category': [{'category_id': 'COMMUNICATION', 'name': u'Communication', 'url': 'https://play.google.com/store/apps/category/COMMUNICATION'}],
    'content_rating': u'Everyone',
    'current_version': u'Varies with device',
    'description': 'Browse fast on your Android phone and tablet with the Google Chrome browser you love on desktop. Pick up where you left ...',
    'description_html': 'Browse fast on your Android phone and tablet with the Google Chrome browser you love on desktop. Pick up where you left off on your other devices with tab sync, search by voice, and save up to 50% of data usage while browsing. <br/> ...',
    'developer': u'Google Inc.',
    'developer_address': u'1600 Amphitheatre Parkway, Mountain View 94043',
    'developer_email': 'apps-help@google.com',
    'developer_url': 'http://www.google.com/chrome/android',
    'editors_choice': False,
    'free': True,
    'histogram': {1: 350676, 2: 158345, 3: 325869, 4: 733685, 5: 2674148},
    'icon': 'https://lh3.ggpht.com/O0aW5qsyCkR2i7Bu-jUU1b5BWA_NygJ6ui4MgaAvL7gfqvVWqkOBscDaq4pn-vkwByUx',
    'in_app_purchases': None,
    'installs': [1000000000, 5000000000],
    'interactive_elements': [u'Unrestricted Internet'],
    'offers_iap': False,
    'price': '0',
    'recent_changes': u'Bug fixes and speedy performance improvements.',
    'required_android_version': u'Varies with device',
    'reviews': 4242723,
    'score': 4.230880260467529,
    'screenshots': ['https://lh4.ggpht.com/6D21o4j_OJUnVCTARqcdajTmX_5_8UJtzVuN91smALZBuMq0p3MIvwZj2qofXeqmFIU=h900-rw', ...],
    'size': u'Varies with device',
    'thumbnails': ['https://lh4.ggpht.com/6D21o4j_OJUnVCTARqcdajTmX_5_8UJtzVuN91smALZBuMq0p3MIvwZj2qofXeqmFIU=h310-rw', ...],
    'title': u'Chrome Browser - Google',
    'top_developer': True,
    'updated': u'March 25, 2016',
    'url': 'https://play.google.com/store/apps/details?id=com.android.chrome',
    'video': None
}
```

#### collection

Fetch a list of applications from a collection and an optional category.

Options:

* `collection` a [collection](https://github.com/danieliu/play-scraper/blob/master/play_scraper/lists.py#L59) to fetch.
* `category` (optional) a [category](https://github.com/danieliu/play-scraper/blob/master/play_scraper/lists.py#L3) to filter by.
* `results` (default 60) the number of apps to fetch.
* `page` (default 0) the page number to get. Multiplies by `results` to get the collection start index. Limit: `page * results <= 500`.
* `detailed` (default False) if True, sends a GET request per app to fetch the full details as in [details](#details).

```python
>>> import play_scraper
>>> print play_scraper.collection(
        collection='TRENDING',
        category='GAME_RACING',
        results=5,
        page=1)
[ { 'app_id': 'com.tinylabproductions.firefighters',
    'description': u'Grab your favorite fire fighters ride and go for a true hero adventure!',
    'free': True,
    'icon': 'https://lh3.googleusercontent.com/D3K9lGOrmBkvUyAdQSNslDE6Y_ma7CQO1YZ57kMJZ-hTIcyS_oTGEZTGOXR7JqqS6W4',
    'price': '0',
    'score': '3.8',
    'title': 'Fire Fighters Racing for Kids',
    'url': 'https://play.google.com/store/apps/details?id=com.tinylabproductions.firefighters'},
  { 'app_id': 'com.labexception.truckdrivercargo',
    'description': u'Drive trucks through dangerous roads and deliver cargo',
    'free': True,
    'icon': 'https://lh3.googleusercontent.com/_N_baVt-zIlPvuJEFvo3Bn3ywhDl_kNzH89VU2tbrHtbyDW2dt-gb5sXugdMML9fKA',
    'price': '0',
    'score': '3.9',
    'title': 'Truck Driver Cargo',
    'url': 'https://play.google.com/store/apps/details?id=com.labexception.truckdrivercargo'}, ...]
```

#### developer

Fetch a list of applications by a developer.

Options:

* `developer` the developer name to fetch applications, e.g. `Disney`. (Case sensitive)
* `results` (default 24) the number of apps to fetch. (Developer may have more or less published apps)
* `detailed` (default False) if True, sends a GET request per app to fetch the full details as in [details](#details).

```python
>>> import play_scraper
>>> print play_scraper.developer('Disney', results=5)
[ { 'app_id': 'com.disney.disneycrossyroad_goo',
    'description': u'An all-new take on the ultimate 8-bit endless adventure to cross the road!',
    'developer': 'Disney',
    'free': True,
    'icon': 'https://lh3.googleusercontent.com/mHHQ-GA_hu8shAEtzj8trGBOJK7dtMrmV4XXvjl49MQbIDHytb8kQenB4IaUB9NvYA',
    'price': '0',
    'score': '4.5',
    'title': 'Disney Crossy Road',
    'url': 'https://play.google.com/store/apps/details?id=com.disney.disneycrossyroad_goo'},
  { 'app_id': 'com.disney.disneydescendants_goo',
    'description': u'Join Mal, Evie, Jay & Carlos for a wickedly fun adventure in Descendants!',
    'developer': 'Disney',
    'free': True,
    'icon': 'https://lh3.googleusercontent.com/uzyRRHl7Jxy_TN1WKvp0rf1q9sS05JcTzmhILZI16Gbu4N7TGP88nHSQTPfBKwor5g',
    'price': '0',
    'score': '3.7',
    'title': 'Descendants',
    'url': 'https://play.google.com/store/apps/details?id=com.disney.disneydescendants_goo'}, ...]
```

#### suggestions

Fetch a list of autocompleted query suggestions.

```python
>>> import play_scraper
>>> print play_scraper.suggestions('cat')
[u'cat games', u'cat simulator', u'cat sounds', u'cat games for cats']
```

### Tests

Run tests:
```
python -m unittest discover
```