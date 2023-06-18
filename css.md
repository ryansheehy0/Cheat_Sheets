# Cascading Style Sheets(CSS)
A language used to customize the styling of HTML and/or XML.

```
selector{
    setting-name: setting value;
}
/* Comments */
/*
    The setting value order is in {top/bottom right/left} or
    {top right bottom left}
*/
```

## Table of contents
- [Miscellaneous](#miscellaneous)
- [Specificity](#specificity)
- [Background](#background)
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
- [Change css based on width of the screen](#change-css-based-on-width-of-the-screen)
- [transform](#transform)
    - [transform functions](#transform-functions)
- [Pseudo classes/elements](#pseudo-classeselements)
    - [Pseudo classes](#pseudo-classes)
        - [Custom JavaScript Pseudo class](#custom-javascript-pseudo-class)
    - [Pseudo elements](#pseudo-elements)
- [CSS reset](#css-reset)
- [CSS combinators](#css-combinators)
- [CSS attribute selectors](#css-attribute-selectors)
- [Variables in CSS](#variables-in-css)
- [Need to research](#need-to-research)

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

## Specificity
- The CSS selector that is more specific will be applied last. In the order of id being the lowest, class 2nd, and element 3rd.
    - In the order of less specificity to more specificity. Universal selector(*), 1 element(div), multiple number of elements with more elements meaning more specificity( div div), 1 class(.class), universal selector and 1 class(*.class), 
    - http://specifishity.com/
- If given the same specificity last CSS attribute is applied.

## Background

| CSS Name                            | What it does                                                       |
|-------------------------------------|--------------------------------------------------------------------|
| background                          | Combination of background properties.                              |
| background-color                    | Sets the background color.                                         |
| background-image: url('file path'); | Sets a background image.                                           |
| background-size                     | Sets the how the background image is shown. Usually `cover`        |
| background-repeat                   | Sets background image repeating property. Usually `no-repeat`      |
| background-position                 | Sets the position of the background image. Usually `center center` |
| background: linear-gradient(        | Creates a gradient that can be between 2 or more colors.           |

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

## Visibility

`visibility: {visibility name}`

| visibility name | What it does |
|----------|--------------|
| hidden   |  Hides an element. Takes up space.            |


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

## Pseudo classes/elements

### Pseudo classes
Pseudo classes allow you to style an element based on a specific state or condition.

Pseudo classes take the format of {selector}:{pseudo-class}

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

#### Custom JavaScript Pseudo class
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

### Pseudo elements
In order for the pseudo elements to show the content has to be set. Usually `content: ""`

Pseudo elements have the format of {selector}::{pseudo-element-name}

- before
    - Inserts content before the element.
- after
    - Inserts content after the element.
- placeholder

## CSS reset
The browser applies some CSS by default. The CSS reset is used to remove this default CSS so that your website will look the same on all browsers.

Your custom CSS has to be applied after the CSS reset so that the custom CSS overwrites the CSS reset.

## CSS selectors
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

### CSS combinators
CSS combinators are special characters that are used to select specific elements with relations to another element.

|       |                           |
|-------|---------------------------|
| space | descendant selector       |
| >     | child selector            |
| \+    | selects an element that directly follows another element |
| ~     | general sibling selector  |

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

### CSS attribute selectors
CSS attribute selectors select elements based upon attributes and attribute values.



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

## Need to research
- Make 3d images with CSS
- All pseudo elements
- All pseudo classes
- All css selectors
    - [type="checkbox"]
        - What does this do?
    - [href$=".css"]
        - $ means it ends with .css
        - * means contains .css. [href*=".css"]
    - * wild card selector
        - any element
- All Media queries
    - tend to go at the very bottom so that they overwrite the other css
    @media print
        - When user wants to print you can change the css
