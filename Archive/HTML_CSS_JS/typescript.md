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

[Home](../README.md)

# Typescript
Typescript is a developer tool to make it easier to write javascript.
- Instead of errors showing up when you run the code it shows up when you are typing javascript. This is done through type safety.
- Helps populate methods for code completion

Use .ts or .tsx files

Typescript gets compiled into javascript.

`let variableName: type = value`

<!-- TOC -->

- [Installation](#installation)
- [Basic Types](#basic-types)
	- [Literal Types](#literal-types)
	- [Special function return types](#special-function-return-types)
	- [DOM types](#dom-types)
- [Type Aliases](#type-aliases)
	- [Intersection Types](#intersection-types)
- [Casting](#casting)
	- [Non-null assertion](#non-null-assertion)
	- [as const](#as-const)
- [Interfaces](#interfaces)
	- [Declaration merging](#declaration-merging)
	- [Extending interfaces](#extending-interfaces)
	- [Arrays](#arrays)
- [Advanced typing](#advanced-typing)
	- [Index signatures](#index-signatures)
	- [Mapped types](#mapped-types)
	- [Conditional Types](#conditional-types)
	- [Generics](#generics)
	- [lookup types](#lookup-types)
	- [keyof](#keyof)
- [Utility Types](#utility-types)
	- [Mapped Types](#mapped-types)
- [Use instead of enums](#use-instead-of-enums)
- [Type guards](#type-guards)
	- [typeof as a guard](#typeof-as-a-guard)
	- [in](#in)
	- [instanceof](#instanceof)
	- [Type Guard function](#type-guard-function)
- [React](#react)
- [Need to understand these syntaxes](#need-to-understand-these-syntaxes)
- [Phantom Types](#phantom-types)

<!-- /TOC -->

## [Installation](#typescript)
`sudo npm install -g typescript`
- Use `tsc typescriptFile.ts` to compile typescript files into javascript.

## [Basic Types](#typescript)
- number
- string
- boolean
- null
  - Manually set an absence of a value.
  - This can only be set manually and javascript doesn't automatically create something as null. This means that when you see a null it explicitly says there there is no value here.
- undefined
  - Value which has not been assigned yet.
- arrays
  - `let array: number[]`
  - Array of array `let 2dArray: number[][]`
  - You can also do `let array: Array<number>`
  - You can also have an array of unions. `let array: (number | string)[]`
- tuples
  - An array of fixed length where each element can have different types. The order of the data maters.
  - `let tuple: [number, string, boolean]`
  - Note: Tuples still allow for `.push()` and other such function which brake tuple.
- objects

```typescript
let object: {firstName: string, lastName: string} = {
  firstName: "Ryan",
  lastName: "Sheehy"
}
```

- enums
  - It is recommended to never use enums and instead use arrays.
- union types
  - Can be several types
  - `let variable: null | number`
- any
  - If typescript cannot infer the type it puts it as any. It is recommended to not use any in any circumstance.
- unknown
  - functions who return values whose type isn't known until compile time

When initializing variables and assigning them on the same line typescript automatically can infer the type. There is no need to explicitly put the type.

```typescript
let variable: number = 10
// This is the same as
let variable = 10
```

### [Literal Types](#typescript)
Literal types allow you to set a type to only be certain predefined values.

```typescript
let variable: "Name" | "Username" | "Email"
```

### [Special function return types](#typescript)
- void
  - function don't return any value

```typescript
function func(): void {
  console.log("func")
  return
}
```

- never
  - functions which never return anything

```typescript
function func(): never {
  console.log("func")
}
```

### [DOM types](#typescript)

## [Type Aliases](#typescript)
Used to define a type which you can use again and again.

```typescript
// defining object type aliases
type User = {
  name: string
  email: string
  isActive: boolean
  readonly _id: string
  credCardDetails?: number // ? means that it's optional
}

// You can also defined type aliases for union types
type UserRole = "User" | "Admin" | "Staff"

function (user: User): User{
  return user
}
```

### [Intersection Types](#typescript)
Intersection types allows you to combine different types together.

```typescript
type cardNumber = {
  cardNumber: string
}

type cardDate = {
  cardDate: string
}

type cardDetails = cardNumber & cardDate
```

## [Casting](#typescript)
I typescript you can cast between types using the `as` keyword. This is useful when you know more about the variable type than typescript does.

```typescript
let variable: any = "Hello, TypeScript!"
let length: number = (variable as string).length

// This is the old syntax
let length: number = (<string>variable).length
```

### [Non-null assertion](#typescript)
`!.` is used when you know that a variable isn't null or undefined.

```typescript
let id: string = element!.id
// This means you know that the id field of element will always have a value

// You can also use it if you know a variable isn't null
type ID = number | null
let id = 10
console.log(id!) // This tells typescript that id isn't null
```

### [as const](#typescript)

## [Interfaces](#typescript)
Type alias are very similar to interfaces and it is almost always recommended to use type aliases.

Use interfaces if you want to use declaration merging.

Interfaces can only describe objects.

### [Declaration merging](#typescript)
Declaration merging is having an interface with the same name which adds onto an interface.

```typescript
interface ButtonProps {
  text: string
  onClick: () => void
}
interface ButtonProps {
  id: string
}

const button: ButtonProps = {
  text: "button text",
  onClick(){
    console.log("Button was clicked")
  },
  id: "abc"
}
```

### [Extending interfaces](#typescript)
Extending interfaces allows you to extend an interface with another interface. This is like declaration merging, but with interfaces with different names.

```typescript
interface ButtonProps {
  text: string
  onClick: () => void
}

interface MoreButtonProps extends ButtonProps{
  id: string
}

const button: MoreButtonProps = {
  text: "button text",
  onClick(){
    console.log("Button was clicked")
  },
  id: "abc"
}
```

### [Arrays](#typescript)

```typescript
interface Names {
  [index: number]: string
}

// This is the same as
type Names: string[]
```

## [Advanced typing](#typescript)

### [Index signatures](#typescript)
Index signatures allow you to define a type for the properties in an object or array when you don't know their names.

```typescript
type NumberIndexedAlias = {
  [index: number]: string
  // Forces the keys to be numbers
}

// Create an object that matches the type alias
let myObjectAlias: NumberIndexedAlias = {
  0: 'Zero',
  1: 'One',
  2: 'Two',
}
```

You can also use `[number]` to go through each of the elements in an array.

```typescript
type MyArray = [string, string, number]

type ObjArray = {
   [index: string]: typeof MyArray[number]// Gets each type from the tuple
}
```

### [Mapped types](#typescript)

```typescript
type Flags = {
  option1: boolean;
  option2: boolean;
};

type ReadonlyFlags = {
  readonly [K in keyof Flags]: boolean;
};
```

### [Conditional Types](#typescript)
Conditional types allows you to create a type based upon other types.

`T extends U ? X : Y`

`extends` returns a boolean if type `T` is a subtype of type `U`

Examples:

```typescript
// Example 1
type CheckNumber<T> = T extends number ? 'Is a number' : 'Not a number'
type Result1 = CheckNumber<42>        // 'Is a number'
type Result2 = CheckNumber<'hello'>   // 'Not a number'
```

### [Generics](#typescript)
Generics are used for when the exact type is not known beforehand and you want the user to be able to specify the type dynamically.

`T` is the convention for when you want to use a generic type, but generic types can be any name.

```typescript
type MyGenericType<T> = {
  data: T
}

type Example1: MyGenericType<number>
const example1Obj: Example1 = {
  data: 10
}

type Example2: MyGenericType<string>
const example2Obj: Example2 = {
  data: "ten"
}
```

### [lookup types](#typescript)
Lookup types are used ot get the type of a field in an object type.

```typescript
type Point = {
  x: number
  y: number
}

type x = Point.x
type y = Point.["y"]
```

### [keyof](#typescript)
`keyof objType` is used to get the keys of an obj type as a union of strings

```typescript
type MyKeys = keyof { name: string; age: number }; // MyKeys is "name" | "age"
```

## [Utility Types](#typescript)
Utility types allow you to apply certain transformations or combinations on object types to produce other types.

| Type name                           | Description                                                                                               |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------|
| Awaited<T>                          |                                                                                                           |
| Partial<T>                          | Create a type from an obj type and make all the fields optional.                                          |
| Required<Type>                      | Create a type from an obj type and make all the fields required. Removes the ?s                           |
| Readonly<Type>                      | Creates a type from an obj type and make all the fields readonly                                          |
| Record<Keys, Type>                  | Converts a union of literal types to an obj type and defines their type to be Type                        |
| Pick<Type, Keys>                    | Creates a new obj type by selecting properties from the original obj type(Type)                           |
| Omit<Type, Keys>                    | Like the opposite of Pick. omits properties from the original obj type.                                   |
| Exclude<UnionType, ExcludedMembers> | Excludes some values from a union type.                                                                   |
| Extract<Type, Union>                | Extracts only the type literals of Type from a union type                                                 |
| NonNullable<UnionType>              | Removes the null and/or undefined from union types.                                                       |
| Parameters<FunctionType>            | Takes the parameter types from a function and converts them to a type of tuple.                           |
| ConstructorParameters<ClassType>    | Takes the parameter types from a class and convert them to a type of tuple.                               |
| ReturnType<FunctionType>            | Gets the return type of a function type                                                                   |
| InstanceType<ClassType>             | Takes in a class type and return the object type that that class would produce.                           |
| ThisParameterType<FunctionType>     | Extracts the `this` type from a function type.                                                            |
| OmitThisParameter<FunctionType>     | Removes the this parameter from a function type.                                                          |
| ThisType<ObjectType>                | Defines the type of this inside methods in the object type. ThisParameterType<Each method in object type> |

Examples:
- Record<Keys, Type>

```typescript
type Fruit = "apple" | "banana" | "orange"
type FruitCounts = Record<Fruit, number>
const fruitCounts: FruitCounts = {
  apple: 5,
  banana: 10,
  orange: 5
}
```

- Pick<Type, Keys>

```typescript
type Person = {
  name: string
  age: number
  address: string
}

type PersonSummary = Pick<Person, "name" | "age">
const personSummary: PersonSummary = {
  name: "John",
  age: 25
}
```

- Exclude<UnionType, ExcludedMembers>

```typescript
type Fruits = "apple" | "banana" | "orange"
type RoundFruits = Exclude<Fruits, "banana"> // "apple" | "orange"
```

- Extract<Type, Union>

```typescript
type One = "one" | 1 | "uno"
type StringOnes = Extract<string, One>
```

### [Mapped Types](#typescript)
Mapped types allow you to create your own utility types.

The syntax is `[Key in UnionType]`. They key loops through all the values in the union type.

```typescript
type Point = {
  x: number
  y: number
}

// A mapped type that is Readonly
type ReadonlyPoint = {
  readonly [Key in "x" | "y"]: number
  // Same as
    // readonly "x": number
    // readonly "y": number
}
```

- Often times the mapped type is used with the `keyof` operator to get a union of keys from an Object Type. Like `[K in keyof ObjType]`.
- Often times you can use the Key as a lookup type. Like `[K in "a" | "b" | "c" ]: ObjType[K]`. This sets the keys to be the same time as `ObjType[Key]`.

## [Use instead of enums](#typescript)
Enums have some weird behaviors which may cause some issues. Instead you can use these alternatives instead.

```typescript
type UserRole = "User" | "Admin" | "Staff"

// If you need to iterate over the items in your list use this
const UserRoles = ["User", "Admin", "Staff"]
type UserRole = typeof UserRoles[number]

// If you want something more advanced
const UserRoles = {
  User: "User",
  Admin: "Admin",
  Staff: "Staff"
} as const
type UserRole = keyof typeof UserRoles

function logRole(role: UserRole): never{
  console.log(`The user's role is: ${UserRoles[role]}`)
}
```

## [Type guards](#typescript)
Type guards are used to ensure that a variable is a certain type.


### [typeof as a guard](#typescript)
Gets the type of a variable as a string.

```typescript
let x = 10
if(typeof x === "number"){
  // x is a number
}
```

### [in](#typescript)
Checks if a field exists in an object.

```typescript
let obj = { prop: "value" }
if("prop" in obj){
  // prop is in obj
}
```

### [instanceof](#typescript)
Check if an object is an instance of a class.

```typescript
class MyClass {}
let obj = new MyClass()
if(obj instanceof MyClass){
  // obj is an instance of MyClass
}
```

### [Type Guard function](#typescript)
A type guard function is used to check if a value is a certain type at runtime.

A type guard function returns a type predicate, which takes the form of `parameterName is Type`

The `is` keyword is used, instead of a boolean, to let typescript know what the type is after the function is called.

```typescript
function isStringOfLength<Min extends number, Max extends number>(str: string, min: Min, max: Max): str is StringOfLength<Min, Max> {
  return str.length >= min && str.length <= max
}
```

```typescript
function isString(value: any): value is string{
  return typeof value === "string"
}

let x = "hello"
if(isString(x)){
  // typescript knows x is a string
}
```

## [React](#typescript)

```javascript
import React, { ReactNode } from 'react'

type ComponentProps = {
  children: ReactNode
}

const Component: React.FC<ComponentProps> = ({}) => {
}

// Or no Props
const Component: React.FC = () => {
}

export default Component
```


## Need to understand these syntaxes

```typescript
type Pick<Type, Keys extends keyof Type> = {
  [K in Keys]: Type[K];
};

// extends is being used as a Type parameter constraint

type Exclude<UnionType, ExcludedMembers> = UnionType extends ExcludedMembers
  ? never
  : UnionType;

type Parameters<Type extends (...args: any[]) => any> = Type extends (...args: infer P) => any ? P : never;
```

- infer

## [Phantom Types](#typescript)
