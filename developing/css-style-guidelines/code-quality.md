# Writing readable and predictable CSS
*This guide is specifically for the  **modular CSS architecture***

## Naming CSS classes

#### What should I name the class?
Since we are going with **modular CSS**, do not confuse with the naming conventions of **functional CSS**.
This means the class name should tell about **what the element is**, not about the **function it performs**.

_Example:_ Suppose you want to center align your page title, the class name should be `.page-title` rather than, say, `.align-center`.

&nbsp;
#### Do I need to follow [BEM naming methodology](https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)?
No.
Since your CSS has the local scope you don't have to worry prefixing the block names.

In situations where you have quite a lot elements in your component or you find it difficult to name classes for each element, this might be an indication that you should consider breaking your component up into small ones, rather than following BEM.

&nbsp;
#### Make use of modifier classes
Make your code more predictable both in HTML & CSS files with modifier classes.
Another benefit is that you can always group it with it's main class.

_Example:_ `.is-` and `.has-` are commonly used modifiers in CSS.

:thumbsup:
```scss
.item {
  padding: 14px;
  background-color: #40364D;

  &.is-active {
    background-color: #2b2434;
  }
}
```
&nbsp;
#### Avoid using attribute selectors, instead assign class to every key selector
Do not (or try not to) nest attribute selectors within classes. These selectors do not really describe what the element is used for. Also, nesting makes your CSS code less readable.

_Example:_

:thumbsdown:
```hbs
<div local-class="timestamp">
  <time>09: 00</time> AM
</div>
```
```scss
.timestamp {
  font-size: 16px;

  time {
    font-size: 18px;
  }
}
```

:thumbsup:
```hbs
<div local-class="timestamp">
  <time local-class="time-value">09: 00</time> AM
</div>
```
```scss
.timestamp {
  font-size: 16px;
}

.time-value {
  font-size: 18px;
}
```

Apart from this, nesting also affects the performance of selectors.
<details>
  <summary>Read more about selector performance</summary>
  <br>
  There are couple of reasons for avoiding attribute selectors:
  <br>
  1) They are less performant than the class selectors.
  <br>
  2) Browsers read CSS selectors from right to left direction. Taking an example of a menu item <code>.menu li a</code>:
  <br>
  Here browser will read <code>a</code> as the first selector then check if it lives inside <code>li</code>, finally check if they both live  inside <code>.menu</code>. This does not affect when there are a few elements on the page but considering too many elements in a complex design, you should definitely avoid this.
</details>

&nbsp;

#### Do not prefix component name
Doing this is absolutely unnecessary since Ember is already doing it for you.

_Example:_
<br>
:thumbsdown:
```scss
.onboarding-heading {
  ...
}

.onboarding-sub-heading {
  ...
}
```
which compiles to `.onboarding-component__onboarding-heading` & `.onboarding-component__onboarding-sub-heading`. It could be even worse if it had a parent component.

<br>

:thumbsup:
```scss
.heading {
  ...
}

.sub-heading {
  ...
}
```

&nbsp;

#### How would I know whether I've named the classes correctly or not?
Nothing fancy here, just a simple trick:

Once you're done, quickly self-review your CSS code, if you're able to understand roles of all the classes only by reading your CSS then 👍.

<br>

---

<br>
## Improving readability

#### Do not nest the classes unless really needed
Use proper **parent-child** relationships. Avoid unnecessary specificity which is also against the CSS selector performance as mentioned above.

_Example:_

<br>
:thumbsdown:
```scss
.box {
  ...

  .title {
    ...
  }
}
```

:thumbsup:
```scss
.box {
  ...
}

.box-title {
  ...
}
```
<br>

#### Group pseudo and modifier classes
Keep pseudo (`:hover`, `:focus`, etc) and modifier (`.is-`, `.has-`) classes within the element's class to easily identify to which class they belong to.
_Example:_

:thumbsdown:
```scss
.dropdown {
  color: #fff;
}

.dropdown:hover {
  color: #eee;
}

.dropdown.is-open {
  color: #ddd;
}

.navigation {
  ...
```

:thumbsup:
```scss
.dropdown {
  color: #fff;

  &:hover {
    color: #eee;
  }

  &.is-open {
    color: #ddd;
  }
}

.navigation {
  ...
```

<br>

#### Use reverse `&` where the style is dependent on a parent element's class
_Example:_ Continuing with the above dropdown example, suppose the trigger element's style is dependent on it's container element:

:thumbsdown:
```scss
.dropdown-trigger {
  display: block;
}

.is-collapsed .dropdown-trigger {
  display: none;
}
```

:thumbsup:
```scss
.dropdown-trigger {
  display: block;

  .is-collapsed & {
    display: none;
  }
}
```

<br>

#### It's a good practice to write the properties in order
If you aren't already writing respecting the order, you're gonna feel it a bit difficult to follow in the beginning but believe me you will love it once you get used to it.
Instead of sorting properties in alphabetical order, which actually isn't very helpful, consider grouping properties by **type**.

Here's how you order the properties:

```scss
.selector {

  /* Imported style */
  @extend %another-style;

  /* CSS content */
  content: '';

  /* Position */
  position: absolute;
  z-index: 10;
  top: 0;
  right: 0;

  /* Display & box model */
  display: inline-block;
  overflow: hidden;
  width: 100px;
  height: 100px;
  padding: 10px;
  margin: 10px;
  border: 10px solid #333;

  /* Color */
  background: #000;
  color: #fff;

  /* Text */
  font-family: sans-serif;
  font-size: 16px;
  line-height: 1.4;
  text-align: right;

  /* Other */
  cursor: pointer;

  /* Transition & animation */
  transition: color 0.15s;
  animation: slide 0.2s forwards;
}
```

_Example:_

:thumbsdown:
```scss
.box {
  background-color: #fff;
  width: 200px;
  position: relative;
  height: 300px;
}
```

:thumbsup:
```scss
.box {
  position: relative;
  width: 200px;
  height: 300px;
  background-color: #fff;
}
```

<br>

#### Use `:not()` instead of overriding property values
This one is quite obvious but I've seen in many codebases, developers forget to use it. So it might be worth mentioning here.

_Example:_

:thumbsdown:
```scss
.item {
  border: 1px solid #eee;

  &:last-child {
    border: 0;
  }
}
```

:thumbsup:
```scss
.item:not(:last-child) {
  border: 1px solid #eee;
}
```

<br>

#### If you're going against the best practices
If you end up writing such code like negative margins, `!important`, etc. and it seems the only best possible solution, **do not forget to add a comment describing your problem**.

<br>

#### Abstraction in modular CSS?
No. Keep your CSS within the same component. If you think that you're repeating the same code in several components, create mixins instead.

<br>

---

<br>
## Avoiding mistakes

#### Avoid using shorthands
Yes, CSS shorthands are considered as anti-patterns unless you're changing all the values of a property.

How we misuse shorthands:

```scss
.card {
  background: #fff;
}
```

What we are actually telling the browser to do:
```scss
.card {
  background-image: initial;
  background-position-x: initial;
  background-position-y: initial;
  background-size: initial;
  background-repeat-x: initial;
  background-repeat-y: initial;
  background-attachment: initial;
  background-origin: initial;
  background-clip: initial;
  background-color: #fff;
}
```

What we really meant:
```scss
.card {
  background-color: #fff;
}
```
<details>
<br>
<summary>Brief on problems with shorthands</summary>

Suppose you want to override font properties for an element:
<pre><code>
body {
  font-family: 'Source Sans Pro';
  font-size: 18px;
  line-height: 1.8;
}


.box {
  font: 30px 'Fira Code';
}
</code></pre>

and unknowingly, <code>line-height</code> is also set to <code>initial</code>.
</details>

<br>

#### Avoid `margin-top`, use `margin-bottom`
Unlike horizontal margins, vertical margins do collapse. To avoid this, it's a good idea to always keep the margins one direction. Choosing the one with the most use cases, good to go with `margin-bottom`.

<br>

---

<br>
#### Terms used:
* **Attribute selector** - HTML element selectors such as `div`, `span`, `p`, etc.
* **Key selector** - Last child in nested selectors group. e.g. `nav li a`, here `a` is the key selector
* **Parent-child relationship in CSS classes** - It refers to prefixing parent class name to it's children to make the child class names more relevant. e.g. Say `.box-title`, `.box-image`, where `.box` is a parent.
