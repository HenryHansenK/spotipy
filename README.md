# Spotipy

##### A light weight Python library for the Spotify Web API

![Tests](https://github.com/plamere/spotipy/workflows/Tests/badge.svg?branch=master) [![Documentation Status](https://readthedocs.org/projects/spotipy/badge/?version=latest)](https://spotipy.readthedocs.io/en/latest/?badge=latest)

## Documentation

Spotipy's full documentation is online at [Spotipy Documentation](http://spotipy.readthedocs.org/).

## Installation

```bash
pip install spotipy
```

alternatively, for Windows users 

```bash
py -m pip install spotipy
```

or upgrade

```bash
pip install spotipy --upgrade
```

## Quick Start

A full set of examples can be found in the [online documentation](http://spotipy.readthedocs.org/) and in the [Spotipy examples directory](https://github.com/plamere/spotipy/tree/master/examples).

To get started, install spotipy and create an app on https://developers.spotify.com/.
Add your new ID and SECRET to your environment:

### Without user authentication

```python
import spotipy
from spotipy.oauth2 import SpotifyClientCredentials

sp = spotipy.Spotify(auth_manager=SpotifyClientCredentials(client_id="YOUR_APP_CLIENT_ID",
                                                           client_secret="YOUR_APP_CLIENT_SECRET"))

results = sp.search(q='weezer', limit=20)
for idx, track in enumerate(results['tracks']['items']):
    print(idx, track['name'])
```

### With user authentication

A redirect URI must be added to your application at [My Dashboard](https://developer.spotify.com/dashboard/applications) to access user authenticated features.

```python
import spotipy
from spotipy.oauth2 import SpotifyOAuth

sp = spotipy.Spotify(auth_manager=SpotifyOAuth(client_id="YOUR_APP_CLIENT_ID",
                                               client_secret="YOUR_APP_CLIENT_SECRET",
                                               redirect_uri="YOUR_APP_REDIRECT_URI",
                                               scope="user-library-read"))

results = sp.current_user_saved_tracks()
for idx, item in enumerate(results['items']):
    track = item['track']
    print(idx, track['artists'][0]['name'], " – ", track['name'])
```

## Example of getting artist image with artist's name

```python
import spotipy
import sys
from spotipy.oauth2 import SpotifyClientCredentials

spotify = spotipy.Spotify(auth_manager=SpotifyClientCredentials())

if len(sys.argv) > 1:
    name = ' '.join(sys.argv[1:])
else:
    name = 'Radiohead'

results = spotify.search(q='artist:' + name, type='artist')
items = results['artists']['items']
if len(items) > 0:
    artist = items[0]
    print(artist['name'], artist['images'][0]['url'])
```
## Reporting Issues

For common questions please check our [FAQ](FAQ.md).

You can ask questions about Spotipy on
[Stack Overflow](http://stackoverflow.com/questions/ask).
Don’t forget to add the *Spotipy* tag, and any other relevant tags as well, before posting.

### Reporting Bugs

If you have suggestions, bugs or other issues specific to this library,
file them [here](https://github.com/plamere/spotipy/issues).
Or just send a pull request.

When reporting a bug please fill out all the given fields: 
**Describe the bug**
A clear and concise description of what the bug is and where/when it occured. Does the program terminate? Is the retrived information correct? Which endpoints are you making a call to? Include formatted text, not screen shots.

**Your code**
Share a complete minimal working example. Include libraries used.

**Expected behavior**
A clear and concise description of what you expected to happen.

**Output**
Paste and format errors (with complete stacktrace) or logs. Make sure to remove sensitive information.

You can find these catagories by navagating to the bug report [link](https://github.com/plamere/spotipy/issues) then selecting "New issue" and then "Get started" next to Bug Report on the following page.

Please fill out all above fields. The information helps identify bugs faster, enabling bug patches to be released faster. Leaving any field blank may resort in your report going unanswered. 