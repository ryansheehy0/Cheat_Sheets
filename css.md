# Cascading Style Sheets(CSS)
- Everything in CSS is a box.
- Browser can use GPU to render things.

```
{setting name}: {setting value}
{setting name}: {top/bottom right/left}
{setting name}: {top right bottom left} /* Starts on top and goes clockwise*/
```

## Order in which CSS is applied
- Specificity
    - The more specific the tag(element vs class vs id) will be applied. In the order of id being the lowest, class 2nd, and element 3rd.
        - If you have more than one tag the more specific one wins.
        - http://specifishity.com/
- If given the same specificity last css attribute is applied.

## Background

| CSS Name         | What it does |
|------------------|--------------|
| background       | Combination of background properties.              |
| background-color |              |

## Text

| CSS Name    | What it does               |
|-------------|----------------------------|
| font-size   | Changes size of text.      |
| color       | Changes color of the text. |
| font-weight |                            |
| text-align: |                            | 


## Sizing

| CSS Name      | What it does                                                                    |
|---------------|---------------------------------------------------------------------------------|
| width         | Changes width of the content.                                                   |
| height        | Changes height of the content.                                                  |
| border-radius | Set equal width and height and border-radius to 50% to make it a circle. |

## Margin/Padding/Border/Outline

```
+-----------------------+
|        Margin         |
| +-------------------+ |
| |      Outline      | |
| | +---------------+ | |
| | |    Border     | | |
| | | +-----------+ | | |
| | | |  Padding  | | | |
| | | | +-------+ | | | |
| | | | |Content| | | | |
| | | | +-------+ | | | |
| | | +-----------+ | | |
| | +---------------+ | |
| +-------------------+ |
+-----------------------+
```
- The outline is ontop and doesn't effect any elements nearby.

```
padding: 
border: {size} {style} {color}
```
margin block start
margin block end
margine inline start
margin inline end

### Border styles

```
border-style: {type}
border-top-style: {type}
border-right-style: {type}
border-bottom-style: {type}
border-left-style: {type}
```

- solid
- dotted
- dashed
- double
- groove
- ridge
- inset
- outset
- none
- hidden

## Positioning

`position: {type}`

### Static
Default behavior.
### Relative
Relative to the normal position. Allows for top, right, bottom, left. Doesn't change the other elements. Still in the document flow.
### Absolute
Moves relative to the nearest position ancestor or the body if none is specified. In order to position to the nearest ancestor it needs to have a `position: relative`. Take it out of the flow of the document. Other elements ignore it.
### Fixed
Moves relative to the view port.
### Sticky

## Display

`display: {display name}`

| display name | What it does                                 |
|--------------|----------------------------------------------|
| inline       | makes element inline                         |
| block        | makes element block                          |
| none         | hides an element. Doesn't take up space. |

### Flex
Put `display: flex;` on parent.
- On parent is referring to the element that is containing the flex elements
- On child is referring to the element that the flex is being applied to.

|                  |                                                                                                                                         | On parent or On child |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------|-----------------------|
| flex-wrap:       | Forces elements to the next line if they don't fit.                                                                                     | On parent             |
| justify-content: | How content are spaced on the main axis. Applies to multiple items.                                                                     | On parent             |
| justify-items:   | Aligns the main axis multiple lines of flex items created by flex-wrap.                                                                 | On parent             |
| justify-self:    | Aligns self on main axis.                                                                                                               | On child              |
| align-content:   | How items are spaced on the cross axis. Applies to multiple items.                                                                      | On parent             |
| align-items:     | Aligns the cross axis multiple lines of flex items created by flex-wrap                                                                 | On parent             |
| align-self:      | Align self on cross axis.                                                                                                               | On child              |
| flex-direction:  | Change the direction which flex is. By default it is row                                                                                | On parent             |
| order:           | Changes the ordering priority of an element. If multiple items have the same order value, their original order is maintained. On child. | On child              |

|                                              |                                                                                           | On parent or On Child |
|----------------------------------------------|-------------------------------------------------------------------------------------------|-----------------------|
| flex: {flex-grow} {flex-shrink} {flex-basis} | flex-basis is the minimum width the element can be at. Doesn't go smaller than that size. | On child              |

### flex-wrap
- wrap
- wrap-reverse

### flex-direction
Can change the main axis and the cross axis.
- row
- row-reverse
- column
- column-reverse

### justify/align -content/-items/-self
- center
- left
- right
- space-between
- space-around
- space-evenly
- baseline
- end
- start

Flex box froggy Game
    - https://flexboxfroggy.com/

### Grid

## Visibility

`visibility: {visibility name}`

| visibility name | What it does |
|----------|--------------|
| hidden   |  Hides an element. Takes up space.            |

list-style-type: none; /* No bullet points */

## Units

|     |                        |
|-----|------------------------|
| px  | pixles                 |
| %   | Size of parent element |
| vw  | Screen width           |
| vh  | Screen height          |
| em  |                        |
| deg |                        |

## Change css based on width of the screen

```
// Change css when screen width is 1000px or less
@media screen and (max-width: 1000px){}
or 
@media screen and (width < 1001px) {}
    // <= doesn't work

// Only between 1000px and 800px inclusive
@media screen and (max-width: 1000px) and (min-width: 800px){}
```

You can also do min-height or max-height

## transform
`transform: {function}`

### transform functions
- skew(deg) or skew(x, y) or skewX() or skewY()
- rotate(deg)
- scale(x) or scale(x, y) or scaleX() or scaleY()
- translateX() or translateY() or translate(x, y)

## Need to research
box-sizing: border-box;
text-decoration: none;
All Media queries
    - tend to go at the very bottom so that they overwrite the other css
    @media print
        - When user wants to print you can change the css
box-shadow:
    - Offset, blur, color
