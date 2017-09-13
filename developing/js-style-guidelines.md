# JS Style Guidelines

## Importing Ember Modules

Import using [`ember-cli-shims`](https://github.com/ember-cli/ember-cli-shims/blob/master/vendor/ember-cli-shims/app-shims.js).

### Rationale

The Ember community is marching towards a [well-designed and consistent module
pattern](https://github.com/emberjs/rfcs/blob/master/text/0176-javascript-module-api.md).
Currently, the bridge to that future is `ember-cli-shims`. Once the new module
style is ready to adopt, we can use automated tools to migrate to it from
`ember-cli-shims`.

Originally, all Ember’s modules were made available as properties on the `Ember`
global. Eventually, this global will disappear altogether and the only way to
access module will be with imports.

This keeps us aligned with the platform and ready for the day when the `Ember`
global disappears.

### Recommended Style :thumbsup:

```js
import Component from 'ember-component';
import { assert } from 'ember-metal/utils';
import run, { next, later } from 'ember-runloop';
import on from 'ember-evented/on';

export default Component.extends({
});
```

### Deprecated Styles :thumbsdown:

```js
import Ember from 'ember';

export default Ember.Component.extend({
});
```

```js
import Ember from 'ember';
const { Component, run } = Ember;

export default Component.extend({
});
```

## Declaring Variables

For variables at the module level, **always** use `const`.

For variables in function bodies, use `let` or `const` according to which best suits your needs and preferences.

Never use `var`.

### Rationale

For a great overview of the advantages of `let` and `const` over `var`, please read [“Let It Be - How to declare JavaScript variables” by Matthew Beale](http://madhatted.com/2016/1/25/let-it-be).

We agree with Matthew that `let` and `const` are preferable to `var` but we’re not quite so strict regarding when to use `let` and when to use `const`. The
rule of thumb is: whichever you think better expresses your intent in a function body. We’d rather not re-litigate this issue over and over again and instead
become comfortable with each others’ preferences.

### Recommended Style :thumbsup:

```js
const GRAVITY = 9.8;

function update() {
  const x = 1;
  let y = 0;

  if (somePredicate) {
    y = -1;
  }
}

// equally acceptable...

function update() {
  let x = 1;
  let y = 0;

  if (somePredicate) {
    y = -1;
  }
}
```

### Deprecated Styles :thumbsdown:

```js
var GRAVITY = 9.8;

function update() {
  var x = 1;
  var y = 0;

  if (somePredicate) {
    y = -1;
  }
}
```

## Avoid creating new Promises

You should rarely need to create promises explicitly and manually call `resolve` and `reject`.
Most of the time you'll be calling something which already returns a promise and so should use that instead of wrapping another layer on top.

One common example is wrapping jQuery ajax requests, we have [ember-ajax](https://github.com/ember-cli/ember-ajax) which handles this, so is
a better solution than manually wrapping.

Any methods called on the `store` will return promises, so don't need to be wrapped.

If there's code which may error before calling the first promise returning function, then you can wrap this in `RSVP.resolve` without needing to create a
`new Promise`.

### Recommended Style :thumbsup:

```js
return this.get('store').findAll('blah');

return this.get('ajax').request({ url });

return RSVP.resolve(() => {
  // something which may explode
}).then(() => {
  return this.get('store').findAll('blah')
})
```

### Deprecated Styles :thumbsdown:

```js
return new Promise((resolve, reject) => {
  this.get('store').findAll('blah')
    .then(resolve)
    .catch(reject);
});

return new Promise((resolve, reject) => {
  jQuery.ajax({
    url,
    success(data) {
      resolve(data);
    },
    error() {
      reject();
    }
  });
});

return new Promise((resolve, reject) => {
  try {
    // something which may explode
    resolve()
  } catch(e) {
    reject();
  }
}).then(() => {
  return this.get('store').findAll('blah')
})
```
