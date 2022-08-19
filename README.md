# Code Standards Guide

Guidelines for writing flexible, consistent and maintainable HTML and CSS.

## HTML

### Syntax

*   Avoid capitalising html tags, including the doctype.
*   Use double quotes on attributes.
*   Don’t use a closing slash in self-closing elements.
*   Don’t skip any optional closing tags (e.g. `</li>` or `</body>`).
  
```html
    <!doctype html>
    <html>
      <head>
        <title>Page title</title>
      </head>
      <body>
        <img src="images/logo.png" alt="Company">
        <h1 class="hello-world">Hello, world!</h1>
      </body>
    </html>
``` 

### doctype

Use standards mode rendering for more reliably consistent rendering across every browser by using this doctype at the beginning of every HTML page. Keep it lowercase.

```html
    <!doctype html>
``` 

### Language attribute

Use a lang attribute on the root html element. This helps speech synthesis tools, for accessibility, to best choose which pronunciations to use, translation tools to choose which rules to use, and so forth.

```html
    <html lang="en">
```   

### IE compatibility mode

If you need support for IE10 and older. 

```html
    <!-- IE10 and below only -->
    <meta http-equiv="x-ua-compatible" content="ie=edge">
```

### Character encoding

Character encoding is used to determine the correct content rendering so that you can use regular characters instead of their HTML equivalent entities, like `—` instead of `&emdash;`. As long as their encoding matches that of the document. 

UTF-8 is the recommended encoding.

```html
    <head>
      <meta charset="utf-8">
    </head>
    <body>
      <p>Use an em dash like this — instead of an HTML entity.</p>
    </body>
```

### CSS and JavaScript includes

There is no need to specify a `type` when you include CSS and JavaScript since `text/css` and `text/javascript` are taken as their defaults.

```html
    <!-- Include CSS -->
    <link rel="stylesheet" href="main.css">
    
    <!-- Inline CSS -->
    <style>
      /* ... */
    </style>
    
    <!-- Include JavaScript -->
    <script src="main.js"></script>
 ```   

### Practicality over purity

Use semantic html, but not at the cost of pragmatism. Try to use the least amount of code with the fewest intricacies when possible.

```html
    <!-- Good -->
    <button>...</button>
    
    <!-- Less good -->
    <div class="btn" onClick="...">...</div>
```

### Boolean attributes

A boolean attribute is one that does not need to have declared value. XHTML did require a value, but HTML5 does not.

> The presence of a boolean attribute on an element represents true, and the absence of the attribute represents false.


In short, **don’t add a value**.

**Good**

```html
    <input type="text" disabled>
    
    <input type="checkbox" value="1" checked>
    
    <select>
      <option value="1" selected>1</option>
    </select>
```    


**Bad**

```html
    <input type="text" disabled="true">
    
    <input type="checkbox" value="1" checked="false">
    
    <select>
      <option value="1" selected="true">1</option>
    </select>
```    

### Minimise markup

When possible, avoid having unnecessary parent elements. 

```html
    <!-- Bad -->
    <span class="avatar">
      <img src="...">
    </span>
```


```html
    <!-- Good -->
    <img class="avatar" src="...">
```


### Editor preferences

Some good settings for your code editor, which help to avoid common code inconsistencies and difficult merges/diffs:

*   Use double-spaced soft-tabs.
*   Trim trailing white space on save.
*   Set encoding to UTF-8.
*   Add a new line to the end of files.


CSS
---

### Syntax

*   Keep individual selectors to a single line.
*   Include a space before the opening bracket of a blocks for easier legibility.
*   Place closing brackets of a blocks on a new line.
*   Include a space after `:` for each declaration.
*   Each declaration should appear on its own line.
*   End all declarations with a semi-colon. Including the last.
*   Use space separated values for colour properties (`color: rgb(0 0 0 / .5)`). 
*   Don’t use a leading zero (`.5` instead of `0.5` and `-.5px` instead of `-0.5px`).
*   Lowercase all hex values, `#fff`. Lowercase is easier to read when scanning.
*   Use shorthand hex values when possible, `#fff` instead of `#ffffff`.
*   Use quotes on attribute values in selectors, `input[type="text"]
*   Avoid using units for zero values, `margin: 0;` instead of `margin: 0px;`.


```css
    // Bad
    .selector, .selector-secondary, .selector[type=text] {
      padding:15px;
      margin:0px 0px 15px;
      background-color:rgba(0, 0, 0, 0.5);
      box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
    }
```

```css
    // Good
    .selector,
    .selector-secondary,
    .selector[type="text"] {
      padding: 15px;
      margin-bottom: 15px;
      background-color: rgb(0 0 0 / .5);
      box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
    }
```    

### Declaration order

Property declarations should be grouped together using the following order:

1.  Positioning
2.  Box model
3.  Typographic
4.  Visual
5.  Misc

Positioning is first as it can remove an element from the document flow and override any box model related styles. 

Whether it’s flex, float, grid, or table, then follows as it determines a component’s dimensions, placement, and alignment. 

Everything else occurs _inside_ the component or without affecting the previous two sections, so they come last.

```css
    .declaration-order {
      // Positioning
      position: absolute;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
      z-index: 100;
    
      // Box model
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      width: 100px;
      height: 100px;
    
      // Typography
      font: normal 14px "Helvetica Neue", sans-serif;
      line-height: 1.5;
      color: #333;
      text-align: center;
      text-decoration: underline;
    
      // Visual
      background-color: #f5f5f5;
      border: 1px solid #e5e5e5;
      border-radius: 3px;
    
      // Misc
      opacity: 1;
    }
 ```   

### Logical properties

Logical properties are the alternatives to directional and dimensonal properties which are based on more abstract terms like _block_ and _inline_. 

By default, block applies to the vertical direction (top and bottom) while inline refers to the horizontal direction (right and left). 

Not every language flows left-ro-right like English, so the writing mode should be flexible. Using logical properties makes it easier to support languages that can be written both horizontally or vertically (like Chinese, Japanese, and Korean). They’re also shorter and simpler to write.

```css
    // Without logical properties
    .element {
      margin-right: auto;
      margin-left: auto;
      border-top: 1px solid #eee;
      border-bottom: 1px solid #eee;
    }
```
    
```css
    // With logical properties
    .element {
      margin-inline: auto;
      border-block: 1px solid #eee;
    }
```    

### Colors

`rgba()` and `hsla()` are aliases for `rgb()` and `hsl()`, so you can modify alpha values in `rgb()` and `hsl()`. You can also now use a  space-separated syntax for color values.

```css
    .element {
      color: rgb(255 255 255 / .65);
      background-color: rgb(0 0 0 / .95);
    }
```    

### Avoid using `@import`s

For including CSS, `@import`s are slower than `<link>`s, they also add additional page requests. Avoid them and instead go for an alternate approach:

*   Use multiple `<link>`elements
*   Use a preprocessor to compile all your CSS like [Sass](https://sass-lang.com/) or [Less](https://lesscss.org/) into a single file
*   Concatenate your CSS files with features provided in various tooling libraries.

```css
    <!-- Use link elements -->
    <link rel="stylesheet" href="core.css">
```

```css
    <!-- Avoid @imports -->
    <style>
      @import url("more.css");
    </style>
```    

### Media queries

Put your media queries as close to their related rule sets as possible. 

Don’t include them together in a separate stylesheet or at the end of the file. Doing this makes it easier for people to miss them in the future. Here’s a better solution.

```css
    .element { ... }
    .element-avatar { ... }
    .element-selected { ... }
    
    @media (min-width: 480px) {
      .element { ... }
      .element-avatar { ... }
      .element-selected { ... }
    }
```    

### Using Single rule declarations

When a rule set has **only one declaration**, you should remove any line breaks for better readability and easier editing. 

```css
    // Single declarations on one line
    .span1 { width: 60px; }
    .span2 { width: 140px; }
    .span3 { width: 220px; }
```

```css
    // Multiple declarations, one per line
    .sprite {
      display: inline-block;
      width: 16px;
      height: 15px;
      background-image: url("../img/sprite.png");
    }
    .icon           { background-position: 0 0; }
    .icon-home      { background-position: 0 -20px; }
    .icon-account   { background-position: 0 -40px; }
```    

### Shorthand notations

It is best to limit shorthand declarations to those instances where you need to explicitly set all the available values. Some commonly overused shorthand properties include:

*   `padding`
*   `margin`
*   `font`
*   `background`
*   `border`
*   `border-radius`

When we don’t need to set all the values of a shorthand property represents. For example, HTML headings only set top and bottom margin, so when necessary, only override those two values. A `0` value implies an override of either a browser default or previously specified value.

Excessive use of shorthand properties leads to sloppier code with unnecessary overrides and unintended side effects.

The Mozilla Developer Network has a great article on [shorthand properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties) for those unfamiliar with notation and behavior.

    // Bad example
    .element {
      margin: 0 0 10px;
      background: red;
      background: url("image.jpg");
      border-radius: 3px 3px 0 0;
    }
    
    // Good example
    .element {
      margin-bottom: 10px;
      background-color: red;
      background-image: url("image.jpg");
      border-top-left-radius: 3px;
      border-top-right-radius: 3px;
    }
    

### Nesting in preprocessors

Avoid unnecessary nesting in preprocessors whenever possible—keep it simple and avoid reverse nesting. Consider nesting only if you must scope styles to a parent and if there are multiple elements to be nested.

**Additional reading:**

*   [Nesting in Sass and Less](https://markdotto.com/2015/07/20/css-nesting/)

    // Without nesting
    .table > thead > tr > th { … }
    .table > thead > tr > td { … }
    
    // With nesting
    .table > thead > tr {
      > th { … }
      > td { … }
    }
    

### Operators in preprocessors

For improved readability, wrap all math operations in parentheses with a single space between values, variables, and operators.

    // Bad example
    .element {
      margin: 10px 0 @variable*2 10px;
    }
    
    // Good example
    .element {
      margin: 10px 0 (@variable * 2) 10px;
    }
    

### Comments

Code is written and maintained by people. Ensure your code is descriptive, well commented, and approachable by others. Great code comments convey context or purpose. Do not simply reiterate a component or class name. Use the `//` syntax when writing CSS with preprocessors. When shipping CSS to production, remove all comments.

Be sure to write in complete sentences for larger comments and succinct phrases for general notes.

    // Bad example
    // Modal header
    .modal-header {
      ...
    }
    
    // Good example
    // Wrapping element for .modal-title and .modal-close
    .modal-header {
      ...
    }
    

### Class names

*   Keep classes lowercase and use dashes (not underscores or camelCase). Dashes serve as natural breaks in related class (e.g., `.btn` and `.btn-danger`).
*   Avoid excessive and arbitrary shorthand notation. `.btn` is useful for _button_, but `.s` doesn’t mean anything.
*   Keep classes as short and succinct as possible.
*   Use meaningful names; use structural or purposeful names over presentational.
*   Prefix classes based on the closest parent or base class.
*   Use `.js-*` classes to denote behavior (as opposed to style), but keep these classes out of your CSS.

It’s also useful to apply many of these same rules when creating custom properties and preprocessor variable names.

    // Bad example
    .t { ... }
    .red { ... }
    .header { ... }
    
    // Good example
    .tweet { ... }
    .important { ... }
    .tweet-header { ... }
    

### Selectors

*   Use classes over generic element tags for more explicit and reliable styling that isn’t dependent on your markup.
*   Avoid using several attribute selectors (e.g., `[class^="..."]`) on commonly occuring components. Browser performance is known to be impacted by these.
*   Keep selectors short and strive to limit the number of elements in each selector to three.
*   Scope classes to the closest parent `only` when necessary (e.g., when not using prefixed classes).

**Additional reading:**

*   [Scope CSS classes with prefixes](https://markdotto.com/2012/02/16/scope-css-classes-with-prefixes/)
*   [Stop the cascade](https://markdotto.com/2012/03/02/stop-the-cascade/)

    // Bad example
    span { ... }
    .page-container #stream .stream-item .tweet .tweet-header .username { ... }
    .avatar { ... }
    
    // Good example
    .avatar { ... }
    .tweet-header .username { ... }
    .tweet .avatar { ... }
    

### Child and descendant selectors

When necessary, it may be helpful to use [the child combinator (`>`)](https://developer.mozilla.org/en-US/docs/Web/CSS/Child_combinator) to limit the cascade of some styles in elements like `<table>`s that are often recursively nested. Use it to limit styles to the immediate children elements of a parent element to avoid unnecessary overrides later on.

    .custom-table > tbody > tr > td,
    .custom-table > tbody > tr > th {
      /* ... */
    }
    

### Organization

*   Organize sections of code by component.
*   Develop a consistent commenting hierarchy.
*   Use consistent white space to your advantage when separating sections of code for scanning larger documents.
*   When using multiple CSS files, break them down by component instead of page. Pages can be rearranged and components moved.

    //
    // Component section heading
    //
    
    .element { ... }
    
    
    //
    // Component section heading
    //
    // Sometimes you need to include optional context for the entire component. Do that up here if it's important enough.
    //
    
    .element { ... }
    
    // Contextual sub-component or modifer
    .element-heading { ... }
    

Open sourced by [@mdo](https://twitter.com/mdo) under MIT license. Copyright 2022.

*   
*   

*   [Follow @mdo](https://twitter.com/mdo)
*   [Tweet](https://twitter.com/share)