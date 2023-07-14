[Home](./README.md)

# Bootstrap

A front end framework that provides pre-designed CSS and JavaScript components, styles, and utilities.

```
// CSS in the head before any custom CSS
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css">
// JS script to the end of the body before any custom JS
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>
```

To use bootstrap you add classes to html element in order to create different elements.

## Table of Contents

- [Table of Contents](#table-of-contents)
- [Components](#components)
- [Containers](#containers)
  - [Container](#container)
  - [Container-Fluid](#container-fluid)
- [Buttons](#buttons)
- [Colors](#colors)
- [Icons](#icons)

## Components

| Components Name | Description                                                                  |
|-----------------|------------------------------------------------------------------------------|
| Alerts          | A small feedback message in a specific color.                                |
| Badges          | A colored rectangle around text in order to bring attention to it.           |
| Breadcrumbs     | Navigation aid to represent hierarchy. `Home / Library / Data`               |
| Buttons         | A button.                                                                    |
| Cards           | Flexible container to display content such as imgs, text, and buttons.       |
| Carousel        | Slideshow for cycling through a set of items.                                |
| Collapse        | Allows element's CSS display to be toggled easily between none and default.  |
| Dropdowns       | A dropdown menu.                                                             |
| List group      | A stylized ul or ol that can also include buttons and other elements.        |
| Modal           | A dialog window that overlays ontop of the current page.                     |
| Navbars         | A navigation bar that can collapse in a hamburger button on smaller screens. |
| Paginations     | Used to navigate between pages                                               |
| Popovers        | Small overlay that displays when an element is clicked or hovered upon.      |
| Progress bars   | A progress bar                                                               |
| Scrollspy       | Highlighted navigation links based upon the position in a scrolling element. |
| Spinners        | Animated loading symbol.                                                     |
| Toasts          | Small closable notifications at the bottom of the screen.                    |
| Tooltips        | Like popovers but smaller, texted based, more concise info.                  |
| Icons           | Icons from bootstrap and other common 3-rd party icon libraries.             |
| Tables          | A table.                                                                            |

## Containers

A container contains content that is centered horizontally and can adapt to different screen sizes.

Gutters are the blank spaces on the sides of the container. As the screen size changes the gutters change sizes, but the container remains fixed width until it hits a brake point.

```
<div class="container">
  <div class="row">
    <div class="col-6">Column 1</div> 
    <div class="col-4">Column 2</div> 
    <div class="col-2">Column 3</div> 
  </div>
</div>
<!--
    column 1 takes up 6/12 or 50%
    column 2 takes up 4/12 or 33.33%
    column 3 takes up 2/12 or 16.66%
-->
```

| Breakpoint        | Class name | Dimensions  |
|-------------------|------------|-------------|
| X-Small           | None       | x < 576px   |
| Small             | sm         | x >= 576px  |
| Medium            | md         | x >= 768px  |
| Large             | lg         | x >= 992px  |
| Extra Large       | xl         | x >= 1200px |
| Extra Extra large | xxl        | x >= 1400px |

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

If the cols add up to more than 12 they overlap to the next line.

```
<div class="container">
  <div class="row">
    <div class="col-12">Column 1</div> Takes up 100% of the 1st line
    <div class="col-6">Column 2</div> Takes up 50% of the 2nd line
    <div class="col-6">Column 3</div> Takes up 50% of the 2nd line
  </div>
</div>
<!--
    column 1 takes up 100% of the 1st line
    column 2 takes up 50% of the left side of the 2nd line
    column 3 takes up 50% of the right side of the 2nd line
-->
```

### Container
When a brake point is met then the container changes width otherwise the gutter dynamically changes.  

### Container-Fluid
Takes up the full width with there being no gutters.

## Buttons

```
<button type="button" class="btn">Button</button>
<!--
    type="button" is used to prevent the button from acting like a submit button and accidentally submitting forms.
-->
```

## Colors

| ColorName | Default Color     |
|-----------|-------------------|
| primary   | Blue              |
| secondary | Grey              |
| success   | Green             |
| danger    | Red               |
| warning   | Yellow            |
| info      | Sky Blue          |
| light     | Whiteish          |
| dark      | Blackish          |
| link      | Looks like a link |

|                       |                          |
|-----------------------|--------------------------|
| btn-ColorName         | Color the button         |
| btn-outline-ColorName | Color the button outline |
| bg-ColorName          | Color the background     |

## Icons

```
// Link the bootstrap CSS icons
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.7.2/font/bootstrap-icons.css">

// The html
    <i class="bi bi-icon"></i>
```
