[Home](./README.md)

# HTML Canvas

HTML `<canvas></canvas>` allows you to have a drawable canvas in html.

First get the 2d rendering context

```javascript
const canvas = document.getElementById('myCanvas')
const context = canvas.getContext('2d')
```

| Rectangle Functions              | Description                           |
|----------------------------------|---------------------------------------|
| .fillRect(x, y, width, height)   | Creates a filled rectangle            |
| .strokeRect(x, y, width, height) | Creates an outline of a rectangle     |
| .clearRect(x, y, width, height)  | Clears a rectangle area on the canvas |

| Path Functions                                          | Description                                                                                            |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| .beginPath()                                            | Starts a new path or resets the current path                                                           |
| .moveTo(x, y)                                           | Moves the current position to x an y coordinates                                                       |
| .lineTo(x, y)                                           | Adds a line from the current position to x and y coordinates. This doesn't change the current position |
| .arc(x, y, radius, startAngle, endAngle, anticlockwise) | Creates a circular arc                                                                                 |
| .closePath()                                            | Closes the current path                                                                                |
| .fill()                                                 | Fill the current path with the current fill style                                                      |
| .stroke()                                               | Stroke the current path with the current stroke style                                                  |

How to set the fill style
How to set the stroke style


| Text Functions            | Description                     |
|---------------------------|---------------------------------|
| .font = '16px Arial'      | Sets the font                   |
| .fillText("Text", x, y)   | Draws filled text on canvas     |
| .strokeText("Text", x, y) | Draws outline of text on canvas |

| Transform functions             | Description                                                     |
|---------------------------------|-----------------------------------------------------------------|
| .rotate(angle)                  | Rotate canvas by an angle                                       |
| .scale(scaleX, scaleY)          | Scale the canvas                                                |
| .translate(x, y)                | Moves the origin of the canvas                                  |
| .setTransform(a, b, c, d, e, f) | Resets the current transformation matrix and applies a new one. |

| Image functions                        | Description                                       |
|----------------------------------------|---------------------------------------------------|
| .drawImage(image, x, y, width, height) | Draws an image or video onto the canvas           |
| .getImageData(x, y, width, height)     | Gets the image data of a rectangle on the canvas. |
| .putImageData(image data)              | Paints the image data onto the canvas             |
