# Design System Helper

This guide is the developer documentation for the CivicTechJobs Design System (CTJ-DS). Inside is not only an overview of our components, but also usage tips, and strategies to translate Figma designs into components for flexible, dynamic webpages.

## Concepts

To understand our Design System, here are some overarching concepts to keep in mind when working with the DS.

### Implementing from Figma to Frontend Development

UI designers specialize in turning project requirements into a graphical interface that fits project requirements. Designers, however, are not coders. As a result, here are some development-related aspects of componentization that designers do not consider:

- the way components change as screen size changes
- the ease of replicating components in code
- the proper way to configure svg assets for development

Because of these factors, the way a prototype is built on Figma does not necessarily translate 1:1 to how the designs should be build as code. For example, Figma designs could not indicate the use of SCSS mixins to abstract CSS code, nor the use of percentages as units of size.

Likewise, we must contend with the fact that Figma designs are static screens tied to very specific viewport sizes. As developers we need to recreate both the fidelity and intentions of a design.

As a developer, we need to effectively communicate with designers at multiple stage of the Figma design process. This means understanding the intentions behind a design, and providing recommendations or alternatives that are simpler and easier for the developer to implement and maintain.

At CivicTechJobs, designers use two standard viewport size when creating our UIs: 1440px for desktop and 375px for mobile. The appearance of the UI beyond these two sizes are determined by us, as developers, as we componentize the Figma designs.

### Scalable and Responsive Components

When creating or using components, it is good to keep in mind the differences between a scalable component and responsive component.

A scalable component:

- takes up a certain **fraction** of the total screensize regardless of screen size
- shrinks and grows along with screen size
- uses relative css sizing units, such as % or vm

[show example of columns that are scalable]

A responsive component:

- takes up an **absolute** amount of the screen regardless of screen size
- remains static until reaching a certain breakpoint
- uses static css sizing units, such as px

[show example of buttons that are reponsive]

Scalability and responsiveness are not mutually exclusive. A webpage can contain both scalable and responsive components. As a matter of fact, a single component can be both responsive and scalable.

[insert gif of card which changes size at breakpoints that shows both]

Only by combining both scalability and responsiveness in our design, can we create a high-quality website. When working with the DS, ask yourself, should this portion be scalable or responsive? If this portion is scalable, does it still work in mobile? Do I need a media query to develop for different viewports?

### PropType as Documentation

As a small project, React [recommends](https://reactjs.org/docs/static-type-checking.html) the use of [PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html) as our type checking library.

By using PropTypes with our components, we have an easy way to look up hints on how to use our components.

```Javascript
Button.propTypes = {
  addClass: PropTypes.string,
  color: PropTypes.oneOf(["primary", "primary-dark"]),
  disabled: PropTypes.bool,
  href: PropTypes.string,
  length: PropTypes.oneOf(["", "long"]),
  onClick: PropTypes.func,
  size: PropTypes.oneOf(["sm", "md", "lg", "icon"]),
  target: PropTypes.oneOf([
    "_blank",
    "_self",
    "_parent",
    "_top",
    PropTypes.string,
  ]),
};
```
*<p style="text-align: center;">For this <Button\> component, PropTypes provide clues on props to pass in. As can be surmised, a small, long button would be declared as <Button size="sm" length="long"\> </p>*

Since comprehensive documentation is difficult to maintain, we rely on PropTypes and cleanly written code to provide clues on how to use each component. We recommend new developers take time to play with the components in [`components/`](https://github.com/hackforla/CivicTechJobs/tree/main/frontend/src/components).

## Components

While we can use pure CSS as our styling sheet, using SCSS with React components vastly improve our ability to standardize our components beyond just styling. Componentization allows:

- quick customizations through React props
- standardizations to our components for accessibility
- reuse of the same component across multiple pages
- updating designs by simply readjusting the base component

Because of these benefits, we use a component-first approach to developing web pages. Please componentize as much as possible and use them to build high-quality web pages!

As a note, the DS is put together based on industry trends and practices. If you had ever explored Bootstrap, MUI, or Atlassian Design System, you will see many similiaries between their components and ours.

### Layout and Columns

> "Using layout and column utilities automantically adds scalability to your pages."

As with most design systems, we use a standard 12-column system to subdivide our layouts. Each column, without spacing, is worth *8.33% of its container's width\**.

[show screenshot example of columns]

As is also standard, in order to maintain the 12-column format, margins take away from the width rather than add onto it.

[show gif of when spacing is added]

To use of our columns, first declare a parent container with the `.flex-container` class. Then use `col-*` classes in each children. The `*` specifies a number. For example:

```HTML
<div class="flex-container">
    <div class="col-6">6</div>
    <div class="col-2">2</div>
    <div class="col-2">2</div>
    <div class="col-1">1</div>
    <div class="col-1">1</div>
</div>
```
*<p style="text-align: center;">We need to use a parent `.flex-container` with `col-*` classes to subdivide the UI.</p>*

[shoow what happens when this code is rendered]

Our 12-column system can be used in conjunction with `.row` and nested `.col-*` to further subdivide the UI, and create more complex layouts.

```HTML
 <div class="flex-container mx-5">
        <div class="col-3">
          <div class="row">
            1
          </div>
          <div class="row">
            2
          </div>
        </div>
        <div class="col-9 row">
          <div class="col-3">3</div>
          <div class="col-6">4</div>
          <div class="col-3">5</div>
        </div>
      </div>
```
*<p style="text-align: center;">With `.flex-container`, `.row`, and `.col-*`, we can create complex layouts that fit our purposes.</p>*

[shoow what happens when this code is rendered]

> ###### *\*Note: Although Figma uses 12-col to subdivide the entire screen, our column classes subdivides the **container**. This means that we can make the divide the whole into columns, and then divide each column even further to achieve our desired ratios.*

### Smart Spacing

> "99% of the time, as screens shrinks, you want to reclaim space from paddings and margins."

The spacing utilties are classified by attributes, based on direction, and size, based on a 0-5 range.

**Table of Spacing Attributes**

| Spacing attribute (margins) | Meaning | \| | Spacing attribute (padding) | Meaning |
| :-----------: | :----------- | :-----------: | :-----------: |  :----------- |
| m | all margins | **\|** | p | all paddings |
| mt | margin-top | **\|** | pt | padding-top |
| mr | margin-right | **\|** | pr | padding-right |
| mb | margin-bottom | **\|** | pb | padding-bottom |
| ml | margin-left | **\|** | pl | padding-left |
| mx | margin-left and -right | **\|** | px | padding-left and -right |
| my | margin-top and -bottom | **\|** | py | padding-top and -bottom |

**Table of Spacing Sizes**

| Spacing size | Actual size (px) |
| ----------- | ----------- |
| 0 | 0px |
| 1 | 8px |
| 2 | 16px |
| 3 | 24px |
| 4 | 32px |
| 5 | 40px |

*<p style="text-align: center;">Tables showing the different way we classifies our spacing utilities. As an example, `.px-4` sets the left and right padding as 32px.</p>*

Because our DS is based on 12-columns, spacing utilities are made such that adding them on would not alter the 12-columns. For that reason, it is optimal to use the spacing utilities whenever possible over setting margins or padding.

As an example, if Figma indicates a 10px left margin, use either `.ml-1` or `.ml-2`.

Other times, Figma designs shows spacing that falls outside of our size range.

[show example of large range]

In this scenario, rather than set a specific margin, try to use layout utilities and center alignments to achieve an approximation of the design. This has the benefit of ensuring scalability and reducing the maintainence cost of the resulting code.

### Responsive Mixins

> "When using responsive mixins, order matters! Always declare them from big to small."

Several of our components have `*-responsive` mixins at the end of the `.scss` file. These are there as helpers to quickly create responsiveness into our components, keeping our code nice to read.

These mixins, as convention, always use max-width in its media query, so order matters! To use them properly, specify a default and declare screen size from largest to smallest:

```SCSS
.header-nav-menu {
  @include col-size(7);
  @include col-responsive("lgtablet", 8);
  @include col-responsive("smtablet", 6);
  @include col-responsive("mobile", 8);
}
```
*<p style="text-align: center;">DO: specify a default on top and declare `*-responsive` mixins from large to small screen sizes.</p>*

And do not use a smaller screen size above a larger one:

```SCSS
.header-nav-menu {
  @include col-responsive("mobile", 8);
  @include col-responsive("smtablet", 6);
  @include col-responsive("lgtablet", 8);
}
```
*<p style="text-align: center;">DON'T: declare `*-responsive` mixins without a top default or from small to large screen sizes.</p>*

### SVGs as Components and as Data-URLs

SVG assets are read into our codebase as React components or data-urls.

SVG components:

- allows the use of React props to dynamically alter the component on response
- requires editing stroke and fill values to inherit to allow passing in props
- requires a wrapper element to add additional styling
- are imported directly from the image file
- specified with a starting uppercase

Data-urls:

- are used as the src in `img` tags
- difficult to dynamically change
- easy to use if usage is only size dependent
- are imported with `?url` qualifiers
- specified with a starting lowercase

```Javascript
// COP Icons
import CopIconData from "./svgs/cop-icon-datascience.svg";
import CopIconEngineering from "./svgs/cop-icon-engineering.svg";
import CopIconOps from "./svgs/cop-icon-ops.svg";
import CopIconProduct from "./svgs/cop-icon-product.svg";
import CopIconUiux from "./svgs/cop-icon-uiux.svg";

import copIconData from "./svgs/cop-icon-datascience.svg?url";
import copIconEngineering from "./svgs/cop-icon-engineering.svg?url";
import copIconOps from "./svgs/cop-icon-ops.svg?url";
import copIconProduct from "./svgs/cop-icon-product.svg?url";
import copIconUiux from "./svgs/cop-icon-uiux.svg?url";
```
*<p style="text-align: center;">The top icons are imported from the image file as SVG components. The respective bottom icons are imported as data-urls.</p>*

When using our SVG assets make sure to use the best import for the job. In some cases, however, neither of these images are optimal to use. For example an SVG might have extra space that makes it hard to center.

[insert example of svg with extra spaces]

In this case, rather than calculating some difficult to maintain, complex spacing, simply request the design team to provide a better SVG or edit the SVG and inform the design team.

## Resources

[Atomic Design](https://bradfrost.com/blog/post/atomic-web-design/)<br>
[Atlassian Design System](https://atlassian.design/)<br>
[Bootstrap](https://getbootstrap.com/)<br>
[Material-UI](https://mui.com/)<br>