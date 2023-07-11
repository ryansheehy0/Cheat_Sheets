# Bootstrap

A front end framework that provides pre-designed CSS and JavaScript components, styles, and utilities.

You add classes to html element in order to create different elements.

See up to date links:

```
Add css in head
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-9ndCyUaIbzAi2FUVXJi0CjmCapSmO7SnpJef0486qhLnuZ2cdeRhO02iuK6FUUVM" crossorigin="anonymous">

Add JS to the end of body
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js" integrity="sha384-geWF76RCwLtnZ8qwWowPQNguL3RmwHVBC9FhGdlKrxdiJJigb/j/68SIy3Te4Bkz" crossorigin="anonymous"></script>
```

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
