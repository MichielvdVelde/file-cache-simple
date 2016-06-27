# Simple file cache

A simple file cache that is easy to use and doesn't need a lot of set up. I made this for my [portfolio site project thingy](https://github.com/MichielvdVelde/portfolio-site) and extracted it.

## Install

```
npm i file-cache-simple
```

# Use

Every key is stored in its own file in `cacheDir`. You can set a `prefix` for the file name, see the options below. This also allows you to easily store data in subdirectories.

```js
const FileCacheSimple = require('file-cache-simple');
let cache = new FileCacheSimple(); // see below for options

// Store some data
// In this case, 'some data' is stored in cacheDir / prefix.key.json
// You can easily store JSON without stringifying it
cache.set('key.name', 'some data');

// You can also overwrite the default cache expiry time for a setting:
cache.set('key.name', { 'my': 'data' }, 43200 * 1000); // 12h

// And get some out
cache.get('key.name')
	.then(function(value) {
		if(!value || value === null) {
			return console.log('No value was found for this key');
		}
		return console.log('The value is', value);
	})
```

When `get()`ting a key, if it doesn't exist it returns `null`.

You can also change the default options by giving them to the constructor. The defaults are:

```js
const DEFAULT_OPTIONS = {
	'cacheDir': process.cwd() + '/cache',
	'cacheExpire': 3600 * 1000, // 1hr
	'prefix': 'cs', // cache files are prefixed with this
	'fixCacheExpire': false,
	'rejectOnNull': false
};
```

Is `fixCacheExpire` in the options is set to `true`, the active cache expiry time (either given through the settings or as the last argument to `set`) is stored in the JSON file as well and will be used to check if the cache is still fresh when `get()`ting it. This allows you to hve different expiry times for different keys.

If `rejectOnNull` is set to `true`, the promise will be rejected instead of resolving with `null`.

# Changelog

* v0.0.6 - 27 June 2016
  * Reject on expired cache when rejectOnNull is set, contributed by [TomTom101](https://github.com/TomTom101)
* v0.0.5 - 13 Januari 2016
  * Return promises on remove and write, contributed by [gregorskii](https://github.com/gregorskii)
* v0.0.4 - 31 December 2015
  * Add `rejectOnNull` to default options
* v0.0.3 - 14 December 2015
  * Add `fixCacheExpire` to `cache.set()` and default options
* v0.0.1 - v0.0.2 - 11 December 2015
  * (0.0.2) Add dependencies
  * (0.0.1) Initial commit

## License

Copyright 2015 Michiel van der Velde.

This software is licensed under [the MIT License](LICENSE).
