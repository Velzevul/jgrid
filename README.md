# jGrid

jGrid is the css grid framework that takes advantage of `text-align: justify;` css property on inline elements.

What's the difference between jGrid and http://justifygrid.com/ ? First of all, the latter has a number of bugs in IE8 which were fixed in this framework. Secondly, jGrid has built-in mobile-first responsiveness :-)

jGrid is build using SASS (http://sass-lang.com/), so if you are new to SASS, you'll need to compile it first: http://lmgtfy.com/?q=how+to+compile+sass

#### Why use justify-based grid?

1. No need to specify gutter between columns: all columns in one "row" are distributed equally.
2. No browser rounding issues = no "jumping" floated containers on screen zoom/resize.
3. Centering a column relatively to another column is super easy: just set `vertical-align: middle;` on both.

## How to use (basic)

jGrid is very easy to use.

```html
<div class="grid">
    <div class="col-12">...</div>
    <div class="col-6">...</div> <div class="col-6">...</div>
</div>
```

By default, `.grid` container will provide you with 12-col grid. You can add classes `col-1` through `col-12` to tell each of inner `<div>`'s how many columns it should occupy. Additionally you have `prepend-N` and `append-N` classes which will reserve `N` columns of space before and after each block.

## Grid types

jGrid has 3 types of grids:

1. **Standard**. `max-width` depends on configurations (maximum amount of columns). This is default grid type (example above)
2. **Fluid**. No `max-width`. Grid will cover all available width. To use, add `fluid` class to the grid element: `<div class="grid fluid">`
3. **Without padding**. This grid type has no padding on `.grid` element (useful for inner grids). To add this grid just add `no-padding` class to grid element: `<div class="grid no-padding">`

## Goin' responsive

By default, jGrid has 4 breakpoints: 

* *mobile*: 6 columns
* *tablet*: 8 columns
* *desktop*: 12 columns, default one
* *large*: 18 columns

By default, your `col-*` classes would assume that you are working on the *desktop* breakpoint and will give similar percentage width on other breakpoints: `col-4` on *mobile* 6-column breakpoint will occupy about 1/3 of available grid space.

You can configure behaviour on different breakpoints by adding additional classes to your blocks:

* for *mobile*: `mobile-N`, `mobile-prepend-N`, `mobile-append-N`
* for *tablet*: `tablet-N`, `tablet-prepend-N`, `tablet-append-N`
* for *large*: `large-N`, `large-prepend-N`, `large-append-N`
 
where `N` stands for number of columns block should occupy on the respective grid. Example:

```html
<div class="grid">
    <div class="mobile-6 
                tablet-4 tablet-prepend-2 tablet-append-2 
                col-8 col-append-4 
                large-18">...</div>
</div>
```

will have the following behaviour based on breakpoints:

* *mobile* - will span 6 columns out of 6 available
* *tablet* - will span 4 columns (out of 8 available) and wil have 2 columns of reserved space before & after it
* *desktop* - will span 8 columns (out of 12 available) and will have 4 columns of reserved space after it
* *large* - will span 18 columns (out of 18 available)

## Configuring jGrid

inside `jgrid.scss` under `--- GRID CONFIGURATION ---` you can fine-tune parameters to your needs.

*  `$font-size` and `$line-height` are default font-size/line-height for current context. These values are set to 0 on `.grid` element, and need to be set back in each of `.col-*` elements.
*  `$column-width`, `$column-gutter`, and `$column-padding` are grid parameters. Those will determine grid's max-width and breakpoints.
*  `$desktop` - default number of columns
*  `$mobile`, `$tablet`, and `$large` are number of columns for each breakpoint. These breakpoints are optional, so if you do not want to have *large* breakpoint, just set `$large: false;`
