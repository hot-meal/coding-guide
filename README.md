# Simple CSS and HTML Guide

These guidelines are for writing flexible, consistent and maintainable HTML and CSS.

## HTML

### Syntax

*   Don't capitalise html tags
*   use a doctype.
*   Use double quotes on attributes.
*   Don’t use a closing slash for self-closing elements.
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

Use standards mode rendering for more consistent rendering across  browsers. Keep it lowercase.

```html
    <!doctype html>
``` 

### Language attribute

Use a lang attribute. This helps speech and language tools choose which rules to use.

```html
    <html lang="en">
```   

### IE compatibility mode

Only if you need support for IE10 and older. 

```html
    <!-- IE10 and below only -->
    <meta http-equiv="x-ua-compatible" content="ie=edge">
```

### Character encoding

Used to determine the correct rendering of characters. Allows you to use `—` instead of `&emdash;` for example.

UTF-8 is the recommended.

```html
    <head>
      <meta charset="utf-8">
    </head>
    <body>
      <p>Use an em dash like this — instead of an HTML entity.</p>
    </body>
```

### CSS and JavaScript includes

No need to specify `type` when you include CSS or JavaScript. `text/css` and `text/javascript` are taken as defaults.

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

Use semantic html, but be pragmatic. Prefer the option that gives the least amount of code with the fewest intricacies.

```html
    <!-- Good -->
    <button>...</button>
    
    <!-- Less good -->
    <div class="btn" onClick="...">...</div>
```

### Boolean attributes

A boolean attribute is one that does not need to have a declared value. XHTML did require a value, but HTML5 does not.

> The presence of a boolean attribute on an element represents true, and the absence of the attribute represents false.

Basically, **don’t add a value**.

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

Avoid unnecessary parent elements. 

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

Settings for your code editor to avoid inconsistencies and messy merges/diffs:

*   Use double-spaced soft-tabs.
*   Trim trailing white space on save.
*   Set encoding to UTF-8.
*   Add a new line to the end of files.


CSS
---

### Syntax

*  Each selector on its own line.
*   Add a space before the opening bracket of blocks.
*   Closing bracket of a block goes on a new line.
*   Include a space after `:`.
*   Each declaration on its own line.
*   End all declarations with a semi-colon. 
*   Don’t use a leading zero (`.5` instead of `0.5` and `-.5px` instead of `-0.5px`).
*   Lowercase all hex values, `#fff`. Lowercase is easier to read when scanning.
*   Use shorthand hex values, `#fff` instead of `#ffffff`.
*   Use quotes on attribute values, `input[type="text"]
*   Avoid using units for zero, `margin: 0;` instead of `margin: 0px;`.


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

Property declarations should be grouped together with the this order:

1.  Positioning
2.  Box model
3.  Typographic
4.  Visual
5.  Misc

Positioning first as it can remove an element from the document flow and override any box model related styles. 

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

Not every language flows left-ro-right like English, so the writing mode should be flexible. Using logical properties makes it easier to support these languages.

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

Use `rgba()` and `hsla()` instead for `rgb()` and `hsl()`.

```css
    .element {
      color: rgb(255 255 255 / .65);
      background-color: rgb(0 0 0 / .95);
    }
```    

### Avoid using `@import`s

`@import`s are slower than `<link>`s, they add additional page requests. Avoid them and instead use:

*   Multiple `<link>`elements
*   A preprocessor to compile all your CSS like [Sass](https://sass-lang.com/) or [Less](https://lesscss.org/) into a single file
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

Put your media queries close to their related rule sets. 

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

When a rule has **only one declaration**, remove any line breaks for better readability and editing. 

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

Limit shorthand declarations to those cases where you need to set all the available values. 

*   `padding`
*   `margin`
*   `font`
*   `background`
*   `border`
*   `border-radius`

Using shorthand properties can lead to more verbose code with unnecessary overrides and unpredictable side effects.

```css
    // Bad
    .element {
      margin: 0 0 10px;
      background: red;
      background: url("image.jpg");
      border-radius: 3px 3px 0 0;
    }
```

```css
    // Good 
    .element {
      margin-bottom: 10px;
      background-color: red;
      background-image: url("image.jpg");
      border-top-left-radius: 3px;
      border-top-right-radius: 3px;
    }
```    

### Nesting in preprocessors

Avoid nesting in preprocessors. Keep it simple.

```css
    // Without nesting clear
    .table > thead > tr > th { … }
    .table > thead > tr > td { … }
```
```css    
    // With nesting confusing
    .table > thead > tr {
      > th { … }
      > td { … }
    }
````    

### Using operators in preprocessors

Wrap all operations in parentheses.

```css
    // Bad 
    .element {
      margin: 10px 0 @variable*2 10px;
    }
```
```css
    // Good 
    .element {
      margin: 10px 0 (@variable * 2) 10px;
    }
```    

### Comments

Code is written for people. It should be descriptive, well commented, and accessible to others. 

Good comments convey context and purpose. 


```css
    // Bad
    // Modal header
    .modal-header {
      ...
    }
```

```css
    // Good
    // Wrapping element for .modal-title and .modal-close
    .modal-header {
      ...
    }
```    

### Class names

*   Use lowercase and dashes (not underscores or camelCase). Dashes provide natural divisions for readability (e.g., `.btn` and `.btn-danger`).
*   Avoid shorthand. `.btn` is useful for _button_, but `.s` doesn’t mean anything.
*   Use meaningful names; structural over presentational.
*   Prefix classes based on the closest parent or base.
*   Use `.js-*` classes to indicate behavior.

```css
    // Bad 
    .t { ... }
    .red { ... }
    .header { ... }
```

```css
    // Good
    .tweet { ... }
    .important { ... }
    .tweet-header { ... }
```    

### Selectors

*   Choose classes over element tags for more explicit and reliable styling that isn’t dependent on your markup.
*   Avoid using many selectors (e.g., `[class^="..."]`) on commonly occuring components. Browser performance is impacted.
*   Keep selectors short and limit the number of elements in each selector to three.
*   Scope classes to the closest parent `only` when necessary.

```css
    // Bad
    span { ... }
    .page-container #stream .stream-item .tweet .tweet-header .username { ... }
    .avatar { ... }
```

```css
    // Good
    .avatar { ... }
    .tweet-header .username { ... }
    .tweet .avatar { ... }
```    

### Child and descendant selectors

Use the child combinator `>` to limit the cascade of styles used with elements like `<table>`s that can be deeply nested. 

```css
    .custom-table > tbody > tr > td,
    .custom-table > tbody > tr > th {
      /* ... */
    }
```    

### Code Organization

*   Split your code by component.
*   When using multiple CSS files, split them by component instead of by page..

```css
    //
    // Component section heading
    //
    
    .element { ... }
  ```  
    
  ```css
    //
    // Component section heading
    //
    // Sometimes you need to include optional context for the entire component. Do that up here if it's important enough.
    //
    
    .element { ... }
    
    // Contextual sub-component or modifer
    .element-heading { ... }
```    
