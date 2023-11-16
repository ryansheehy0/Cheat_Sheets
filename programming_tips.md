[Home](./README.md)

# Advanced Programming Tips

## Table of Contents

<!-- TOC -->

- [Advanced Programming Tips](#advanced-programming-tips)
  - [Table of Contents](#table-of-contents)
  - [Project Management](#project-management)
  - [Formatting and Rules](#formatting-and-rules)
  - [Code Organization](#code-organization)

<!-- /TOC -->

## [Project Management](#table-of-contents)
- Have a well detailed end goal app idea
  - A full write up on how all the features are going to work and how each page of the app will look and work
- Develop in stages of Minimum Viable Product
  - MVP 1, MVP 2, etc. Keep adding MVPs until you reach all the features in the end goal app idea
  - The 1st MVP should be the most bare bones features as possible. Just the minimum to make it somewhat usable.
- Delegate tasks and every few days or week have a group meeting on the progress of those tasks
  - If one member is falling behind then put more resources to help them catch up

## [Formatting and Rules](#table-of-contents)
- No space between ()s and {s
- Use "s instead of 's
- When setting variables use spaces between the =s
- Use guard clauses when possible
- Pseudo-code in comments before programming
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