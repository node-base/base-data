# base-data [![NPM version](https://img.shields.io/npm/v/base-data.svg)](https://www.npmjs.com/package/base-data) [![Build Status](https://img.shields.io/travis/jonschlinkert/base-data.svg)](https://travis-ci.org/jonschlinkert/base-data)

> adds a `data` method to base-methods.

- [Usage](#usage)
- [API](#api)
  * [[.dataLoader](index.js#L50)](#-dataloader--indexjs-l50-)
  * [[.data](index.js#L85)](#-data--indexjs-l85-)
- [Glob patterns](#glob-patterns)
- [Namespacing](#namespacing)
- [Related projects](#related-projects)
- [Running tests](#running-tests)
- [Contributing](#contributing)
- [Author](#author)
- [License](#license)

_(TOC generated by [verb](https://github.com/verbose/verb) using [markdown-toc](https://github.com/jonschlinkert/markdown-toc))_

## Usage

Adds a `data` method to [base-methods][] that can be used for setting, getting and loading data onto a specified object in your application.

```js
var Base = require('base-methods');
var data = require('base-data');

// instantiate `Base`
var base = new Base();
// add `data` as a plugin
base.use(data());
```

**Examples**

Add data:

```js
app.data('a', 'b');
app.data({c: 'd'});
app.data('e', ['f']);
console.log(app.cache.data);
//=> {a: 'b', c: 'd', e: ['f']}
```

**cache.data**

By default, all data is loaded onto `app.cache.data`. This can be customized by passing the property to use when the plugin is initialized.

For example, the following set `app.foo` as object for storing data:

```js
app.use(data('foo'));
app.data('a', 'b');
console.log(app.foo);
//=> {a: 'b'}
```

## API

### [.dataLoader](index.js#L50)

Register a data loader for loading data onto `app.cache.data`.

**Params**

* `ext` **{String}**: The file extension for to match to the loader
* `fn` **{Function}**: The loader function.

**Example**

```js
var yaml = require('js-yaml');

app.dataLoader('yml', function(str, fp) {
  return yaml.safeLoad(str);
});

app.data('foo.yml');
//=> loads and parses `foo.yml` as yaml
```

### [.data](index.js#L85)

Load data onto `app.cache.data`

**Params**

* `key` **{String|Object}**: Key of the value to set, or object to extend.
* `val` **{any}**
* `returns` **{Object}**: Returns the instance of `Template` for chaining

**Example**

```js
console.log(app.cache.data);
//=> {};

app.data('a', 'b');
app.data({c: 'd'});
console.log(app.cache.data);
//=> {a: 'b', c: 'd'}

// set an array
app.data('e', ['f']);

// overwrite the array
app.data('e', ['g']);

// update the array
app.data('e', ['h'], true);
console.log(app.cache.data.e);
//=> ['g', 'h']
```

## Glob patterns

Glob patterns may be passed as a string or array. All of these work:

```js
app.data('foo.json');
app.data('*.json');
app.data(['*.json']);
// pass options to node-glob
app.data(['*.json'], {dot: true});
```

## Namespacing

Namespacing allows you to load data onto a specific key, optionally using part of the file path as the key.

**Example**

Given that `foo.json` contains `{a: 'b'}`:

```js
app.data('foo.json');
console.log(app.cache.data);
//=> {a: 'b'}

app.data('foo.json', {namespace: true});
console.log(app.cache.data);
//=> {foo: {a: 'b'}}

app.data('foo.json', {
  namespace: function(fp) {
    return path.basename(fp);
  }
});
console.log(app.cache.data);
//=> {'foo.json': {a: 'b'}}
```

## Related projects

* [base-cli](https://www.npmjs.com/package/base-cli): Plugin for base-methods that maps built-in methods to CLI args (also supports methods from a… [more](https://www.npmjs.com/package/base-cli) | [homepage](https://github.com/jonschlinkert/base-cli)
* [base-config](https://www.npmjs.com/package/base-config): base-methods plugin that adds a `config` method for mapping declarative configuration values to other 'base'… [more](https://www.npmjs.com/package/base-config) | [homepage](https://github.com/jonschlinkert/base-config)
* [base-methods](https://www.npmjs.com/package/base-methods): base-methods is the foundation for creating modular, unit testable and highly pluggable node.js applications, starting… [more](https://www.npmjs.com/package/base-methods) | [homepage](https://github.com/jonschlinkert/base-methods)
* [base-options](https://www.npmjs.com/package/base-options): Adds a few options methods to base-methods, like `option`, `enable` and `disable`. See the readme… [more](https://www.npmjs.com/package/base-options) | [homepage](https://github.com/jonschlinkert/base-options)
* [base-pipeline](https://www.npmjs.com/package/base-pipeline): base-methods plugin that adds pipeline and plugin methods for dynamically composing streaming plugin pipelines. | [homepage](https://github.com/jonschlinkert/base-pipeline)
* [base-plugins](https://www.npmjs.com/package/base-plugins): Upgrade's plugin support in base-methods to allow plugins to be called any time after init. | [homepage](https://github.com/jonschlinkert/base-plugins)
* [base-store](https://www.npmjs.com/package/base-store): Plugin for getting and persisting config values with your base-methods application. Adds a 'store' object… [more](https://www.npmjs.com/package/base-store) | [homepage](https://github.com/jonschlinkert/base-store)

## Running tests

Install dev dependencies:

```sh
$ npm i -d && npm test
```

## Contributing

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/base-data/issues/new).

## Author

**Jon Schlinkert**

* [github/jonschlinkert](https://github.com/jonschlinkert)
* [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

## License

Copyright © 2016 [Jon Schlinkert](https://github.com/jonschlinkert)
Released under the MIT license.

***

_This file was generated by [verb](https://github.com/verbose/verb) on January 06, 2016._