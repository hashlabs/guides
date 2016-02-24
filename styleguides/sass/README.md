# Sass

One of the simplest goals of this style guide is setting your documents to be consistent. This is a set of rules regarding syntax and formatting. Having a standard way of writing SCSS means that code will always look, feel and behave familiar to all members of the team.

## General

At a very high-level, we want:

* Two (2) space indents.
* Always use Tab instead spacebar.
* Multi-line CSS. Avoid single line rules.
* Meaningful use of whitespace.

Your selectors are fundamental to writing good CSS. To very briefly sum it up our intentions:

* Select what you want explicitly, rather than relying on circumstance or coincidence.
* __Write selectors for reusability__, so that you can work more efficiently and reduce waste and repetition.
* __Do not nest selectors unnecessarily__, because this will increase specificity and affect where else you can use your styles.
* __Do not qualify selectors unnecessarily__, as this will impact the number of different elements you can apply styles to.
* __Keep selectors as short as possible__, in order to keep specificity down and performance up.

Focussing on these points will keep your selectors a lot more sane and easy to work with on changing and long-running projects.

### BEM naming (sort of)

BEM, meaning Block, Element, Modifier, is a front-end methodology coined by developers working at Yandex. Whilst BEM is a complete methodology, here we are only concerned with its naming convention. Further, the naming convention here only is BEM-like; the principles are exactly the same, but the actual syntax differs slightly.

BEM splits components classes into three groups:

* Block: The sole root of the component.
* Element: A component part of the Block.
* Modifier: A variant or extension of the Block.

To take an analogy (note, not an example):

```
.capybara {}
.capybara-head {}
.capybara--tall {}
```

Elements are delimited with two (1) hyphen `(-)`, and Modifiers are delimited by two (2) hyphens `(--)`.

Here we can see that `.capybara {}` is the Block; it is the sole root of a discrete entity. `.capybara-head {}` is an Element; it is a smaller part of the `.capybara {}` Block. Finally, `.capybara--tall {}` is a Modifier; it is a specific variant of the `.capybara {}` Block.

### Starting Context

Your Block context starts at the most logical, self-contained, discrete location. To continue with our person-based analogy, we'd not have a class like `.room-person {}`, as the room is another, much higher context. We'd probably have separate Blocks, like so:

```
.room {
  &-door {}
  &--girly {}
}

.capybara {
  &-head {}
}
```

If we did want to denote a `.capybara {}` inside a `.room {}`, it is more correct to use a selector like `.room .capybara {}` which bridges two Blocks than it is to increase the scope of existing Blocks and Elements.

A more realistic example of properly scoped blocks might look something like this, where each chunk of code represents its own Block:

```
.page {}
.content {}
.sub-content {}
.footer {
  &-copyright {}
}
```

## Files

One of the structures for us to develop, is the use of  small snippets of code that we embed in our `main.scss` file for compiling.

The naming convention for files name is:

```
_<type>--<subject>.scss
```

For instance a typically object file name is going to look like:

```
_objects--buttons.scss
```

Note the use of plural names in order to represent the types, besides, the subject is in plural since the type is `objects` otherwise will be singular like:

```
_layouts--dashboard.scss
```

The structure we follow to group files is:

* __Settings__: it includes all the files that set variables that are going to be used on several files of the project
* __Tools__: it includes files that make easier the development of the project such as `_tools--mixins.scss`, `_tools--functions.scss`, `_tools--z-map.scss` and any other that can be added for any particular project needs.
* __Objects__: are any individual and isolates representations of coherent elements that can be used on any context within the project. for instance: `_objects--buttons.scss`
* __Components__: are composites of several objects that generate a more complex element such as: `_components--searcher.scss` which typically may be a compound of a button and an input. Together they become something new and individually they may be transformed too.
* __Layouts__: are a set of rules that define the appearance of any generic pages, in nuts, is like set the baseline format for pages that are similar, for instance blog posts, data listings or any page that even when has different content keeps similar structure.
* __Partials__: unlike layouts partials represents specific appearance for some pages, for instance in a blog website we can have a custom-thing page which in many aspects is different to other pages.

Keep in mind that Layouts and Partials can be used to apply some context to objects, while the object file has styles specific for just the object core, in the other hand, layouts or partials has some specific styles to be applied over the object core  in order to meet the design needs.

Finally, is important to mention that we conserve the same order like the one listed above to create the `main.scss` file. In addition, a typically main file will look like:

```
/**
 * Settings
 */

@import 'settings--palette.scss';
@import 'settings--bootstrap.scss';
@import 'bootstrap';
@import 'settings--defaults.scss';

/**
 * Tools
 */

@import 'tools--<subject>.scss';

/**
 * Objects
 */

@import 'objects--<subject>.scss';

/**
 * Components
 */

@import 'components--<subject>.scss';


/**
 * Layouts
 */

@import 'layouts--<subject>.scss';

/**
 * Partials
 */

@import 'partials--<subject>.scss';
```

## Working with Bootstrap

We use [Bootstrap](http://getbootstrap.com/) as our CSS Framework, in order to make the most of it all variables that need to be changed to satisfied the project needs are going to be listed as show below in a file called `_settings--bootstrap.scss`: (All this in order to do not overwrite rules as a first alternative to achieve the expected results)

```
/*!
 * Bootstrap v3.3.5 (http://getbootstrap.com)
 * Add into this file the variables that are going
 * to be used by Bootstrap to delivery its grid and
 * overall styles. A complete list of variables
 * can be found at: (http://getbootstrap.com/customize/#less-variables)
 */

// Colors
...

// Scaffolding
...

// Grid system
...

// Components
...

// Buttons
...

...

```

## Z-MAP

This file contain a SASS function to declare the way we will be doing the z-index styles for major components. The way it works, is creating an array of elements with usual names and giving the position of that element inside the array, that's the correspondant z-index. A basic implementation of this will look like:

```
$z-layers: (
  'initial': 0,
  'menu': 500,
  'overlay': 1000,
);

@function z($layer) {
  @if not map-has-key($z-layers, $layer) {
    @warn 'No layer found for `#{$layer}` in $z-layers map. Property omitted.';
  }
  @return map-get($z-layers, $layer);
}
```

## Variables

Variables should be declared on a file basis, only leave globals for colors and settings that are really global.

### Variable Naming

Variable naming convention goes like this:

`${type}--{element}-{attribute}:`

### Types

`types` can be one of the following:

1. size
2. color
3. font
4. animation
5. transition

Feel free do add a new type, as long is necessary

### Element

This is the part of the component the variable applies, for example `header`, `hero`, `navigation` etc

### Attribute

This is the attribute the variable applies, for example `background`, `height`, `width` etc

### Variable Definition

Variables should be the first section of a file. Like the following example

```
$color--foo-background:       $blueshell;
$color--foo-font:             $blueshell;
$<variable>:                  <value>;

.foo {
  background-color: $color--foo-background;
}
```

> Keep in mind how the variables declaration is aligned, we encourage to keep that format (it doesn't need to be an specific space but all the values should be aligned).
