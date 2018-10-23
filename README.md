# bem-flex-grid

CSS flex grid, [BEM](http://getbem.com/) compliant.

*A responsive grid that perfectly fits the window size in both width and height and lets you design interfaces such as a car dashboard or a bloomberg page, as well as a scrollable page of widgets.*

## Grid block and elements

At core the grid system consists of one block `.bfg` and several elements `.bfg__box`.

```html
<div class="bfg">
  <div class="bfg__box"></div>
  <div class="bfg__box"></div>
  ...
</div>
```

Fill the boxes using the optional `.bfg__content` element.

```html
<div class="bfg">
  <div class="bfg__box">
    <div class="bfg__content"></div>
  </div>
  ...
</div>
```

Add an header to the content using the optional `.bfg__header` element.

```html
<div class="bfg">
  <div class="bfg__box">
    <div class="bfg__header"></div>
    <div class="bfg__content"></div>
  </div>
  ...
</div>
```

Add multiple actions to the header using the optional `.bfg__action` element.

```html
<div class="bfg">
  <div class="bfg__box">
    <div class="bfg__action"></div>
    <div class="bfg__action"></div>
    ...
    <div class="bfg__header"></div>
    <div class="bfg__content"></div>
  </div>
  ...
</div>
```

## .bfg modifiers

### .bfg--row, .bfg--col

It is required to define the direction the `.bfg__box` elements are placed in the `.bfg` block, using `.bfg--row` or `.bfg--col` modifiers.

```html
<div class="bfg bfg--row">...</div>
```

> When using `.bfg--row` modifier, the grid needs the `.bfg` block width (or its parent width) to be defined.

```html
<div class="bfg bfg--col">...</div>
```

> When using `.bfg--col` modifier, the grid needs the `.bfg` block height (or its parent height) to be defined.

### .bfg--wrap

To allow `.bfg__box` elements to wrap as needed onto multiple lines, use the optional `.bfg--wrap` modifier.

```html
<div class="bfg bfg--wrap">...</div>
```

### .bfg--[B]lines-[N]

**[B]** Breakpoint: `xl-`, `lg-`, `sm-`, `xs-` or none.

**[N]** Number: `2`, `3` or `4`.

As said above, if you use the selector `.bfg.bfg--row.bfg--wrap` then `.bfg__box` elements are placed in the row direction and wrapped onto multiple lines when needed.

But in this case the total height of all `.bfg__box` elements might be bigger than the `.bfg` block height itself!

If you know that there's exactly 2 lines of `.bfg__box` elements, you can constrain them to fit into the `.bfg` block, by using `.bfg--lines-2` modifier.

In the same way, use `.bfg--lines-3` or `.bfg--lines-4` modifiers to fit exactly 3 or 4 lines respectively.

> In this case, all the rows will have the same height.

```html
<div class="bfg bfg--row bfg--wrap bfg--lines-2">...</div>
```

```html
<div class="bfg bfg--row bfg--wrap bfg--lines-3">...</div>
```

```html
<div class="bfg bfg--row bfg--wrap bfg--lines-4">...</div>
```

The same pattern applies to the selector `.bfg.bfg--col.bfg--wrap`.

```html
<div class="bfg bfg--col bfg--wrap bfg--lines-2">...</div>
```

```html
<div class="bfg bfg--col bfg--wrap bfg--lines-3">...</div>
```

```html
<div class="bfg bfg--col bfg--wrap bfg--lines-4">...</div>
```

As the grid is responsive, you can change the number of lines at each breakpoint.

**Example:**

- Fit boxes on 2 lines for all *screen size* (even greater than 1200px).
- Fit boxes on 3 lines for *large screens* (until 992px).
- Fit boxes on 4 lines for *small screens* (until 768px).

```html
<div class="bfg
  bfg--lines-2
  bfg--lg-lines-3
  bfg--sm-lines-4">
  ...
</div>
```

### .bfg--gap, .bfg--gap-in

To add a gap between `.bfg__box` elements, use `.bfg--gap` modifier.

```html
<div class="bfg bfg--gap">...</div>
```

In this case, the grid is self contained and you don't need to add margin (or padding) to the parent node of the `.bfg` block.

But if you prefer to define a main margin (or padding) to the parent node of the `.bfg` block then use `.bfg--gap-in` modifier.

```html
<div style="margin: 1rem">
  <div class="bfg bfg--gap-in">...</div>
</div>
```

```html
<div style="padding: 1rem">
  <div class="bfg bfg--gap-in">...</div>
</div>
```

> The default value of the gap is `1rem` (see below the Sass variable `$bfg-gap`).

### .bfg--main-[P]

**[P]** Position: `center`, `end`, `between`, `around`.

Justify content along the "main" axis using `.bfg--main-*` modifiers.

```html
<div class="bfg">...</div><!-- default grid behavior is like: `.bfg--main-start` -->

<div class="bfg bfg--main-center">...</div>

<div class="bfg bfg--main-end">...</div>

<div class="bfg bfg--main-between">...</div>

<div class="bfg bfg--main-around">...</div>
```

> This is relevant only when the total size of the boxes along the line is less than `12` (see below the size modifiers for `.bfg__box` element).
> Then you can choose the distribution mode of the remaining space.

### .bfg--cross-[P]

**[P]** Position: `start`, `center`, `end`.

Align items along the "cross" axis using `.bfg--cross-*` modifiers.

```html
<div class="bfg">...</div><!-- default grid behavior is like: `.bfg--cross-stretch` -->

<div class="bfg bfg--cross-start">...</div>

<div class="bfg bfg--cross-center">...</div>

<div class="bfg bfg--cross-end">...</div>
```

### .bfg--box-overflow, .bfg--content-overflow

By default, `.bfg__box` and `.bfg__content` elements use the rule `overflow: auto;`.

Use `.bfg--box-overflow` modifier on `.bfg` block to apply the rule `overflow: visible;` instead on all `.bfg__box` elements.

```html
<div class="bfg bfg--box-overflow">...</div>
```

Use `.bfg--content-overflow` modifier on `.bfg` block to apply the rule `overflow: visible;` instead on all `.bfg__content` elements.

```html
<div class="bfg bfg--content-overflow">...</div>
```

> In the same way, use `.bfg__box--overflow` modifier on `.bfg__box` element and `.bfg__content--overflow` modifier on `.bfg__content` element to apply this behavior to a specific element.

```html
...
  <div class="bfg__box bfg__box--overflow">
    <div class="bfg__content bfg__content--overflow">...</div>
  </div>
...
```

### .bfg--[B]reverse

**[B]** Breakpoint: `xl-`, `lg-`, `sm-`, `xs-` or none.

Use `.bfg--reverse` modifier to reverse the boxes order.

```html
<div class="bfg bfg--reverse">...</div>
```

As the grid is responsive, you can reverse the `.bfg__box` elements order at each breakpoint.

```html
<div class="bfg bfg--reverse">...</div>

<div class="bfg bfg--xl-reverse">...</div>

<div class="bfg bfg--lg-reverse">...</div>

<div class="bfg bfg--sm-reverse">...</div>

<div class="bfg bfg--xs-reverse">...</div>
```

### .bfg--[B]disabled, .bfg--[B]disabled-all

**[B]** Breakpoint: `xl-`, `lg-`, `sm-`, `xs-` or none.

To disable the grid system for the current `.bfg` block only use `.bfg--disabled` modifier.

To disable the grid system for the current `.bfg` block and its chained or nested `.bfg` blocks use `.bfg--disabled-all` modifier.

```html
<div class="bfg bfg--disabled">...</div>

<div class="bfg bfg--disabled-all">...</div>
```

As the grid is responsive, you can disable the grid system at each breakpoint.

Here's an example of disabling the grid system for the current `.bfg` block only.

```html
<div class="bfg bfg--disabled">...</div>

<div class="bfg bfg--xl-disabled">...</div>

<div class="bfg bfg--lg-disabled">...</div>

<div class="bfg bfg--sm-disabled">...</div>

<div class="bfg bfg--xs-disabled">...</div>
```

## .bfg__box modifiers

### .bfg__box--[B][S]

**[B]** Breakpoint: `xl-`, `lg-`, `sm-`, `xs-` or none.

**[S]** Size: `1`, `2`, ..., `11`, `12`.

Define the `.bfg__box` element size using `.bfg__box--1`,  `.bfg__box--2`, ...,  `.bfg__box--11`,  `.bfg__box--12` modifiers.

```html
...
  <div class="bfg__box bfg__box--1"></div>
  <div class="bfg__box bfg__box--2"></div>
  ...
  <div class="bfg__box bfg__box--11"></div>
  <div class="bfg__box bfg__box--12"></div>
...
```

> If the total size of the boxes along the line is less than `12` then the remaining space is distributed depending of `.bfg--main-[P]` modifiers.

As the grid is responsive, you can change the `.bfg__box` element size at each breakpoint.

**Example:**

- Use `.bfg__box--5` to set the box size to be 5/12 of the available size for all *screen size* (even greater than 1200px).
- Add `.bfg__box--xl-6` to increase the size on *extra large screens* (until 1200px).
- Add `.bfg__box--lg-4` to reduce the size on *large screens* (until 992px).
- Add `.bfg__box--sm-8` to increase the size on *small screens* (until 768px).
- Add `.bfg__box--xs-12` to increase the size on *extra small screens* (until 576px).

```html
...
  <div class="bfg__box
    bfg__box--5
    bfg__box--xl-6
    bfg__box--lg-4
    bfg__box--sm-8
    bfg__box--xs-12">
  </div>
...
```

### .bfg__box--[B]first, .bfg__box--[B]last

**[B]** Breakpoint: `xl-`, `lg-`, `sm-`, `xs-` or none.

Use `.bfg__box--first` or `.bfg__box--last` modifiers to change the box order.

```html
...
  <div class="bfg__box bfg__box--6 bfg__box--last"></div>
  <div class="bfg__box bfg__box--6 bfg__box--first"></div>
...
```

As the grid is responsive, you can change the `.bfg__box` element order at each breakpoint.

### .bfg__box--fit

Use `.bfg__box--fit` modifier to indicate that a `.bfg__box` element should not grow or shrink.

Here's an example when using `.bfg--row` modifier:

```html
<div class="bfg bfg--row">
  <div class="bfg__box bfg__box--fit" style="width:150px">
    <!-- width is fixed at 150px -->
  </div>
  <div class="bfg__box bfg__box--4">
    <!-- width is 4/12 of the remaining space (`.bfg` width, minus 150px) -->
  </div>
  <div class="bfg__box bfg__box--8">
    <!-- width is 8/12 of the remaining space (`.bfg` width, minus 150px) -->
  </div>
</div>
```

Here's an example when using `.bfg--col` modifier:

```html
<div class="bfg bfg--col">
  <div class="bfg__box bfg__box--fit" style="height:150px"></div>
  <div class="bfg__box bfg__box--4"></div>
  <div class="bfg__box bfg__box--8"></div>
</div>
```

### .bfg__box--overflow

By default, `.bfg__box` element use the rule `overflow: auto;`.
Use `.bfg__box--overflow` modifier to apply the rule `overflow: visible;` instead.

```html
...
  <div class="bfg__box bfg__box--overflow">...</div>
...
```

### .bfg__box--nopad

When using `.bfg--gap` modifier, add `.bfg__box--nopad` modifier to remove the padding of a specific box.

```html
<div class="bfg bfg--row bfg--gap">
  <div class="bfg__box bfg__box--4"></div>
  <div class="bfg__box bfg__box--4 bfg__box--nopad">
    <!-- no padding -->
  </div>
  <div class="bfg__box bfg__box--4"></div>
</div>
```

### .bfg__box--theme-[N]

**[N]** Name: `light` or any string.

Use `.bfg__box--theme-light` to add look and feel to the box content, header and actions.

```html
...
  <div class="bfg__box bfg__box--theme-light">
    <div class="bfg__action"></div>
    <div class="bfg__header"></div>
    <div class="bfg__content"></div>
  </div>
...
```

> See below the Sass mixin `bfg-theme` to create your own themes.

## .bfg__content modifier

### .bfg__content--nopad

Use `.bfg__content--nopad` modifier to remove the box content padding.

```html
...
  <div class="bfg__content bfg__content--nopad"></div>
...
```

### .bfg__content--overflow

By default, `.bfg__content` element use the rule `overflow: auto;`.
Use `.bfg__content--overflow` modifier to apply the rule `overflow: visible;` instead.

```html
...
  <div class="bfg__content bfg__content--overflow">...</div>
...
```

## Chained and nested grids

### Chained grid

To chain grids, use selector `.bfg__box.bfg` to treat a `.bfg__box` *element* as a `.bfg` *block* too.

**Example:**

See below the `<div>` that has both roles:

- `.bfg__box.bfg__box--6` as it is an *element* of the parent `.bfg.bfg--col` *block*.
- `.bfg.bfg--row` as it is a *block* of the children `.bfg__box` *elements*.

```html
<div class="bfg bfg--col bfg--gap">
  <div class="bfg__box bfg__box--3"></div>

  <!-- Chained grid starts here, on the `.bfg__box` element -->
  <div class="bfg__box bfg__box--6 bfg bfg--row">

    <div class="bfg__box bfg__box--3"></div>
    <div class="bfg__box bfg__box--6"></div>
    <div class="bfg__box bfg__box--3"></div>

  </div>

  <div class="bfg__box bfg__box--3"></div>
</div>
```

### Nested grid

Another alternative consists to nest a new `.bfg` *block* inside a `.bfg__box` *element*.

> If you use `.bfg--gap` modifier, you need to add `.bfg__box--nopad` modifier on the parent `.bfg__box` of the nested grid.

```html
<div class="bfg bfg--col bfg--gap">
  <div class="bfg__box bfg__box--3"></div>
  <div class="bfg__box bfg__box--6 bfg__box--nopad">

    <!-- Nested grid starts here, inside the `.bfg__box` element -->
    <div class="bfg bfg--row">
      <div class="bfg__box bfg__box--3"></div>
      <div class="bfg__box bfg__box--6"></div>
      <div class="bfg__box bfg__box--3"></div>
    </div>

  </div>
  <div class="bfg__box bfg__box--3"></div>
</div>
```

## Sass customization

### Default variables

```scss
$bfg-gap: 1rem !default;

$bfg-padding: 0.5rem !default;

$bfg-header-height: 2rem !default;

$bfg-theme-light: (
  box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.075),
  border-radius: 3px,
  border-width: 1px,

  header-border: #d5d5d5,
  header-background: #f6f6f6,
  header-forground: false,

  content-border: #ddd,
  content-background: #fff,
  content-forground: false
) !default;

$bfg-theme-light-included: true;

$bfg-breakpoints: (
  xs: 576px,
  sm: 768px,
  lg: 992px,
  xl: 1200px
) !default;
```

**Example:**

To change the boxes gap, create a new file `my-custo-bfg.scss` with the following content:

```scss
// Overwrite gap
$bfg-gap: 2rem;

@import "[PATH_TO]/node_modules/bem-flex-grid/src/lib/bem-flex-grid.scss";
```

### Mixin

The `bfg-theme` mixin allows you to customize the content look and feel.

```scss
@mixin bfg-theme($name, $settings) { ... }
```

**Example:**

To add a new theme with name `info`, create a new file `my-custo-bfg.scss` with the following content:

```scss
@import "[PATH_TO]/node_modules/bem-flex-grid/src/lib/bem-flex-grid.scss";

// Add new theme
@include bfg-theme(info, (
  border-radius: 0,
  border-width: 3px,

  header-border: #90CAF9,
  header-background: #BBDEFB,
  header-forground: #1E88E5,

  content-border: #BBDEFB,
  content-background: #E3F2FD,
));
```

> Notice that omitted map keys (`box-shadow` and `content-forground` in this example) fall back to their default value.

Now, you can use the new theme named `info`:

```html
...
  <div class="bfg__box bfg__box--theme-info">
    <div class="bfg__action"></div>
    <div class="bfg__header"></div>
    <div class="bfg__content"></div>
  </div>
...
```

## Selectors summary

| `.bfg` block             |
| ------------------------ |
| `.bfg--row`              |
| `.bfg--col`              |
| `.bfg--gap`              |
| `.bfg--gap-in`          |
| `.bfg--wrap`             |
| `.bfg--main-center`      |
| `.bfg--main-end`         |
| `.bfg--main-between`     |
| `.bfg--main-around`      |
| `.bfg--cross-start`      |
| `.bfg--cross-center`     |
| `.bfg--cross-end`        |
| `.bfg--lines-2`, `.bfg--lines-xl-2`, `.bfg--lines-lg-2`, `.bfg--lines-sm-2`, `.bfg--lines-xs-2` |
| `.bfg--lines-3`, `.bfg--lines-xl-3`, `.bfg--lines-lg-3`, `.bfg--lines-sm-3`, `.bfg--lines-xs-3` |
| `.bfg--lines-4`, `.bfg--lines-xl-4`, `.bfg--lines-lg-4`, `.bfg--lines-sm-4`, `.bfg--lines-xs-4` |
| `.bfg--reverse`, `.bfg--xl-reverse`, `.bfg--lg-reverse`, `.bfg--sm-reverse`, `.bfg--xs-reverse` |
| `.bfg--disabled`, `.bfg--xl-disabled`, `.bfg--lg-disabled`, `.bfg--sm-disabled`, `.bfg--xs-disabled`                      |
| `.bfg--disabled-all`, `.bfg--xl-disabled-all`, `.bfg--lg-disabled-all`, `.bfg--sm-disabled-all`, `.bfg--xs-disabled-all`  |
| `.bfg--box-overflow`     |
| `.bfg--content-overflow` |

| `.bfg__box` element   |
| --------------------- |
| `.bfg__box--1`, `.bfg__box--xl-1`, `.bfg__box--lg-1`, `.bfg__box--sm-1`, `.bfg__box--xs-1` |
| `.bfg__box--2`, `.bfg__box--xl-2`, `.bfg__box--lg-2`, `.bfg__box--sm-2`, `.bfg__box--xs-2` |
| `.bfg__box--3`, `.bfg__box--xl-3`, `.bfg__box--lg-3`, `.bfg__box--sm-3`, `.bfg__box--xs-3` |
| ...                   |
| `.bfg__box--11`, `.bfg__box--xl-11`, `.bfg__box--lg-11`, `.bfg__box--sm-11`, `.bfg__box--xs-11` |
| `.bfg__box--12`, `.bfg__box--xl-12`, `.bfg__box--lg-12`, `.bfg__box--sm-12`, `.bfg__box--xs-12` |
| `.bfg__box--first`, `.bfg__box--xl-first`, `.bfg__box--lg-first`, `.bfg__box--sm-first`, `.bfg__box--xs-first` |
| `.bfg__box--last`, `.bfg__box--xl-last`, `.bfg__box--lg-last`, `.bfg__box--sm-last`, `.bfg__box--xs-last` |
| `.bfg__box--fit`          |
| `.bfg__box--nopad`        |
| `.bfg__box--overflow`     |
| `.bfg__box--theme-light`  |

| `.bfg__content` element   |
| ------------------------- |
| `.bfg__content--nopad`    |
| `.bfg__content--overflow` |

## Install

```bash
npm install

# Build `bem-flex-grid.css` and `bem-flex-grid.min.css` from `bem-flex-grid.scss`
# Build `bem-flex-grid.ie11.css` and `bem-flex-grid.ie11.min.css` from `bem-flex-grid.ie11.scss`
npm run build

# Build `index.html` from `README.md`
npm run doc

# Open showcase in your favorite browser
npm start
```
