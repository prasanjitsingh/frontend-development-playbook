# CSS Style Guidelines

## Use css-modules values over Sass variables

### Rationale

It's not always obvious where a Sass variable is defined, whether it's been overridden somewhere etc…

By using css-modules @values instead it's immediately obvious when reading the CSS where a value has come from.

### Recommended Style :thumbsup:

```css
/* app/styles/colors.css */
@value primary-color: #8af;
@value secondary-color: #fc0;
```

```css
/* app/components/x-foo/styles.css */
@value primary-color, secondary-color from 'frontend-cp/styles/colors';

.foo {
  color: primary-color;
  background-color: secondary-color;
}
```

### Deprecated Styles :thumbsdown:

```scss
// app/styles/settings/_colors.scss
$primary-color: #8af;
$secondary-color: #fc0;
```

```scss
// app/components/x-foo/styles.css
.foo {
  color: $primary-color;
  background-color: $secondary-color;
}
```

## Use local-class="xxx" vs class="{{styles.xxx}}"

Accessing the `styles` property in templates has been deprecated in ember-css-modules, and `local-class` should be used instead.

Static classes should still use `class="xxx"`.

### Recommended Style :thumbsup:

```hbs
<div local-class="foo"></div>

<div local-class="foo" class="bar"></div>

<div local-class="{{if foo 'foo' 'bar'}} baz"></div>
```

### Deprecated Styles :thumbsdown:

```hbs
<div class="{{styles.foo}}"></div>

<div class="{{styles.foo}} bar"></div>

<div class="{{join-classes (if foo styles.foo styles.bar) styles.baz}}"></div>
```
