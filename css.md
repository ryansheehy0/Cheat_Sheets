[Home](./README.md)

# Cascading Style Sheets(CSS)
A language used to customize the styling of HTML and/or XML.

```
selector{
    property: property value;
}
/* Comments */
/*
    The setting value order is in {top/bottom right/left} or
    {top right bottom left}
*/
```

## Table of contents
- [Miscellaneous](#miscellaneous)
- [Background](#background)
    - [Linear Gradient](#linear-gradient)
- [Text](#text)
- [Sizing](#sizing)
    - [Box Sizing](#box-sizing)
- [Margin/Padding/Border/Outline](#marginpaddingborderoutline)
    - [Border Styles](#border-styles)
- [Positioning](#positioning)
    - [Static](#static)
    - [Relative](#relative) 
    - [Absolute](#absolute)
    - [Fixed](#fixed)
    - [Sticky](#sticky)
- [Display](#display)
    - [Flex](#flex)
        - [flex-wrap](#flex-wrap)
        - [flex-direction](#flex-direction)
        - [justify/align -content/-items/-self](#justifyalign--content-items-self)
    - [Grid](#grid)
- [Visibility](#visibility)
- [Units](#units)
- [Adaptive Screen Width](#adaptive-screen-width)
- [Transform](#transform)
    - [Transform Functions](#transform-functions)
- [Pseudo classes/elements](#pseudo-classeselements)
    - [Pseudo classes](#pseudo-classes)
        - [Custom JavaScript Pseudo class](#custom-javascript-pseudo-class)
    - [Pseudo elements](#pseudo-elements)
- [CSS reset](#css-reset)
- [CSS selectors](#css-selectors)
    - [CSS combinators](#css-combinators)
    - [CSS attribute selectors](#css-attribute-selectors)
    - [Selector Specificity](#selector-specificity)
- [Variables in CSS](#variables-in-css)
- [Need to research](#need-to-research)
- [JASS](#jass)

## Miscellaneous
- Everything in CSS is a box.
- Browser can use GPU to render things.
- `margin: 0 auto;`
    - Can be used to center something horizontally in the screen.
    - Doesn't work if there isn't a defined width for the parent.
- `margin-left:` can be used to indent a list.
- list-style-type: none; 
    - Removes bullet points on list.
- cursor:
    - Changes cursor. To get the little hand it is `pointer`.
- `box-shadow: h-offset v-offset blur spread color inset;`
    - inset creates and inset shadow so it appears to be inside the element.

## Background

| CSS Name                                                                | What it does                                                       |
|-------------------------------------------------------------------------|--------------------------------------------------------------------|
| background                                                              | Combination of background properties.                              |
| background-color                                                        | Sets the background color.                                         |
| background-image: url('file path');                                     | Sets a background image.                                           |
| background-size                                                         | Sets the how the background image is shown. Usually `cover`        |
| background-repeat                                                       | Sets background image repeating property. Usually `no-repeat`      |
| background-position                                                     | Sets the position of the background image. Usually `center center` |
| background: linear-gradient(direction, color stop 1, color stop 2, ...) | Creates a gradient that can be between 2 or more colors.           |

### Linear Gradient
- Direction
    - to top/right/bottom/left
    - They can be combined. Ex: `to top right`
    - Angles can be used.

## Text

| CSS Name        | What it does                                                                                            |
|-----------------|---------------------------------------------------------------------------------------------------------|
| font-size       | Changes size of text.                                                                                   |
| color           | Changes color of the text.                                                                              |
| font-weight     | Changes the thickness or boldness of the text characters.                                               |
| text-align      | Aligns the text itself. Not its container.                                                              |
| font-style      | Sets italics, normal, or oblique.                                                                       |
| text-transform  | Used to control the capitalization. none, capitalize, uppercase, lowercase, initial, inherit.           |
| text-decoration | Changes underline, overline, line-through, or other effects.                                            |
| font-family     | Sets the font of the text. Apply multiple fonts for backups. `sarif` is common on almost all devices.   |
| line-height     | Specifies the height of the line. This includes vertical spacing between lines and highlighting height. |
| user-select     | Controls if the user can select/highlight the text.                                                     |

## Sizing

| CSS Name      | What it does                                                             |
|---------------|--------------------------------------------------------------------------|
| width         | Changes width of the content.                                            |
| height        | Changes height of the content.                                           |
| border-radius | Set equal width and height and border-radius to 50% to make it a circle. |
| max-width     | Sets the maximum width an element can have. Can't go over.               |
| min-width     | Sets the minimum width an element can have. Can't go under.              |

In order for a percentage height or width to work properly, the parent container needs to have a specified height.

### Box Sizing
`box-sizing` is used to control how the width and height are calculated, taking into account the element's padding and border.
- By default it is content-box. Which when specifying the width/height it changes the content.
- With border-box the width/height changes the content, padding, and border.

## Margin/Padding/Border/Outline

```
-----------------------------------
/             Margin              \
/  -----------------------------  \
/  /          Outline          \  \
/  /  -----------------------  \  \
/  /  /       Border        \  \  \
/  /  /  -----------------  \  \  \
/  /  /  /    Padding    \  \  \  \
/  /  /  /  -----------  \  \  \  \
/  /  /  /  / Content \  \  \  \  \
/  /  /  /  -----------  \  \  \  \
/  /  /  -----------------  \  \  \
/  /  -----------------------  \  \
/  -----------------------------  \
-----------------------------------
```

- The outline is on top and doesn't effect any elements nearby.

```
padding: 
border: {size} {style} {color}
```
margin block start
margin block end
margine inline start
margin inline end

### Border Styles

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

| display name | What it does                                                                                  |
|--------------|-----------------------------------------------------------------------------------------------|
| inline       | Makes element inline. Stays on the same line.                                                 |
| block        | Makes element a block. Puts element on a new line.                                            |
| none         | Hides an element. Doesn't take up space.                                                      |
| inline-block | Block of text but stuff can be on either side. Not styled the same as the other inline stuff. |
| initial      | Reverts the display to its defualt state.                                                     |

### Flex
Put `display: flex;` on parent.
- On parent is referring to the element that is containing the flex elements
- On child is referring to the element that the flex is being applied to.

Each wrap creates a new item. The content includes all the items/lines.

- You can use margins to force a wrap without doing a width of 100%.

|                  |                                                                                          | On parent or On child |
|------------------|------------------------------------------------------------------------------------------|-----------------------|
| flex-wrap:       | Forces elements to the next line if they don't fit.                                      | On parent             |
| justify-content: | How content are spaced on the main axis. Applies to multiple items.                      | On parent             |
| justify-items:   | Aligns the main axis multiple lines of flex items created by flex-wrap.                  | On parent             |
| justify-self:    | Aligns self on main axis.                                                                | On child              |
| align-content:   | How items are spaced on the cross axis. Applies to multiple items.                       | On parent             |
| align-items:     | Aligns the cross axis items/lines created by flex-wrap                                   | On parent             |
| align-self:      | Align self on cross axis.                                                                | On child              |
| flex-direction:  | Change the direction which flex is. By default it is row                                 | On parent             |
| order:           | Changes the ordering priority of an element.                                             | On child              |

|                                              |                                                                                           | On parent or On Child |
|----------------------------------------------|-------------------------------------------------------------------------------------------|-----------------------|
| flex: {flex-grow} {flex-shrink} {flex-basis} | flex-basis is the initial size of the flex item before any available space is distributed.| On child              |

#### flex-wrap
- wrap
- wrap-reverse

#### flex-direction
Can change the main axis and the cross axis.
- row
- row-reverse
- column
- column-reverse

#### justify/align -content/-items/-self
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
Similar to flex-box/display flex, but for 2 dimensions instead of 1.

Put `display: grid` on parent.

|                        |                                                                |
|------------------------|----------------------------------------------------------------|
| grid-template-columns: | Sets the columns of the grid.                                  |
| grid-template-rows:    | Sets the rows of the grid.                                     |
| grid-auto-rows:        | Determines the size of all rows added after the template rows. |
| grid-gap:              | Sets the size of the gaps between both rows and columns.       |
| grid-row-gap:          | Sets the size of the gaps between rows.                        |
| grid-columns-gap:      | Sets the size of the gaps between columns.                     |
| grid-template-areas:   | Used to define named grid areas in a grid container.           |

#### Grid Template
- Fractional units can be used to set the grid templates to take up the available space.

```
div{
    display: grid;
    grid-template-columns: 2fr 1fr;
}
```

- The repeat command can be used instead of writing out all the lengths one at a time. `repeat(4, 100px)` is the same as `100px 100px 100px 100px`.
- `grid-auto-rows: minmax(150px, auto)` can be used to prevent overflows.

##### Grid Template Areas
Used to define named grid areas in a grid container.

```
div{
    grid-template-areas:
        "header header"
        "sidebar content"
        "sidebar content"
}

div div{
    grid-area: header; /*Sets the child div as the header */
}

```

## Visibility

`visibility: {visibility name}`

| visibility name | What it does                      |
|-----------------|-----------------------------------|
| visible         | Default.                          |
| hidden          | Hides an element. Takes up space. |

## Units

|     |                             |
|-----|-----------------------------|
| px  | pixles                      |
| %   | Size of parent element      |
| vw  | Screen width                |
| vh  | Screen height               |
| rem | Relative to root font size usually defined by the browser. |

## Adaptive Screen Width

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

## Transform
`transform: {function}`

### Transform Functions
- skew(deg) or skew(x, y) or skewX() or skewY()
- rotate(deg)
- scale(x) or scale(x, y) or scaleX() or scaleY()
- translateX() or translateY() or translate(x, y)

## Pseudo Classes/Elements

### Pseudo Classes
Pseudo classes allow you to style an element based on a specific state or condition.

Pseudo classes take the format of {selector}:{pseudo-class}

These are the most common pseudo classes.

- hover
    - The mouse is over the element
- active
    - An element is actively being interacted with such as clicked.
- focus
    - Element is in focus.
- visited
    - Link has been visited.
- checked
    - Elements is checked
- nth-child(n)
    - n can be `even`, `odd`, or another number.
- not()
    - Negation selector

#### Custom JavaScript Pseudo Class
The JavaScript is used to create a custom state or condition.

```
<!-- HTML -->
<div class="my-class-element"/>

// JavaScript
let myClassElements = document.querySelectorAll(".my-class-element")

myClassElements.forEach((element) => {
    // Custom state or condition.
    element.addEventListener("click", () => {
        element.classList.toggle("custom-pseudo-class")
    })
})

/* CSS */
.my-class-element:custom-pseudo-class{
    /* Styling */
}
```

### Pseudo Elements
In order for the pseudo elements to show the content has to be set. Usually `content: ""`

Pseudo elements have the format of {selector}::{pseudo-element-name}

These are the most common pseudo element.

- before/after
    - Goes before or after the content. Not before or after the margin.
    - before or after don't work on imgs.
    - before
        - Inserts content before the element.
    - after
        - Inserts content after the element.

## CSS Reset
The browser applies some CSS by default. The CSS reset is used to remove this default CSS so that your website will look the same on all browsers.

Your custom CSS has to be applied after the CSS reset so that the custom CSS overwrites the CSS reset.

## CSS Selectors
CSS selectors are used to select an element in order to apply styling to it.

|                  |                                                 |
|------------------|-------------------------------------------------|
| .class           | Selects elements with class="class"             |
| .class1.class2   | Selects elements with both class1 and class2    |
| #id              | Selects elements with id="id"                   |
| element          | Selects all elements of that element            |
| element.class    | Selects all elements of that element with class |
| element, element | Selects all elements of both elements           |
| *                | Selects all elements of any type                |

### CSS Combinators
CSS combinators are special characters that are used to select specific elements with relations to another element.

|       |                                                          |
|-------|----------------------------------------------------------|
| space | descendant selector                                      |
| >     | child selector                                           |
| \+    | selects an element that directly follows another element |
| ~     | general sibling selector                                 |

```
/* Example */
    /* HTML */
<div>
   <p>Par 1</p>
   <div>
      <p>Par 2</p>
   </div>
</div>
<p>Par 3</p>
<p>Par 4</p>

    /* CSS */
div p       /* Selects Par 1 and Par 2 */
div > p     /* Selects Par 1*/
div + p     /* Selects Par 3*/
div ~ p     /* Selects Par 3 and Par 3*/
```

### CSS Attribute Selectors
CSS attribute selectors select elements based upon attributes and attribute values.

|                       |                                                                                                      |
|-----------------------|------------------------------------------------------------------------------------------------------|
| [attribute]           | Select elements with attribute.                                                                      |
| [attribute="value"]   | Selects elements with attribute="value"                                                              |
| [attribute~="value"]  | Selects elements with attribute containing "value" as a stand alone word. So "value-" will not work. |
| [attribute\|="value"] | Selects elements with attribute starting with "value-" or matching exactly "value"                   |
| [attribute^="value"]  | Selects elements with attributes starting with "value"                                               |
| [attribute$="value"]  | Selects elements with attributes ending with "value"                                                 |
| [attribute*="value"]  | Selects elements with attributes containing "value"                                                  |

```
/* Example */
    /* HTML */
<div attribute class="div1"/>
<div attribute="value" class="div2"/>
<div attribute="value-test" class="div3"/>
<div attribute="values" class="div4"/>

    /* CSS */
[attribute]{
    /* Styles div1, div2, div3, and div4 */
}
[attribute="value"]{
    /* Styles div2 */
}
[attribute~="value"]{
    /* Styles div2 */
}
[attribute|="value"]{
    /* Styles div2 and div3 */
}
[attribute^="value"]{
    /* Styles div2, div3, and div4 */
}
[attribute$="value"]{
    /* Styles div2 */
}
[attribute*="value"]{
    /* Styles div2, div3, and div4 */
}
```

### Selector Specificity
- The CSS selector that is more specific will be applied.
    - Specificity is calculated based upon 4 components in the order of more specificity to less specificity.
        - !important is the most specific. `property: property value !important;`
        - Specificity 1,0,0,0: Inline styles
        - Specificity 0,1,0,0: IDs
        - Specificity 0,0,1,0: Classes, attributes, and pseudo-classes
        - Specificity 0,0,0,1: Elements and pseudo-elements
    - To calculate the specificity, assign a value to each of the four components and count the occurrences from left to right. The higher the value, the higher the specificity.
- If given the same specificity last CSS attribute is applied.

```
/* If all the selectors target the same element then the one with the highest specificity will be applied. */
body div#header.container {
  /* Specificity: 0,1,1,2 */
  /* This has the highest specificity so it will be applied. */
}

#header {
  /* Specificity: 0,1,0,0 */
}

div.container {
  /* Specificity: 0,0,1,1 */
}

h1 {
  /* Specificity: 0,0,0,1 */
}
```

## Variables in CSS

```
/* Declare vars*/
:root{/*Doesn't have to be in root, but it is recommended. Root allows all css bodies to use the variables.*/
    --hex-var: #ffffff;
    --string-var: "string";
    --px-var: 10px;
}

/* Reference vars */
var(--var);

/* Sets the variable again */
.class{
    --hex-var: #000000;
}
```

JavaScript can be used to set variables in CSS.

```
/* JavaScript */
document.documentElement.style.setProperty("--var", "10px")

/* CSS */
:root{
    --var: 0;
}
```

## JASS

Often times a jass.css file is used which has a lot of CSS utility classes which can be added and removed with JS to apply custom CSS easily.
