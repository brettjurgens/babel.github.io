---
layout: docs
title: Require Hook
description: How to use the require hook.
permalink: /docs/usage/require/
---

One of the ways you can use Babel is through the require hook. The require hook
will bind itself to node's `require` and automatically compile files on the
fly. This is equivalent to CoffeeScript's
[coffee-script/register](http://coffeescript.org/documentation/docs/register.html).

## Install

```sh
$ npm install babel-register
```

## Usage

```js
require("babel-register");
```

All subsequent files required by node with the extensions `.es6`, `.es`, `.jsx`
and `.js` will be transformed by Babel. The [polyfill](/docs/usage/polyfill) is also automatically required.

**NOTE:** By default all requires to `node_modules` will be ignored. You can
override this by passing an ignore regex via:

```js
require("babel-register")({
  // This will override `node_modules` ignoring - you can alternatively pass
  // an array of strings to be explicitly matched or a regex / glob
  ignore: false
});
```

## Specifying options

```javascript
require("babel-register")({
  // Optional ignore regex - if any filenames **do** match this regex then they
  // aren't compiled.
  ignore: /regex/,

  // Ignore can also be specified as a function.
  ignore: function(filename) {
    if (filename === '/path/to/es6-file.js') {
      return false;
    } else {
      return true;
    }
  },

  // Optional only regex - if any filenames **don't** match this regex then they
  // aren't compiled
  only: /my_es6_folder/,

  // Setting this will remove the currently hooked extensions of .es6, `.es`, `.jsx`
  // and .js so you'll have to add them back if you want them to be used again.
  extensions: [".es6", ".es", ".jsx", ".js"]
});
```

You can pass in all other [options](/docs/usage/options/#options) as well.

## Environment variables

By default `babel-node` and `babel-register` will save to a json cache in your
temporary directory.

This will heavily improve with the startup and compilation of your files. There
are however scenarios where you want to change this behaviour and there are
environment variables exposed to allow you to do this.

### BABEL_CACHE_PATH

Specify a different cache location.

```sh
$ BABEL_CACHE_PATH=/foo/my-cache.json babel-node script.js
```

### BABEL_DISABLE_CACHE

Disable the cache.

```sh
$ BABEL_DISABLE_CACHE=1 babel-node script.js
```
