# Simple file cache

A simple file cache that is easy to use and doesn't need a lot of set up. I made this for my [portfolio site project thingy](https://github.com/MichielvdVelde/portfolio-site) and extracted it.

## Install

```
npm i file-cache-simple
```

# Use

```js
let FileCacheSimple = require('file-cache-simple');
let cache = new FileCacheSimple(); // see below for options

// Store some data
cache.set('key.name', 'some data');

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
	'prefix': 'cs' // cache files are prefixed with this
};
```

# Changelog

* v0.0.1 - v0.0.2 - 11 December 2015
  * (0.0.2) Add dependencies
  * (0.0.1) Initial commit

## License

Copyright 2015 Michiel van der Velde.

This software is licensed under [the MIT License](LICENSE).
