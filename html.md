[Home](./README.md)

# HTML
- The purpose of this cheat sheet is to provide an overview of the most useful HTML elements.

## Table of Contents

## Start of HTML

```
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

## Text Formatting

```
<h1>Heading</h1>        <!-- Headings from 1 to 6 -->
<p>Paragraph</p>
<strong>Bold</strong>
<em>Italic</em>
<sup>Superscript</sup>
<sub>Subscript</sub>
<del>Crossed out</del>
<ins>Underline</ins>
```

## Links and Images

```
<a href="URL/filepath">Link</a>
<img src="URL/filepath" alt="Description">
    <!-- "Image of" is said before alt texts. -->
```

## Lists

```
<ul>                 <!-- Unordered list -->
  <li>Item 1</li>    <!-- List item -->
  <li>Item 2</li>
</ul>
<ol>                 <!-- Ordered list -->
  <li>Item 1</li>
  <li>Item 2</li>
</ol>
```

## Tables

```
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

## Forms

```
<form action="/submit" method="post">  <!-- Defines a form -->
  <input type="text" name="username" placeholder="Username">  <!-- Text input -->
  <input type="password" name="password" placeholder="Password">  <!-- Password input -->
  <input type="submit" value="Submit">  <!-- Submit button -->
  <input type="checkbox" name="agree" id="agree">  <!-- Checkbox -->
  <label for="agree">I agree to the terms</label>

  <input type="radio" name="gender" value="male">  <!-- radio button where you can only click the circle -->
  <label for="male">male</label>
  <input type="radio" name="gender" value="female">
  <label for="female">female</label>

  <input type="radio" name="gender" id="male">  <!-- radio button where you can click the label and the circle-->
  <label for="male">male</label>
  <input type="radio" name="gender" id="female">
  <label for="female">female</label>

  <textarea name="message" placeholder="Message"></textarea>  <!-- Textarea -->
  <select name="country">  <!-- Select dropdown -->
    <option value="us">United States</option>
    <option value="ca">Canada</option>
  </select>
</form>
```

## Grouping

```
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

## Comments

```
<!-- Comments -->
```

## HTML entities
- Used to represent reserved characters within HTML.

| Text    | Symbol |
|---------|--------|
| \&lt;   | <      |
| \&gt;   | >      |
| \&amp;  | &      |
| \&quot; | "      |
| \&apos; | '      |
| \&copy; | &copy; |
| \&reg;  | &reg;  |

## Attributes

|          |                                                                          |
|----------|--------------------------------------------------------------------------|
| class    | Elements can have multiple classes and multiple elements can have the same class. |
| id       | A unique identifier. 2 or more elements cannot have the same id.         |
| style    | Inline CSS.                                                              |
| title    | Additional info that is often displayed as a tooltip.                    |
| disabled | Disables user interaction.                                               |

## Inline elements vs block elements
- Block elements take up the whole line
- Inline elements just are inline
- You can force inline or block with CSS

## CSS in HTML
- Put into the `<head>` of the HTML so the browser can style before it paints the page.

```
<link rel="stylesheet" type="text/css" href="CSS File Path.css" />
```

## JavaScript in HTML
- Put at the very end of the HTML `<body>` so the JavaScript can interact with the HTML elements. 

```
<script src="script.js"></script>
```
