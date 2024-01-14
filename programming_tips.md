[Home](./README.md)

# Advanced Programming Tips

## Table of Contents

<!-- TOC -->

- [Advanced Programming Tips](#advanced-programming-tips)
  - [Table of Contents](#table-of-contents)
  - [Project Management](#project-management)
  - [Formatting and Rules](#formatting-and-rules)
  - [Code Organization](#code-organization)
  - [When to reuse code](#when-to-reuse-code)

<!-- /TOC -->

## [Project Management](#table-of-contents)
- Have a well detailed end goal app idea
  - A full write up on how all the features are going to work and how each page of the app will look and work
- Develop in stages of Minimum Viable Products(MVPs)
  - MVP 1, MVP 2, etc. Keep adding MVPs until you reach all the features in the end goal app idea
  - The 1st MVP should be the most bare bones features as possible. Just the minimum to make it somewhat usable.
  - The last 20-10% of your MVP will be integration hell and finding any edge cases where you code breaks
- Delegate tasks and every few days or week have a group meeting on the progress of those tasks
  - If one member is falling behind then put more resources to help them catch up

## [Formatting and Rules](#table-of-contents)
- No space between ()s and {s
- Use 's instead of "s
- When assigning variables use spaces between the `=`s
- Use guard clauses when possible
- When possible use variables and self explanatory code instead of comments
  - Sometimes it maybe necessary to write your pseudo-code before beginning, but if done the unnecessary comments should be removed after the code is done.
  - If you need to use comments have no spaces between comments and code

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

## [When to reuse code](#table-of-contents)
Always be hesitant to re-use code.

It is better to change the same code in multiple places then it is to pass more and more information between the parent and child.

It is better to change the same code in multiple places then it is to completely reorganize your code in order to add a new feature.
  - This is especially important when it comes to re-using separate components/classes.
  - Over time small changes become larger and larger. This creates more and more complexity as the reused component it given more and more information to distinguish between its different roles.