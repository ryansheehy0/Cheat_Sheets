[Home](./README.md)

# Typescript
Typescript is a developer tool to make it easier to write javascript.
- Instead of errors showing up when you run the code it shows up when you are typing javascript. This is done through type safety.
- Helps populate methods for code completion

Use .ts or .tsx files

Typescript gets compiled into javascript.

`let variableName: type = value`

## Table of Contents
<!-- TOC -->

- [Typescript](#typescript)
  - [Table of Contents](#table-of-contents)
  - [Installation](#installation)
  - [Basic Types](#basic-types)

<!-- /TOC -->

## [Installation](#table-of-contents)
`sudo npm install -g typescript`
- Use `tsc typescriptFile.ts` to compile typescript files into javascript.

## [Basic Types](#table-of-contents)
- number
- string
- boolean
- null
  - Absence of a value.
  - This can only be set manually and javascript doesn't automatically create something as null. This means that when you see a null it explicitly says there there is no value here.
- undefined
  - Value which has not been assigned yet.
- arrays
- tuples
  - An array of fixed length where each element can have different types
- objects
- enums
- union types
  - Can be several types
  - `let variable: null | number`
- any
- void
  - function don't return any value
```typescript
function func(): void {
  console.log("func")
}
```

type keyword?
?:
Props
Casting using as