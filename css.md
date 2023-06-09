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

| CSS Name  | What it does               |
|-----------|----------------------------|
| font-size | Changes size of text.                            |
| color     | Changes color of the text. |
| font-weight     |  |


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
Flex box froggy
    - Game
### Grid

## Visibility

`visibility: {visibility name}`

| visibility name | What it does |
|----------|--------------|
| hidden   |  Hides an element. Takes up space.            |


list-style-type: none; /* No bullet points */
