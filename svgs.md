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

What does this do? xmlns:xlink="http://www.w3.org/1999/xlink"

## Table of Contents
<!-- TOC -->

- [SVGs](#svgs)
	- [Table of Contents](#table-of-contents)
	- [Width, Height, and viewBox attributes](#width-height-and-viewbox-attributes)
	- [Attributes for all SVG elements](#attributes-for-all-svg-elements)
		- [stroke-dasharray and stroke-dashoffset](#stroke-dasharray-and-stroke-dashoffset)
		- [transform](#transform)
	- [Line](#line)
	- [Rectangle](#rectangle)
	- [Polygon](#polygon)
	- [Polyline](#polyline)
	- [Circle](#circle)
	- [Ellipse](#ellipse)
	- [Path](#path)
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
- stroke-opacity
- fill-opacity
- id and class
- Different event attributes
	- onclick, onmouseover, onmouseout, onload, etc
- accessible rich internet applications(aria-)

### [stroke-dasharray and stroke-dashoffset](#table-of-contents)
**stroke-dasharray** is an array of values which defines the lengths of alternating dashes and gaps. It follows the pattern of line length then gap length.

- Ex 1: `stroke-dasharray="10 5"` line length of 10 followed by gap length of 5. This repeats for the whole SVG element.
- Ex 2: `stroke-dasharray="2 6 8"` line 2 -> gap 6 -> line 8 -> gap 2 -> line 6 -> gap 8 -> repeat.

**stroke-dashoffset** rotates the lines and gaps. If it's positive it rotates it clockwise, if negative counter clockwise.

### [transform](#table-of-contents)

- translate(x, y)
	- Moves the svg according to the top left
- rotate(degrees)
	- Rotates from the top left
- scale(ratio)
	- Scales by the ration from the top left
- skewX(angle) and skewY(angle)
	- Skews an element along the X or Y axis
- matrix(a, b, c, d, e, f)

The order of transforms matters
- `transform="translate(10, 10) rotate(45)`
	- Moves then rotates from the new origin set by translate
- `transform="rotate(45) translate(10, 10)`
	- Rotates from the original origin and then translates. The translation is also rotated.

## [Line](#table-of-contents)
`<line x1="" y1="" x2="" y2=""/>`

## [Rectangle](#table-of-contents)
`<rect x="" y="" width="" height=""`

## [Polygon](#table-of-contents)
Used to create a closed shape by connecting the first and last points.

- Polygon automatically connects the first and last points.

`<polygon points="x1,y1 x2,y2 x3,y3"`

- Lines are drawn at each of the points.
- Ex: `<polygon points="10,10 10,50 50,50"/>` draws a triangle

## [Polyline](#table-of-contents)
Used to create an open shape. There is no connecting between the last and first points.

`<polyline points="x1,y1 x2,y2 x3,y3/>`

## [Circle](#table-of-contents)
`<circle cx="" cy="" r=""`

## [Ellipse](#table-of-contents)
`<ellipse cx="" cy="" rx="" ry="" />`

## [Path](#table-of-contents)
Used to draw lines, arcs, quadratics, and cubic bezier curves.

- The path element used a virtual pen. Move the pen then draw with the pen. When a drawing element is used, it moves the virtual pen.
	- `Mx,y` moves the pen
	- `Lx,y` draws a line to x and y
		- `Hdistance` draws a line on the x axis that distance
		- `Vdistance` draws a line on the y axis that distance
	- `Arx,ry xRotation largeArcFlag,sweepFlag x,y` draws an elliptical arc
		- rx and ry are the radius in the x or y axis.
		- xRotation rotates the elliptical arc across the x axis
			- An xRotation of 45 rotates the elliptical arc from _ to \
		- largeArcFlag of 1 pics the arc that is that large of the 2
		- sweepFlag of 1 put the arc in the clockwise and 0 in the counterclockwise directions.
		- x and y are the ending points
	- `Qcx,cy x,y` draws the quadratic equations
		- cx and cy define the control point
		- x and y defines the end point
	- `Ccx1,cy1 cx2,cy2 x,y` draws the cubic bezier curve which has 2 more control points than the quadratic equation.
		- cx1,cy1 and cx2,cy2 defines the 2 other control points
		- x and y defines the end point
	- `Z` draws a line from the starting point to the end point of the path. If the start and end point are the same it closes the path.

- Any commands which are uppercase letters are absolutely positioned while any commands which are lowercase letters are relatively positioned.
	- Relatively positioned means positioned from the last command/virtual pen position.
	- Ex: `M100,100 L150,150` draws line from 100,100 to 150,150
	- Ex: `M100,100 l150,150` draws line from 100,100 to 250,250

```HTML
<path d="M100,100 L150,150 L150,200
	A50,50 0 1,0 100,150
	Q20,250 200,300
	C200,400 375,350 400,300
	Z
"/>
```


## Elements
  <text fill="#ffffff" font-size="45" font-family="Verdana" x="50" y="86">SVG</text>
  Sorry, your browser does not support inline SVG.

- text
- g(group)
- use
	- References and uses other svg elements
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