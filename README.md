pyLast
======

[![Build Status](https://travis-ci.org/hugovk/pylast.png?branch=master)](https://travis-ci.org/hugovk/pylast) [![Coverage Status](https://coveralls.io/repos/hugovk/pylast/badge.png?branch=master)](https://coveralls.io/r/hugovk/pylast?branch=master)

A Python interface to Last.fm (and other api-compatible websites such as Libre.fm).

Try using the pydoc utility for help on usage or see test_pylast.py for examples.

Original code can be found at http://code.google.com/p/pylast/ but hasn't been updated since 2011.

Features
--------

 * Simple public interface.
 * Access to all the data exposed by the Last.fm web services.
 * Scrobbling support.
 * Full object-oriented design.
 * Proxy support.
 * Internal caching support for some web services calls (disabled by default).
 * No extra dependencies but Python itself.
 * Support for other API-compatible networks like Libre.fm.
 * Python 3-friendly (Starting from 0.5).


Getting Started
---------------

Here's a simple code example to get you started. In order to create any object from pyLast, you need a Network object which represents a social music network that is Last.fm or any other API-compatible one. You can obtain a pre-configured one for Last.fm and use it as follows:

```
import pylast

# You have to have your own unique two values for API_KEY and API_SECRET
# Obtain yours from http://www.last.fm/api/account for Last.fm
API_KEY = "b25b959554ed76058ac220b7b2e0a026" # this is a sample key
API_SECRET = "425b55975eed76058ac220b7b4e8a054"

# In order to perform a write operation you need to authenticate yourself
username = "your_user_name"
password_hash = pylast.md5("your_password")

network = pylast.LastFMNetwork(api_key = API_KEY, api_secret = 
    API_SECRET, username = username, password_hash = password_hash)

# now you can use that object everywhere
artist = network.get_artist("System of a Down")
artist.shout("<3")


track = network.get_track("Iron Maiden", "The Nomad")
track.love()
track.add_tags(("awesome", "favorite"))

# type help(pylast.LastFMNetwork) or help(pylast) in a Python interpreter to get more help
# about anything and see examples of how it works
```

Testing
-------

test_pylast.py contains integration tests with Last.fm, and plenty of code examples.

You need a test account at Last.fm that can be cluttered with test data, and an API key and secret. Either copy test_pylast_example.yaml to test_pylast.yaml and fill out the credentials, or set them as environment variables like:

```
export PYLAST_USERNAME=TODO_ENTER_YOURS_HERE
export PYLAST_PASSWORD_HASH=TODO_ENTER_YOURS_HERE
export PYLAST_API_KEY=TODO_ENTER_YOURS_HERE
export PYLAST_API_SECRET=TODO_ENTER_YOURS_HERE
```

Then:
```
pip install pyyaml
./test_pylast.py
```

To run with coverage:
```
pip install 
pip install coverage
coverage run --source=pylast ./test_pylast.py
coverage report # for command-line report
coverage html   # for HTML report
open htmlcov/index.html
```