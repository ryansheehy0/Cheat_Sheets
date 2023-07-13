[Home](./README.md)

# Bootstrap

A front end framework that provides pre-designed CSS and JavaScript components, styles, and utilities.

Add a CSS link in the head and a JS script to the end of the body to use Bootstrap.

To use bootstrap you add classes to html element in order to create different elements.

## Table of Contents

## Components

| Components Name | Description                                                                  |
|-----------------|------------------------------------------------------------------------------|
| Alerts          | A small feedback message in a specific color.                                |
| Badges          |                                                                              |
| Breadcrumbs     |                                                                              |
| Buttons         | A button.                                                                    |
| Cards           | Flexible container to display content such as imgs, text, and buttons.       |
| Carousel        | Slideshow for cycling through a set of items.                                |
| Collapse        | Allows element's CSS display to be toggled easily between none and default.  |
| Dropdowns       | A dropdown menu.                                                             |
| List group      | A stylized ul or ol that can also include buttons and other elements.        |
| Modal           | A dialog window that overlays ontop of the current page.                     |
| Navbars         | A navigation bar that can collapse in a hamburger button on smaller screens. |
| Panels          |                                                                              |
| Paginations     | Used to navigate between pages                                               |
| Popovers        | Small overlay that displays when an element is clicked or hovered upon.      |
| Progress bars   | A progress bar                                                               |
| Scrollspy       | Highlighted navigation links based upon the position in a scrolling element. |
| Spinners        | Animated loading symbol.                                                     |
| Toasts          | Small closable notifications at the bottom of the screen.                    |
| Tooltips        | Like popovers but smaller, texted based, more concise info.                  |
| Clearfix        |                                                                              |
| Icons           | Icons from bootstrap and other common 3-rd party icon libraries.             |
| Tables          |                                                                             |
| Responsive Ut   |                                                                              |
| Gutters         |                                                                              |

## Padding and Margin
p-#
m-#
mb-# margin bottom
my-# margin top and bottom
mx-# margin left and right
the # is between 1 and 5

## Layouts
d-flex
align-items-center
ms-auto
container-fluid
bg-dark
text-light
mb-#
p-#

## Containers

A container is a fixed-width container that is center horizontally.

- Gutters are the blank spaces on the sides of the container.

```
<div class="container">
  <div class="row">
    <div class="col-6">Column 1</div>
    <div class="col-4">Column 2</div>
    <div class="col-2">Column 3</div>
  </div>
</div>
```

`col-#`. All the cols should add up to 12.

|           |                                                                |
|-----------|----------------------------------------------------------------|
| col       | Equal width columns                                            |
| col-#     | Columns that occupy #/12 columns                               |
| col-sm-#  | Columns that occupy #/12 columns on small screens and up       |
| col-md-#  | Columns that occupy #/12 columns on medium screens and up      |
| col-lg-#  | Columns that occupy #/12 columns on large screens and up       |
| col-xl-#  | Columns that occupy #/12 columns on extra large screens and up |
| col-xxl-# | Columns that occupy #/12 columns on extra extra large screens and up |

Do mobile first. Start with the smaller classes first and then the larger classes.

### Container
When a brake point is met then the container changes width otherwise the gutter dynamically changes.  

### Container-Fluid
Takes up the full width with there being no gutters.


but
card
btn-info //color class
bg-warning // yellow
bg-success //green
bg-danger //
bg-dark
bg-light
display-3
text-white
text-center
rounded // rounds corners
form-group

## Width and Height
min-vh-100
min-vw-100
min-w-100

## Customize Colors
Bring custom css below the bootstrap css

Order matters with bootstrap because classes can overwrite each other.
