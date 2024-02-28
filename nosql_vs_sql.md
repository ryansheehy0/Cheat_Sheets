<!--
 * This file is part of RS Cheat Sheets.
 *
 * RS Cheat Sheets is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * RS Cheat Sheets is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with RS Cheat Sheets. If not, see <https://www.gnu.org/licenses/>.
 */
-->

[Home](./README.md)

# NoSQL vs SQL

This will be coving the styles of NoSQL and SQL databases and not any particular databases or querying languages.

## Table of Contents
<!-- TOC -->

- [NoSQL vs SQL](#nosql-vs-sql)
	- [Table of Contents](#table-of-contents)
	- [Deep vs Broad](#deep-vs-broad)
	- [Reading](#reading)
- [For heavily nested data it is easier to do CRUD operations with NoSQL](#for-heavily-nested-data-it-is-easier-to-do-crud-operations-with-nosql)

<!-- /TOC -->

## Deep vs Broad
Deep databases are ones that have a lot of 

```typescript
// NoSQL
type Card = {
  id: number
  name: string
  cards: Card[]
}

type List = {
  id: number
  name: string
  cards: Card[]
}

type Board = {
  id: number
  name: string
  lists: List[]
}

// SQL
type Card = {
  itemId: List.id
  id: number
  name: string
  cards: number[]
}

type List = {
  boardId: Board.id
  id: number
  name: string
  cards: Card.id[]
}

type Board = {
  id: number
  name: string
  lists: number[]
}
```

## Reading

```javascript
// NoSQL
// Board
const board = db.boards.get(boardId)

// List
let list
board.lists.forEach((tempList) => {
  if(tempList.id === listId){
    list = tempList
  }
})

// Card
let card
list.forEach((tempCard) => {
  if(tempCard.id === cardId){
    card = tempCard
  }
})

// Card in a card

```

# For heavily nested data it is easier to do CRUD operations with NoSQL