# One Sass Toolkit

A collection of foundational utilities for Sass.

## Tools

- [Color](#color)
- [Type Styles](#type-styles)
- [Spacing](#spacing)
- [Fluid Type](#fluid-type)

## Install

```sh
npm install one-sass-toolkit --save
```

```scss
// in your main.scss
@import "one-sass-toolkit/color";
@import "one-sass-toolkit/spacing";
@import "one-sass-toolkit/type-styles";
@import "one-sass-toolkit/fluid-type";
```

## Use

### Requirements & Assumptions

The included tools are based heavily on the frontend development process at One Design Company, and as a result make some assumptions about the tools you're using and how your styles are organized.

#### Media Queries

One Sass Toolkit uses [sass-mq](https://github.com/sass-mq/sass-mq) for responsive adjustments, which expects you to have a global `$mq-breakpoints` variable that defines your mobile-first breakpoints. The exact sizes you have defined for these breakpoints can be anything, and you can specify additional breakpoints:

```scss
$mq-breakpoints: (
  small: 500px,
  medium: 768px,
  large: 1024px,
  xlarge: 1400px
);
```

### Color

The `color` utility grabs colors and optionally generates helper class for your colors that can be used directly in your HTML.

#### As a SCSS function

```scss
.my-stuff {
  background-color: color(blue);
  color: color(yellow);
}
```

#### As an HTML class

```html
<div class="h-color-bg-blue">
  <h1 class="h-color-text-yellow">We all live in a yellow submarine</h1>
</div>
```

#### Required Setup

Relies on a `$colors` map variable existing in the following format:

```scss
$colors: (
  black: #222,
  white: #fff,
  gray: #aaa,
  blue: #118bc1,
  yellow: #ffe215
);
```

### Type Styles

Automatically generates all of the type styles for a project, provides a mixin for grabbing a specific set of predefined styles, adjusts type responsively, and provides optional helper classes for your type styles that can be used directly in your HTML.

#### As an SCSS mixin

```scss
.my-heading {
  @include type-style(heading);
}

// Outputs the following css

/*
.my-heading {
  font-family: Futura, 'Trebuchet MS', Arial, sans-serif,
  font-size: 1.4rem,
  line-height: 1,
  text-transform: normal,
  letter-spacing: 0
}

@media (min-width: 768px)
  .my-heading {
      font-size: 1.8rem;
  }
}
*/
```

#### As an HTML class

```html
<h1 class="h-type-heading">Ground control to Major Tom</h1>
```

#### Required Setup

Assumes that you are using 10-based `rem` (e.g. `font-size: 1.4rem; // 14 px`) units for sizing across the site, via something like `html { font-size: 62.5%; }`

Also relies on $`type-styles` and `$font-stacks` map variables existing in the following format:

```scss
$font-stacks: (
  futura-bold: (
    font-family: (Futura, 'Trebuchet MS', Arial, sans-serif),
    font-weight: 700,
    font-style: normal
  ),
  helvetica: (
    font-family: ('Helvetica Neue', Helvetica, Arial, sans-serif;),
    font-weight: normal,
    font-style: normal
  )
);

$type-styles: (
  heading: (
    stack: futura-bold,
    line-height: 1,
    text-transform: normal,
    letter-spacing: 0,
    sizes: (
      default: 14,
      medium: 18
    )
  ),

  body: (
    stack: helvetica,
    line-height: 1.4,
    text-transform: uppercase,
    letter-spacing: 1.2,
    font-smoothing: true,
    sizes: (
      default: 16,
      medium: 24
    )
  )
);
```

### Spacing

Mixin to provide spacing (either margin or padding) to a defined
location of an element and have that spacing scale down proportionally
at smaller screen sizes. Can also optionally generate helper classes for use directly in your HTML.

#### As an SCSS mixin

```scss
.foo + .bar {
  @include spacing(s); // by default, the value is applied to `margin-top`
}

.bar + .foo {
  @include spacing(m, padding-bottom);
}
```

#### As an SCSS function

**Important:** when provided as a function, the spacing will *not* be responsive.

```scss
.bar + .foo {
  margin-top: get-spacing(m);
}
```

#### As an HTML class

Works for any of the following classes:

- `h-spacing-top-margin-{$amount}`
- `h-spacing-bottom-margin-{$amount}`
- `h-spacing-top-padding-{$amount}`
- `h-spacing-bottom-padding-{$amount}`

```html
<h1 class="h-spacing-top-margin-m">Ground control to Major Tom</h1>
```

#### Required Setup

Relies on a $spacing map variable existing in the following format:

```scss
$spacing: (
  none: 0,
  xs: 2rem,
  s: 3rem,
  sm: 4rem,
  m: 5rem,
  ml: 6rem,
  l: 8.5rem,
  xl: 15rem
);
```

The exact names of the keys in this map aren't important, as long as `@include spacing(foo)` has a matching key `foo` in the map.

### Fluid Type
Written by [Indrek Paas](https://github.com/indrekpaas) and inspired by [Mike Riethmuller](https://madebymike.com.au/writing/precise-control-responsive-typography/) this mixin allows you to specify a minumum and maximum size for values. Allowing for more fluid websites.

#### As an SCSS mixin
```
@include fluid-type($properties)
/* Single property */
html {
  @include fluid-type(font-size, 320px, 1366px, 14px, 18px);
}

/* Multiple properties with same values */
h1 {
  @include fluid-type(padding-bottom padding-top, 20em, 70em, 2em, 4em);
}
```
