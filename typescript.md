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
    - [Indexing with number](#indexing-with-number)
    - [Mapped types](#mapped-types)
    - [Conditional Types](#conditional-types)
    - [Generics](#generics)
    - [lookup types](#lookup-types)
    - [keyof](#keyof)
  - [Utility Types](#utility-types)
  - [Use instead of enums](#use-instead-of-enums)
  - [Type guards](#type-guards)
    - [typeof as a guard](#typeof-as-a-guard)
    - [in](#in)
    - [instanceof](#instanceof)
    - [Guard function](#guard-function)
  - [Need to understand these syntaxes](#need-to-understand-these-syntaxes)

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

### [Literal Types](#table-of-contents)
Literal types allow you to set a type to only be certain predefined values.

```typescript
let variable: "Name" | "Username" | "Email"
```

### [Special function return types](#table-of-contents)
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

### [DOM types](#table-of-contents)

## [Type Aliases](#table-of-contents)
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

### [Intersection Types](#table-of-contents)
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

## [Casting](#table-of-contents)
I typescript you can cast between types using the `as` keyword. This is useful when you know more about the variable type than typescript does.

```typescript
let variable: any = "Hello, TypeScript!"
let length: number = (variable as string).length

// This is the old syntax
let length: number = (<string>variable).length
```

### [Non-null assertion](#table-of-contents)
`!.` is used when you know that a variable isn't null or undefined.

```typescript
let id: string = element!.id
// This means you know that the id field of element will always have a value
```

### [as const](#table-of-contents)

## [Interfaces](#table-of-contents)
Type alias are very similar to interfaces and it is almost always recommended to use type aliases.

Use interfaces if you want to use declaration merging.

Interfaces can only describe objects.

### [Declaration merging](#table-of-contents)
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

### [Extending interfaces](#table-of-contents)
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

### [Arrays](#table-of-contents)

```typescript
interface Names {
  [index: number]: string
}

// This is the same as
type Names: string[]
```

## [Advanced typing](#table-of-contents)

### [Indexing with number](#table-of-contents)
[number]

### [Mapped types](#table-of-contents)

```typescript
type Flags = {
  option1: boolean;
  option2: boolean;
};

type ReadonlyFlags = {
  readonly [K in keyof Flags]: boolean;
};
```

### [Conditional Types](#table-of-contents)
`T extends U ? X : Y`

### [Generics](#table-of-contents)
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


### [lookup types](#table-of-contents)
Lookup types are used ot get the type of a field in an object type.

```typescript
type Point = {
  x: number
  y: number
}

type x = Point.x
type y = Point.["y"]
```

### [keyof](#table-of-contents)
`keyof objType` is used to get the keys of an obj type as a union of strings

```typescript
type MyKeys = keyof { name: string; age: number }; // MyKeys is "name" | "age"
```

## [Utility Types](#table-of-contents)
Utility types allow you to apply certain transformations or combinations on object types to produce other types.

| Type name                           | Description                                                                        |
|-------------------------------------|------------------------------------------------------------------------------------|
| Awaited<T>                          |                                                                                    |
| Partial<T>                          | Create a type from an obj type and make all the fields optional.                   |
| Required<Type>                      | Create a type from an obj type and make all the fields required. Removes the ?s    |
| Readonly<Type>                      | Creates a type from an obj type and make all the fields readonly                   |
| Record<Keys, Type>                  | Converts a union of literal types to an obj type and defines their type to be Type |
| Pick<Type, Keys>                    | Creates a new obj type by selecting properties from the original obj type(Type)    |
| Omit<Type, Keys>                    | Like the opposite of Pick. omits properties from the original obj type.            |
| Exclude<UnionType, ExcludedMembers> | Excludes some values from a union type.                                            |
| Extract<Type, Union>                | Extracts only the type literals of Type from a union type                          |
| NonNullable<UnionType>              | Removes the null and/or undefined from union types.                                |
| Parameters<FunctionType>            | Takes the parameter types from a function and converts them to a type of tuple.    |
| ConstructorParameters<ClassType>    | Takes the parameter types from a class and convert them to a type of tuple.        |
| ReturnType<FunctionType>                    | Gets the return type of a function type                                                                                    |
| InstanceType<Type>                  |                                                                                    |
| ThisParameterType<Type>             |                                                                                    |
| OmitThisParameter<Type>             |                                                                                    |
| ThisType<Type>                      |                                                                                    |
| ReturnType<Type>                    |                                                                                    |

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

## [Use instead of enums](#table-of-contents)
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

## [Type guards](#table-of-contents)
Type guards are used to ensure that a variable is a certain type.


### [typeof as a guard](#table-of-contents)
Gets the type of a variable as a string.

```typescript
let x = 10
if(typeof x === "number"){
  // x is a number
}
```

### [in](#table-of-contents)
Checks if a field exists in an object.

```typescript
let obj = { prop: "value" }
if("prop" in obj){
  // prop is in obj
}
```

### [instanceof](#table-of-contents)
Check if an object is an instance of a class.

```typescript
class MyClass {}
let obj = new MyClass()
if(obj instanceof MyClass){
  // obj is an instance of MyClass
}
```

### [Guard function](#table-of-contents)
Guard functions are functions that manually check if a value is of a certain type. This uses the `is` keyword.

The reasons you use `is` instead of just returning a boolean is to let typescript now what the type is after the function is called.

```typescript
function isString(value: any): value is string{
  return typeof value === "string"
}

let x = "hello"
if(isString(x)){
  // typescript knows x is a string
}
```

## Need to understand these syntaxes

```typescript
type Pick<Type, Keys extends keyof Type> = {
  [K in Keys]: Type[K];
};

type Exclude<UnionType, ExcludedMembers> = UnionType extends ExcludedMembers
  ? never
  : UnionType;

type Parameters<Type extends (...args: any[]) => any> = Type extends (...args: infer P) => any ? P : never;
```
