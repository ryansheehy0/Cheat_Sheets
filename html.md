# HTML
- The purpose of this cheat sheet is to provide an overview of the most useful HTML elements.

## Head elements
- Elements used in the &lt;head&gt; tag. Aren't displayed within the page.

| Element | Description |
| ------| ----|
| <a href="">Text</a> | Link |

## Inline elements
- Only occupy the space required by the content within them.
## Block elements
- Start on a new line and take up the whole line.
## Mathjax
- Mathjax is a way to display math expressions in HTML.
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


- Comments
- details
- summary
- links
- tables
- lists
    - ordered/unordered
- pre

For img alt text the screen reader automatically says image of. Just put what the alt image is. Ex: alt="cat" instead of alt="image of cat"


## Inline elements vs block elements
Block elements take up the whole like
Inline elements just are inline

You can force inline or block with css

### Inline
- 
### Block
- div

## Symantec Elements
navbar, section, aside

## Start of HTML

```
<!DOCTYPE html>
<html>
    <head>
        <title>Title</title>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    </head>
    <body>
    </body>
</html>
```

## CSS in HTML
- Put into the `<head>` of the HTML so the browser can style before it paints the page.

```
<style 
```

## JavaScript in HTML
- Put at the very end of the HTML `<body>` so the JavaScript can interact with the HTML elements. 

```
<script src="script.js"></script>
```
