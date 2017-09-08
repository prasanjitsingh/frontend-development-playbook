# Implementing a Flag

Now it’s time to use the feature flag in your code.

The first thing you should do is go and  read the [ember-launch-darkly README](https://github.com/kayako/ember-launch-darkly/blob/master/README.md) which is the Ember addon we use to provide the Launch Darkly functionality. In short, you'll likely be using the following helpers to check feature flags:

**Javascript**

```js
price: computed('price', function() {
  if (variation('feature-apply-discount')) {
    return this.get('price') * 0.8;
  }

  return this.get('price');
})
```

**Handlebars**

```js
{{#if (variation "feature-apply-discount")}}
  {{priceWithDiscount}}
{{else}}
  {{price}}
{{/if}}
```

Make sure you refer to the feature flagging best practices and patterns section of this book for ideas on some effective ways to implement a feature flag in your code. And by all means, if you come across another or a better pattern, please contribute it back to this book.

Also, make sure you remember to [create another PR to remove the feature flag](/feature-flags/when-to-remove-feature-flags.md) at this point as well.

