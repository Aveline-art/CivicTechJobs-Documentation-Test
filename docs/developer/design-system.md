# Design System Helper

This guide is the documentation for the CivicTechJobs Design System (CTJ-DS). Inside is not only an overview of our components, but also usage tips, and strategies to translate Figma designs into components and flexible, dynamic webpages.

## Concepts

### UI (User-Interface) Designers

UI designers specialize in turning project requirements into a graphical interface that fits project requirements. That said designers are not coders.

Some things that designers do not consider that developers do are:

- The way components change as screen size changes
- The ease of replicating components in code
- The proper way to configure assets

Because of thes factors, the way a prototype is built on Figma does not necessarily translate 1:1 on how the designs should be build as code. For example, the designs could not consider the use of SCSS mixins to abstract CSS code, nor the use of percentages as units of size.

As a developer, we need to effectively communicate with designers at multiple stage of the Figma design process. This means understanding the intention behind a design, and providing recommendations or alternatives that are simple and easy for the developer to implement and maintain.

At CivicTechJobs, designers use two standard viewport size when creating our UIs: 1440px for desktop and 375px for mobile. This means that as developers, we ourselves have to determine how the website appear in other viewport size.

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

Scalability and responsiveness are not mutually exclusive. A webpage can contain components that are both scalable and responsive. As a matter of fact, a single component can be both responsive and scalable.

[insert gif of card which changes size at breakpoints that shows both]

Only by combining both scalability and responsiveness in our design, can we create a high-quality website. When working with our design system, ask yourself, should this portion be scalable or responsive? If this portion is scalable, does it still work in mobile? Do I need a media query to develop for different viewports?


### PropType as Documentation

As a small project, React [recommends](https://reactjs.org/docs/static-type-checking.html) the use of [PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html) as our type checking library.

By using PropTypes with our components, we have an easy way to look up hints on how to use our components.

[insert example with button]

Because we are building our product with a component-first approach, it is important to be well-versed with our design system. In lieu of documentation, we do use PropTypes and cleanly written code to provide clues on how to use each component.

As an example,

[show example with the buttons proptypes]

## Components

While we can use CSS-only as our design system, using React components with SCSS vastly improve our ability to standardize our components beyond just styling. With components, we can add quick customizations through React props and standardize our components for accessibility. Because of these benefits, we use a component-first approach to developing web pages. Please componentize whenever you can and use them to build high-quality web pages!

As a note, the design system is put together based on industry trends and practices. If you had ever explored Bootstrap, MUI, or Atlassian Design System, you will see many similiaries between their components and ours.

### Layout and Columns

> "Using layout and column utilities automantically adds scalability to your pages."

As with most design systems, we use a standard 12-column system to subdivide our layouts. Each column, without spacing, is worth *8.33% of its container's width*.

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
```

[shoow what happens when this code is rendered]

Our 12-column system can be used in conjunction with `.row` to further subdivide the UI, and create more complex layouts.

```
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
```

### Smart Spacing

> "99% of the time, as screens shrinks, you want to reclaim space from paddings and margins."

The spacing utilties are based upon a 0-5 range, with an 8px difference between them.

[insert table of values to translated px]

Because our design system is based on 12-columns, spacing utilities are made such that adding them on would not alter the 12-columns. For that very reason, it is optimal to use the spacing utilities whenever possible over custom spacing.

For example, if Figma indicates a 10px spacing, use either the 8px or 16px utility. Other times, Figma indicates a space far outside of our utility's range.

[show example of large range]

In this scenario, do think about the intent behind the design before adding the space. Is it so wide because of alignment? Or are these actual spaces that would require a custom padding or margin?

### Responsive Mixins

> "When using responsive mixins, order matters! Always declare them from big to small."

Several of our components have *-responsive mixins at the end of the `.scss` file. These are there as helpers to create responsiveness into our components without directly calling the media utilities.

Each one of them uses max-width as part of its media query, so order matters! Do use them to go from largest screen size to small:

[insert image]

And do not use a smaller screen size above a larger one:

[insert image]

Please, also make a habit of setting a default so that unexpected behaviors do not happen. 

### SVGs as Components and as Data-URLs

SVGs are read into our code base in the form of a React component or as data-urls.

SVG components:

- allows the use of React props to dynamically alter the component on response
- requires editing stroke and fill values to inherit to allow passing in props
- requires a wrapper element to add additional styling

Data-urls:

- are used as the src in image tags
- difficult to dynamically change
- easy to use if usage is only size dependent

When using our SVG assets make sure to use the best version for the job. In some cases, however, neither of these are particularly helpful. For example an SVG might have extra space that makes it hard to center.

[insert example of svg with extra spaces]

In these cases, rather than calculating some difficult to maintain, complex spacing, simply request the design team to provide a better SVG, or edit the SVG, and send the updated version to the design team.

## Resources

[Atomic Design](https://bradfrost.com/blog/post/atomic-web-design/)
[Atlassian Design System](https://atlassian.design/)
[Bootstrap](https://getbootstrap.com/)
[Material-UI](https://mui.com/)