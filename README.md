## SmartRecruiters  

![SmartRecruiters](https://fbcdn-profile-a.akamaihd.net/hprofile-ak-frc3/t1.0-1/p160x160/393735_10151047695605780_1051448429_n.png)

# HTML/CSS Code Style Guide

>Code Style Guide bridges the gap between framework and developer

The following document contains ruleset of writing both HTML and CSS code in SmartRecruiters. It's based on best practices and strongly relies on idiomatic CSS and HTML principles published by Nicholas Gallagher. 

<br />
> Programs are meant to be read by humans <br />
and only incidentally for computers to execute.  
**Harold Abelson and Gerald Jay Sussman**  
*Structure and Interpretation of Computer Programs, 1984*

## Table of content

- [Common principles](#common-principles)
- [CSS principles](#css-principles)
- [HTML principles](#html-principles)

## Common principles

### Best practices

#### Semantics

Don't try to name classes to get more semantic code. Semantics is about elements only. Attributes should be sensible for other developers, not machines

#### Keep your selectors short

To avoid problems with performance, maintanence and entanglement in general, do not use nested selectors.
What is more, it helps to avoid location dependency. 

#### The Single Responsibility Principle

Use OOCSS and prefixed classes for differend layers and behaviours in your code.

### Progressive enhancement
Use Modernizr for feature detection 

### Grid

Width of block elements should depend on grid or parent element's width only. Never use width rule for block elements alone in your styles.


### BEM Naming Convention

We use BEM methodology as a core of our naming convention to help us keep the whole frontend architecture consistent, strict, and easy to read and maintain.

However, we found much more efficient and easier to name BEM items as follow:

* **Block**: `.foo`

* **Element**: `.foo-bar`

* **Modifier**: `.foo--baz`

Use lower CamelCase if you need to write a class with multiple words.


```css
/* Good */
.fooBar
.fooBar-baz
.fooBar--qux
```

```css
/* Bad */
.foo-bar
.foo-bar-baz
.foo-bar--qux

.foo_bar
.foo_bar-baz
.foo_bar--qux
```

To avoid long, hard to read and maintain names of classes, keep only root block name in elements.

```html
<!-- Good -->
<div class="rating">
	<div class="rating-hedaer">
		<h3 class="rating-title"></h3>
	</div>
</div>
```

```html
<!-- Bad -->
<div class="rating">
	<div class="rating-header">
		<h3 class="rating-header-title"></h3>
	</div>
</div>
```



## CSS principles


### Format
* Use four spaces for indentaction

**Idiomatic rules**

* Use one discrete selector per line in multi-selector rulesets.
* Include a single space before the opening brace of a ruleset.
* Include one declaration per line in a declaration block.
* Use one level of indentation for each declaration.
* Include a single space after the colon of a declaration.
* Use lowercase and shorthand hex values, e.g., #aaa.
* Use single or double quotes consistently. Preference is for double quotes, e.g., content: "".
* Quote attribute values in selectors, e.g., input[type="checkbox"].
* Where allowed, avoid specifying units for zero-values, e.g., margin: 0.
* Include a space after each comma in comma-separated property or function values.
* Include a semi-colon at the end of the last declaration in a declaration block.
* Place the closing brace of a ruleset in the same column as the first character of the ruleset.
* Separate each ruleset by a blank line.

Use EditorConfig plugin for your IDE to make sure you are using correct code formating settings.

**EditorConfig website:**

[Link](http://editorconfig.org/ "Title")

**EditorConfig settings:**

```
# editorconfig.org
root = true

# Common rules
[*]
indent_size = 4
indent_style = space
end_of_line = lf
charset = utf-8
tab_width = 4
trim_trailing_whitespace = true
insert_final_newline = true

# Matches the exact files either package.json or .travis.yml
[{package.json,.travis.yml}]
indent_style = space
indent_size = 2
```

### Comments

#### Primary comment style

```css
/* ----------------------------------------------------------------
    COMPONENT - Button
    
    @date
    @author
 * ---------------------------------------------------------------- */ 
```

#### Secondary comment style

```css
/* --------------------------
   COMPONTENT Dependencies
* --------------------------- */ 
```

#### Inline LESS comment style

```less
// Comment
```

### Vendor Prefixes

Avoid using vendor prefixes directly in selector rules. It will be added automatically during build process.

### Box model

Keep in mind there is border-box layout model applied to all elements.

### Units

* Use **_rems_** where possible. Do not write any fallbacks in pixels in your styles directly. It will be added automatically during build process.  
To simplify calculations, use _font-size: 62.5%_ on the root element (html, not body) what makes 1rem equal to 10px.

* Do not use unit with 0 values

```css
/* Good */
padding: 0 10%;
```

```css
/* Bad */
padding: 0% 10%;
padding: 0px 10%;
```

* Do not use unit with line-height

```css
/* Good */
line-height: 1.5;
```

```css
/* Bad */
line-height: 1.5rem;
line-height: 150%;
```

### Styling ID's

It's allowed to style IDs in edge cases, but only as a key selector.

```css
/* Good */
#foo {

}
```

```css
/* Bad */
#foo .bar {

}

#foo a {

}
```

#### Exception


#### Overrides

To avoid problems with overriding helper classes, make their specificity higher by including `#root` id added on **body** element.



## HTML principles

### Format

**Idiomatic rules:**

* Always use lowercase tag and attribute names.
* Write one discrete, block-level element per line.
* Use one additional level of indentation for each nested block-level element.
* Use valueless boolean attributes (e.g. checked rather than checked="checked").
* Always use double quotes to quote attribute values.
* Omit the type attributes from link stylesheet, style and script elements.
* Always include closing tags.


### Doctype

The only valid doctype is HTML5 Document Type Definition.

```html
<!doctype html>
```

### Targeting IE browsers

Do not serve different stylesheets for different browsers
To target older IE, use conditional comments and specific classes as listed below.

```html
<!--[if lt IE 9]>  <html class="no-js oldie"> <![endif]-->
<!--[if IE 9 ]>    <html class="no-js ie9"> <![endif]-->
<!--[if (gt IE 9)|!(IE)]><!--> <html class="no-js"> <!--<![endif]-->
```

### HTML classes prefixes

#### JavaScript

Use `js-` prefix for JavaScript hooks.
Do not ever style js- classes in your stylesheet.

#### Smart Testing Framework

Use `st-` prefix in IDs used for Smart Testing Framework hooks

### Accessibility

Remember to use at least these landmark roles in your code:

* banner,
* complementary,
* contentinfo,
* main,
* navigation,
* search

Consider adding skipping links between long blocks of content

### JavaScript hooks

Use button element rather than a link with `href="#"` as a hook for JavaScript interactions.


## Examples 

### Page layout structure

```html
<div class="site site--home">
    <header class="site-hedaer" role="banner">
        <nav class="nav" role="navigation">
            <ul class="nav-list"></ul>
        </nav>
    </header>
    <div class="site-container">
        <section class="main" role="main">
        </section>
    </div>
    <footer class="site-footer" role="contentinfo">
    </footer>
</div>
```



