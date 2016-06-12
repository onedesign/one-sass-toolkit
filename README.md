# One Sass Toolkit

A collection of foundational utilities for Sass.

## Tools

- [Color]()
- [Type Styles]()
- [Spacing]()

## Install

```
npm install one-sass-toolkit --save
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

