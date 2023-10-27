[Home](./README.md)

# HTML
- The purpose of this cheat sheet is to provide an overview of the most useful HTML elements.

## Table of Contents

<!-- TOC -->

- [HTML](#html)
  - [Table of Contents](#table-of-contents)
  - [Start of HTML](#start-of-html)
  - [Text Formatting](#text-formatting)
  - [Links and Images](#links-and-images)
  - [Lists](#lists)
  - [Tables](#tables)
  - [Forms](#forms)
  - [Grouping](#grouping)
  - [Self Closing Tags](#self-closing-tags)
  - [Comments](#comments)
  - [HTML entities](#html-entities)
  - [Attributes](#attributes)
  - [Inline elements vs block elements](#inline-elements-vs-block-elements)
  - [CSS in HTML](#css-in-html)
  - [JavaScript in HTML](#javascript-in-html)

<!-- /TOC -->

## [Start of HTML](#table-of-contents)

```HTML
<!DOCTYPE html>
<html>
    <head> <!-- Contains metadata -->
        <title>Title</title>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    </head>
    <body> <!-- Contains the visible content -->
    </body>
</html>
```

You can add an favicon in the top of the tab by adding this to the head:

```HTML
<link rel="icon" href="/favicon.svg" >
```

## [Text Formatting](#table-of-contents)

```HTML
<h1>Heading</h1>        <!-- Headings from 1 to 6 -->
<p>Paragraph</p>
<strong>Bold</strong>
<em>Italic</em>
<sup>Superscript</sup>
<sub>Subscript</sub>
<del>Crossed out</del>
<ins>Underline</ins>
```

## [Links and Images](#table-of-contents)

```HTML
<a href="URL/filepath">Link</a>
<a href="URL/filepath" target="_blank">Link in new tab</a>
<img src="URL/filepath" alt="Description">
    <!-- "Image of" is said before alt texts. -->
```

## [Lists](#table-of-contents)

```HTML
<ul>                 <!-- Unordered list -->
  <li>Item 1</li>    <!-- List item -->
  <li>Item 2</li>
</ul>
<ol>                 <!-- Ordered list -->
  <li>Item 1</li>
  <li>Item 2</li>
</ol>
```

## [Tables](#table-of-contents)

```HTML
<table>              <!-- Defines a table -->
  <tr>               <!-- Table row -->
    <th>Header 1</th> <!-- Table header cell -->
    <th>Header 2</th>
  </tr>
  <tr>
    <td>Data 1</td>   <!-- Table data cell -->
    <td>Data 2</td>
  </tr>
</table>
```

## [Forms](#table-of-contents)

```HTML
<form action="/submit" method="post">  <!-- Defines a form. Method can only be get and post. -->
  <input type="text" name="username" placeholder="Username">  <!-- Text input -->
  <input type="password" name="password" placeholder="Password">  <!-- Password input -->
  <input type="submit" value="Submit">  <!-- Submit button -->
  <input type="checkbox" name="agree" id="agree">  <!-- Checkbox -->
  <label for="agree">I agree to the terms</label>

  <input type="hidden" name="hiddenValue" value="hidden value sent"> <!-- Sends a hidden value when sending the form -->

  <input type="radio" name="gender" value="male">  <!-- radio button where you can only click the circle -->
  <label for="male">male</label>
  <input type="radio" name="gender" value="female">
  <label for="female">female</label>

  <input type="radio" name="gender" id="male">  <!-- radio button where you can click the label and the circle-->
  <label for="male">male</label>
  <input type="radio" name="gender" id="female">
  <label for="female">female</label>

  <textarea name="message" placeholder="Message"></textarea>  <!-- Textarea used for multi-line text input. -->

  <select name="country">  <!-- Select dropdown -->
    <option value="us">United States</option>
    <option value="ca">Canada</option>
  </select>
</form>
```

Forms by default send a http POST request with the endpoint in action. The server responds with a html page to be loaded after the submission of the post.

## [Grouping](#table-of-contents)

```HTML
<div>Container</div>
<span>Inline</span>
<header>Header</header>
<main>Main content</main>
<footer>Footer</footer>
<nav>Navigation menu</nav>
<section>Section of a document</section>
<article>Self contained article</article>
<aside>Side Content</aside>
```

## [Self Closing Tags](#table-of-contents)

```HTML
<br/>    <!-- Line break -->
<hr/>    <!-- Horizontal rule/line -->
<wbr/>   <!-- Word break. The browser can line wrap at that point if necessary. -->
```

## [Comments](#table-of-contents)

```HTML
<!-- Comments -->
```

## [HTML entities](#table-of-contents)
- Used to represent reserved characters within HTML.

| Text    | Symbol            |
|---------|-------------------|
| &lt\;   | <                 |
| &gt\;   | >                 |
| &amp\;  | &                 |
| &quot\; | "                 |
| &apos\; | '                 |
| &copy\; | &copy;            |
| &reg\;  | &reg;             |
| &deg\;  | &deg;             |
| &emsp\; | non breakable tag |

## [Attributes](#table-of-contents)

|          |                                                                          |
|----------|--------------------------------------------------------------------------|
| class    | Elements can have multiple classes and multiple elements can have the same class. |
| id       | A unique identifier. 2 or more elements cannot have the same id.         |
| style    | Inline CSS.                                                              |
| title    | Additional info that is often displayed as a tooltip.                    |
| disabled | Disables user interaction.                                               |

## [Inline elements vs block elements](#table-of-contents)
- Block elements take up the whole line
- Inline elements just are inline
- You can force inline or block with CSS

## [CSS in HTML](#table-of-contents)
- Put into the `<head>` of the HTML so the browser can style before it paints the page.

```HTML
<link rel="stylesheet" type="text/css" href="style.css" />
```

## [JavaScript in HTML](#table-of-contents)
- Put at the very end of the HTML `<body>` so the JavaScript can interact with the HTML elements. 

```HTML
<script src="script.js"></script>
```

- You can also use the `defer` keyword and put in in the header where it will only be loaded after the dom is created.

```HTML
<script src="script.js" defer></script>
```