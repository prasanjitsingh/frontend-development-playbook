# Avoid Mixing Flag Condition Logic With App Logic

It can be difficult to quickly understand an `if` statement’s logic if it mixes feature flag condition checking with other condition logic. In this case prefer to make your code more verbose and nest the `if` logic for the short time that the feature flag will exist.

**Instead of:**

```js
if (variation('feature-cool-stuff') && (!foo || !bar)) {
  // do something amazing
}
```

**Consider:**

```js
if (variation('feature-cool-stuff') {
  if (!foo || !bar) {
    // do something amazing
  }
}
```

---

**Instead of:**

```js
{{#if (and (variation "feature-cool-stuff") (or (not foo) (not foo)))}}
  {{!-- do something amazing --}}
{{/if}}
```

**Consider:**

```js
{{#if (variation "feature-cool-stuff")}}
  {{#if (or (not foo) (not foo))}}
    {{!-- do something amazing --}}
  {{/if}}
{{/if}}
```



