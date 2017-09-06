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

```Handlebars
{{#if (variation "feature-apply-discount")}}
  {{priceWithDiscount}}
{{else}}
  {{price}}
{{/if}}
```



Next you should familiarise yourself with the feature flagging best practices and patterns section of this book.

