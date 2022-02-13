# Design System Helper

This guide is the documentation for the CivicTechJobs Design System. Inside is not only an overview of our components, but also usage tips, and strategies to translate Figma designs into components and flexible, dynamic webpages.

## Concepts

### UI (User-Interface) Designers

UI designers specialize in turning project requirements into a graphical interface that fits project requirements. Most UI designers are not coders. It is rare to find a designer with the knowledge and skills typical of a web developer.

At CivicTechJobs, designers use two standard viewport size when creating our UIs, 1440px for desktop and 375px for mobile. This means that our product is made with a desktop and mobile first approach.

### Scalable and Responsive Components

When working with or creating components, it is good to keep in mind the differences between a scalable component and responsive component.

A scalable component:

- takes up a certain portion of the screen regardless of screen size
- shrinks and grows along with screen size
- uses relative css sizing units

[show example of columns that are scalable]

A responsive component:

- uses media queries to transform UIs depeding on screen size
- remains static until reaching a certain breakpoint
- uses static css sizing units

[show example of buttons that are reponsive]

Scalability and responsiveness are not mutually exclusive. A webpage can contain components that are both scalable and responsive. As a matter of fact, a single can be both responsive and scalable.

[insert gif of card which changes size at breakpoints that shows both]

### PropType as Documentation

As a small project, React [recommends](https://reactjs.org/docs/static-type-checking.html) the use of [PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html) as our type checking library.

By using PropTypes with our components, we have an easy way to look up hints on how to use our components.

[insert example with button]

## Components

While we can use CSS-only as our design system, using React components vastly improve our ability to standardize our components beyond just styling. With components, we can easily add JS functionality and standardize our components for accessibility.

### Layout and Columns

> "Using layout and column utilities automantically adds scalability to your pages."

As with most design systems, we use a standard 12-column system to divide our layout. Each column, without spacing, is worth *8.33% of its container's width*.

[show example of columns]

As is also standard, in order to maintain the 12-column format, margins take away from the width rather than add onto it. 

[show gif of when spacing is added]

To make full use of our columns, elements with `col-*` classes must be wrapped in a div with the `.flex-container` class.

```HTML
<div class="flex-contaner">
    <div class="col-6">1</div>
    <div class="col-1">2</div>
    <div class="col-1">3</div>
    <div class="col-1">4</div>
    <div class="col-1">5</div>
    <div class="col-1">6</div>
    <div class="col-1">7</div>
</div>

[shoow what happens when this code is rendered]

Our 12-column system can be used in conjunction with `.row` to further subdivide the UI, and create complex layouts.

<div class="flex-contaner">
    <div class="col-3">
        <div class="row">
            1
        </div>
        <div class="row">
            2
        </div>
    </div>
    <div class="col-9">3</div>
</div>

### Smart Spacing

> "99% of the time, as screens shrinks, you want to reclaim space from paddings and margins."

The spacing utilties are based upon a 0-5 range.

[insert table of values to translated px]

### Responsive Mixins

> "When using responsive mixins, order matters! Always declare them from big to small."

### SVGs as Components and as Data-URLs

## Resources