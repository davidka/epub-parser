# 📖 epub-parser

> A powerful yet easy-to-use epub parser

[![npm version](https://badge.fury.io/js/%40gxl%2Fepub-parser.svg)](https://badge.fury.io/js/%40gxl%2Fepub-parser)
[![build state](https://api.travis-ci.org/davidka/epub-parser.svg?branch=master)](https://travis-ci.org/davidka/epub-parser)

The package exports a simple parser function which use epub file as input and output JavaScript object.

As it is written in TypeScript, types are already included in the package.

Inspired by [@gxl/epub-parser](https://www.npmjs.com/package/@gxl/epub-parser) but without dependency to `fs`, which allows it to use this lib with react-native.

## Install

```bash
npm install davidka/epub-parser --save
```

or if you prefer yarn

```bash
yarn add davidka/epub-parser
```

## Usage

```js
import parser from 'davidka/epub-parser'
// if you use `require` don't forget to add `.default`
// const parser = require('simple-epub-parser').default

console.log('epub content:', parser(binaryData))
```

### parser(target: buffer, options?: object): EpubObject

#### target

type: `buffer`

#### EpubObject

The output is an object which contains `structure`, `sections`, `info` along with some other properties that deals with the epub file. They start with `_`. I don't recommend using these properties, since they are subscribed to change. They are where they are simply because JavaScript don't have native private member variable support, and sometimes they are helpful for debugging.

`structure` is the parsed `toc` of epub file, they contain information about how the book is constructed.

`sections` is an array of chapters or sections under chapters, they are referred in `structure`. Each section object contains the raw html string and a few handy methods to help you with you needs. `toMarkdown` convert the current section to markdown object. `toHtmlObjects` converts to html object. And a note about `src` and `href`, the `src` and `href` in raw html stay untouched, but the `toHtmlObjects` method resolves `src` to base64 string, and alters `href` so that they make sense in the parsed epub. And the parsed `href` is something like `#{sectionId},{hash}`.

### One more thing

It provides some util functions as well.

They can be used via

```js
import { parseLink, parseHTML, parseNestedObject, flattenArray } from 'davidka/epub-parser'
```

* parseLink
* parseHTML
* parseNestedObject

## How to contribute

* Raise an issue in the issue section.
* PRs are the best.

❤️
