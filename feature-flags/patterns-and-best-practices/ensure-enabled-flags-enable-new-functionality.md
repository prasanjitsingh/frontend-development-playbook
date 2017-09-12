# Ensure Enabled Flags Enable New Functionality

Ensure that when a feature flag is enabled is turns on the new functionality and when it’s disabled it restores the existing functionality. This can save from hard to grok code logic \(double negatives\) and also means that if our code defaults flags to `false` due to some error, then we end up with the application in it’s default state - without the new features.

**Instead of:**

```js
price: computed(function() {
  if(variation('release-no-discount')) {
    return oldPrice;
  }

  return newPrice;
})
```

**Consider:**

```js
price: computed(function() {
  if(variation('release-apply-discount')) {
    return newPrice;
  }

  return oldPrice
})
```



