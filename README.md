# metalsmith slug

Add a `slug` property to the metadata for targeted files in your
[Metalsmith](http://www.metalsmith.io/), based on a particular property.
Useful for generating links to pages based on, say, their `title`.

## Installation

    npm install metalsmith-slug --save

## Usage

If you're not familiar with Metalsmith, [check it out](http://metalsmith.io). It's a versatile file processor that can be used for static site generation,
project scaffolding and more. It can be interacted with via a CLI or
JavaScript API.

### Metalsmith CLI

Add `metalsmith-slug` to your `metalsmith.json`.

```json
{
  "plugins": {
    "metalsmith-slug": {}
  }
}
```

### Metalsmith JavaScript API

Add `metalsmith-slug` to your project and `.use()` it.

```js
var slug = require('metalsmith-slug');

metalsmith.use(slug());
```

## Options

**patterns** `Array`: Glob patterns of files to match. Uses
[minimatch](https://github.com/isaacs/minimatch). Default: `[]`.

```js
metalsmith.use(slug({
  patterns: ['*.md', '*.rst'] // Defaults to all files
}));
```

**property** `String`: Property to generate the slug from. Default: `title`.

```js
metalsmith.use(slug({
  property: 'name'
}));
```

**renameFiles** `Boolean`: When set to `true`, will rename the files passed to
metalsmith-slug to the file's new slug property. Default: `false`.

```js
metalsmith.use(slug({
  renameFiles: true
}));
```

**slug options**: You can additionally use any of the options available for [node-slug][node-slug-options].

```js
// This are the defaults for node-slug 'pretty' mode
metalsmith.use(slug({
  replacement: '-',
  symbols: true,
  remove: /[.]/g,
  lower: false,
  charmap: [object Object], // slug.defaults.charmap
  multicharmap: [object Object], // slug.defaults.multicharmap
}));
```

Alternatively you can change the default node-slug mode:

```
metalsmith.use(slug({
  mode: 'rfc3986'
}));
```

## Manual override

Also, it's possible to override the `slug` property in a single file.
If you define a `slug` in the front matter, the plugin won't replace it with a new one.
However, it will apply the same [slug options][node-slug-options], if any.

```yaml
---
title: Something
slug: Something-Else
---
contents...
```

```js
metalsmith.use(slug());              // => {slug: 'Something-Else', ...}
metalsmith.use(slug({lower: true})); // => {slug: 'something-else', ...}
```

## Tests

`npm test` to run the tests.

## License

The MIT License (MIT)

Copyright (c) 2014 Nikhil Sonnad

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


[node-slug-options]: https://github.com/dodo/node-slug#options
