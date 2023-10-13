[Home](./README.md)

# Advanced Programming Tips

## Table of Contents

<!-- TOC -->

- [Advanced Programming Tips](#advanced-programming-tips)
  - [Table of Contents](#table-of-contents)
  - [Formatting and Rules](#formatting-and-rules)
  - [Code Organization](#code-organization)

<!-- /TOC -->

## [Formatting and Rules](#table-of-contents)
- No space between ()s and {s
- Use "s instead of 's
- When setting variables use spaces between the =s
- Use guard clauses when possible
- Pseudocode in comments before programming
  - Code underneath comments
  - No spaces between comments and code

## [Code Organization](#table-of-contents)
It is almost always better to get started coding with bad organization and then organize your code when you can clearly see the patterns.

- Use function to re-use code
- If a class has a lot of methods brake out those methods into separate classes in a folder called main_subclasses
```
item
  item.js
  item_subclasses
    events.js
```
- If 2 or more classes share a significant amount of code use inheritance in a folder called main_children
```
item
  item.js
  item_children
    list.js
    card.js
```