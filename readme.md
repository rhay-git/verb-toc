# verb-toc [![NPM version](https://img.shields.io/npm/v/verb-toc.svg)](https://www.npmjs.com/package/verb-toc) [![Build Status](https://img.shields.io/travis/jonschlinkert/verb-toc.svg)](https://travis-ci.org/jonschlinkert/verb-toc)

> Verb generator that adds middleware for creating and injecting a table of contents into a markdown document.

## Install

Install globally with [npm](https://www.npmjs.com/)

```sh
$ npm i -g verb-toc
```

**HEADS UP!!!**

This only works with Verb v0.9.0 and higher!

## Usage

```js
var toc = require('verb-toc');
```

**How it works**

Simply add a `<!!-- toc -->` HTML comment to any markdown document

**Middleware**

The main export is a function that when invoked with an instance of `verb` will automatically register two middleware functions:

* a `.postLayout` (`createToc`) middleware that creates the table of contents after a layout has been applied
* a `.preWrite` (`injectToc`) middleware that injects the table of contents back into the document after all other plugins have run.

Both middleware functions are also exposed as properties on `module.exports`, so you can try other stages if you want. Be warned that there are pros and cons to most middleware stages, in my own experience these stages work really well and seem to result in the fewest unwanted side-effects.

**Register the middleware**

In your (v0.9.0 and higher) `verbfile.js`:

```js
module.exports = function(verb) {
  verb.extendWith(require('verb-toc'));
  
  // use any template engine, but you must call `.renderFile` 
  // (below) to trigger the necessary middleware stages
  verb.engine('*', require('engine-base'));

  // example task
  verb.task('docs', function(cb) {
    return verb.src('docs/*.md', { cwd: __dirname })
      .pipe(app.renderFile('*'))
      .pipe(verb.dest('dist'));
  });

  verb.task('default', ['docs']);
};
```

_(In v0.9.0 and higher, verbfiles that export a function are recognized by verb as "generators", allowing them to be locally or globally installed, and composed with other generators. You can alternatively export an instance of verb, but it's not as fun...)_

## Related projects

* [markdown-toc](https://www.npmjs.com/package/markdown-toc): Generate a markdown TOC (table of contents) with Remarkable. | [homepage](https://github.com/jonschlinkert/markdown-toc)
* [verb](https://www.npmjs.com/package/verb): Documentation generator for GitHub projects. Verb is extremely powerful, easy to use, and is used… [more](https://www.npmjs.com/package/verb) | [homepage](https://github.com/verbose/verb)

## Generate docs

Generate readme and API documentation with [verb](https://github.com/verbose/verb):

```sh
$ npm i -d && npm run docs
```

## Running tests

Install dev dependencies:

```sh
$ npm i -d && npm test
```

## Contributing

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/verb-toc/issues/new).

## Author

**Jon Schlinkert**

* [github/jonschlinkert](https://github.com/jonschlinkert)
* [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

## License

Copyright © 2016 [Jon Schlinkert](https://github.com/jonschlinkert)
Released under the [MIT license](https://github.com/jonschlinkert/verb-toc/blob/master/LICENSE).

***

_This file was generated by [verb](https://github.com/verbose/verb), v0.9.0, on February 12, 2016._