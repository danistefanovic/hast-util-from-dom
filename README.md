# hast-util-from-dom [![Build Status][travis-badge]][travis]

Transform a DOM tree to [HAST][]

## Installation

[yarn][]:

```bash
yarn add hast-util-from-dom
```

[npm][]:

```bash
npm install hast-util-from-dom
```

## Usage

This utility is similar to [`hast-util-from-parse5`][hast-util-from-parse5], but is intended for browser use and therefore relies on the native DOM API instead of an external parsing library.

Say we have the following file, `example.html`:

```html
<!doctype html><title>Hello!</title><h1 id="world">World!<!--after--><script src="example.js" charset="UTF-8"></script>
```

Suppose `example.js` is a bundled version of something like this:

```js
import inspect from 'unist-util-inspect';
import fromDOM from 'hast-util-from-dom';

const hast = fromDOM(document.documentElement.parentNode);

console.log(inspect.noColor(hast));
```

Viewing `example.html` in a browser should yield the following in the console:

```text
root[2]
├─ doctype [name="html"]
└─ element[2] [tagName="html"]
   ├─ element[1] [tagName="head"]
   │  └─ element[1] [tagName="title"]
   │     └─ text: "Hello!"
   └─ element[1] [tagName="body"]
      └─ element[3] [tagName="h1"][properties={"id":"world"}]
         ├─ text: "World!"
         ├─ comment: "after"
         └─ element[0] [tagName="script"][properties={"src":"example.js","charSet":"UTF-8"}]
```

## API

### `fromDOM(node)`

Transform a DOM `Node` to a [HAST Node][node].

This works in a similar way to the `parse5` version except that it works directly from the DOM rather than a string of HTML. Consequently, it does not maintain location infomation.

## Contribute

See [`contributing.md` in `syntax-tree/hast`][contributing] for ways to get
started.

This organisation has a [Code of Conduct][coc].  By interacting with this
repository, organisation, or community you agree to abide by its terms.

## License

[ISC][license] © [Keith McKnight][author]

<!-- Definitions -->

[travis-badge]: https://img.shields.io/travis/syntax-tree/hast-util-from-dom.svg

[travis]: https://travis-ci.org/syntax-tree/hast-util-from-dom

[yarn]: https://yarnpkg.com/lang/en/docs/install

[npm]: https://docs.npmjs.com/cli/install

[license]: LICENSE

[author]: https://keith.mcknig.ht

[hast]: https://github.com/syntax-tree/hast

[hast-util-from-parse5]: https://github.com/syntax-tree/hast-util-from-parse5

[node]: https://github.com/syntax-tree/hast#ast

[vfile]: https://github.com/vfile/vfile

[contributing]: https://github.com/syntax-tree/hast/blob/master/contributing.md

[coc]: https://github.com/syntax-tree/hast/blob/master/code-of-conduct.md
