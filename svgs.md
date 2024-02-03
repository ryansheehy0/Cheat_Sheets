[Home](./README.md)

# SVGs

Scalable Vector Graphics is a XML namespace markup language used to describe 2d vector graphics. They are infinity scalable without loosing image quality.

In order to make a svg you need to wrap your element in

```HTML
<svg xmlns="http://www.w3.org/2000/svg">
  <!-- SVG content goes here -->
</svg>
```

XML allows you to define your own custom elements and attributes, but in order to apply rules to these elements and attributes you need a XML namespace. The **xmlns** attribute is used to define this XML namespace.

What if you leave off xmlns?


## Table of Contents
<!-- TOC -->

- [SVGs](#svgs)
	- [Table of Contents](#table-of-contents)
	- [Width, Height, and viewBox attributes](#width-height-and-viewbox-attributes)
	- [Attributes for all SVG elements](#attributes-for-all-svg-elements)
		- [stroke-dasharray and stroke-dashoffset](#stroke-dasharray-and-stroke-dashoffset)
		- [transform](#transform)
		- [Accessible rich internet applicationsaria-*](#accessible-rich-internet-applicationsaria-)
	- [Line](#line)
	- [Elements](#elements)

<!-- /TOC -->

## [Width, Height, and viewBox attributes](#table-of-contents)

The width and height properties define the width and height of the viewPort. The viewPort allows you to see a portion of an svg. Like looking through a window.
- The default units for width and height are pixels.

The viewBox is like the viewPort, but it allows for panning and zooming. Like looking through binoculars.

When defining the viewBox attribute it uses this format: `viewBox="min-x min-y width height"`
- min-x and min-y define the top left corner of viewBox and these are used for panning
- width and height are used for zooming.
	- width/height > width/height attributes then zoom out
	- with/height < width/height attributes then zoom int
- You should only use the viewBox attribute when the width and height attributes are defined.

## [Attributes for all SVG elements](#table-of-contents)
- fill: Defines the fill color
- stroke: Defines the stroke color
- stroke-width
- opacity
- id and class
- Different event attributes
	- onclick, onmouseover, onmouseout, onload, etc


### [stroke-dasharray and stroke-dashoffset](#table-of-contents)
**stroke-dasharray** is an array of values which defines the lengths of alternating dashes and gaps. It follows the pattern of line length then gap length.

- Ex 1: `stroke-dasharray="10 5"` line length of 10 followed by gap length of 5. This repeats for the whole SVG element.
- Ex 2: `stroke-dasharray="2 6 8"` line 2 -> gap 6 -> line 8 -> gap 2 -> line 6 -> gap 8 -> repeat.

**stroke-dashoffset** rotates the lines and gaps. If it's positive it rotates it clockwise, if negative counter clockwise.

### [transform](#table-of-contents)

- translate(x, y)

### [Accessible rich internet applications(aria-*)](#table-of-contents)

## [Line](#table-of-contents)

## Elements
<rect width="400" height="100" style="fill:rgb(0,0,255);stroke-width:10;stroke:rgb(0,0,0)" />
Rounded rect
<rect width="400" height="100" style="fill:rgb(0,0,255);stroke-width:10;stroke:rgb(0,0,0)" />
<circle cx="50" cy="50" r="40" stroke="green" stroke-width="4" fill="yellow" />
<polygon />
<ellipse cx="100" cy="70" rx="85" ry="55" fill="url(#grad1)" />
  <text fill="#ffffff" font-size="45" font-family="Verdana" x="50" y="86">SVG</text>
  Sorry, your browser does not support inline SVG.

- rect
- circle
- line
- path
	- Can also be used for splines
- text
- g(group)
- use
	- References and uses other svg elements
- polygon
- ellipse
- polyline
- tspan
	- Text that can be broken up into multiple lines
- textPath
	- Specifies a path which text should be rendered
- defs
	- Defines reusable svg elements
- image
- clipPath
	- Used to hide or show portions of other elements
- mask
	- Defines an image mask that can be used to hide or reveal portions of other elements.
- linearGradient
- radialGradient
- pattern
	- Defines a patter that can be used to fill SVG shapes
- filter
	- image filters
- animate
- animateTransform
	- scaling or rotating animation
- animateMotion
- metadata
- desc
	- text description of the svg
- title


You can use class to define styling for different svg elements.