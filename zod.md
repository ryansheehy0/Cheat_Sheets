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

# Zod
Zod is a typescript validator which checks for types at runtime.

`npm install zod`

When using zod just include `import { z } from 'zod'`

## Table of Contents
<!-- TOC -->

- [Zod](#zod)
	- [Table of Contents](#table-of-contents)
	- [DataTypes](#datatypes)
	- [Coerce](#coerce)
	- [Parsing](#parsing)
	- [Infer](#infer)
	- [String validations](#string-validations)
	- [Number validations](#number-validations)
	- [Objects](#objects)
	- [Arrays](#arrays)

<!-- /TOC -->

## [DataTypes](#table-of-contents)

| Data Types      | Description                                                                              |
|-----------------|------------------------------------------------------------------------------------------|
| .string()       |                                                                                          |
| .number()       |                                                                                          |
| .bigint()       |                                                                                          |
| .boolean()      |                                                                                          |
| .date()         |                                                                                          |
| .literal(value) | Can only be that value                                                                   |
| .symbol()       |                                                                                          |
| .undefined()    |                                                                                          |
| .null()         |                                                                                          |
| .void()         |                                                                                          |
| .any()          |                                                                                          |
| .unknown()      |                                                                                          |
| .never()        |                                                                                          |
| .object()       |                                                                                          |
| .array()        | `z.array(z.string())` or `z.string().array()`                                            |
| .enum(values)   | Unions when values is an array of strings. A tuple when value has `as const` at the end. |
| .function()     |                                                                                          |

You can make types optional by putting `.optional()` on them.

You can make types nullable by putting `.nullable()` on them. This means they can either be null or the type.

You can remove the optional or nullable with `.unwrap()`

```javascript
const stringSchema = z.string()

const optionalString = stringSchema.optional()
optionalString.unwrap() === stringSchema // true

const nullableString = stringSchema.nullable()
nullableString.unwrap() === stringSchema // true
```

## [Coerce](#table-of-contents)
Zod allows input variables to be easily converted to the type.

```javascript
const schema = z.coerce.string()
schema.parse("tuna") // => "tuna"
schema.parse(12) // => "12"
schema.parse(true) // => "true"
```

## [Parsing](#table-of-contents)
Parsing allows you to check if a variable or value of of that type at runtime.

```javascript
// Check at runtime
schema.parse(var)
  // Throws error if wrong
schema.safeParse(var)
  /* returns either
    { success: true
      data: 'billie' }
    or
    { success: false
      error: ZodError }
  */
```

## [Infer](#table-of-contents)
Used to infer the typescript type from a zod schema.

`z.infer<typeof Schema>`

## [String validations](#table-of-contents)
These are used to add some more limitations to strings. `z.string().validation()` or `z.string().transformation()`

| .validation()       | Description                                                                                 |
|---------------------|---------------------------------------------------------------------------------------------|
| .max(#)             | Sets the max length of string                                                               |
| .min(#)             | Sets the min length of string                                                               |
| .length(#)          | A string can only be this length                                                            |
| .email()            |                                                                                             |
| .url()              |                                                                                             |
| .emoji()            |                                                                                             |
| .uuid()             | Universally unique identifier. 128 bit identifier                                           |
| .cuid()             | Collision-resistant Unique identifier. Usually looks like `c<timestamp>C<counter>`          |
| .cuid2()            | Updated version of cuid                                                                     |
| .ulid()             | Universally Unique Lexicographically Sortable Identifier. 128 bits. First 48 are timestamp. |
| .regex(regex)       |                                                                                             |
| .includes(string)   |                                                                                             |
| .startsWith(string) |                                                                                             |
| .endsWith(string)   |                                                                                             |
| .datetime()         | ISO 8601, default is without UTC offset                                                     |
| .ip()               | defaults to IPv4 and IPv6                                                                   |

You can also do some transformation with strings.
- `.tim()`
- `.toLowerCase()`
- `.toUpperCase()`

You can also put error message if the parse fails
`z.string().min(5, { message: "Must be 5 or more characters long" })`

## [Number validations](#table-of-contents)

| .validation()            | Description                                                                |
|--------------------------|----------------------------------------------------------------------------|
| z.number().gt(#)         | Greater than #                                                             |
| z.number().gte(#)        | Greater than or equal to #                                                 |
| z.number().lt(#)         | Less than #                                                                |
| z.number().lte(#)        | Less than or equal to #                                                    |
| z.number().int()         | Integer                                                                    |
| z.number().positive()    | x > 0                                                                      |
| z.number().nonnegative() | x >= 0                                                                     |
| z.number().negative()    | x \< 0                                                                     |
| z.number().nonpositive() | x \<= 0                                                                    |
| z.number().multipleOf(#) | Needs to be evenly divisible by #                                          |
| z.number().finite()      | Not Infinity or -Infinity                                                  |
| z.number().safe()        | This ensures that ints don't go outside the range their memory can handle. |

## [Objects](#table-of-contents)

```javascript
// All properties are required by default
const Dog = z.object({
  name: z.string(),
  age: z.number(),
})
```

| Object methods         | Description                                                                         |
|------------------------|-------------------------------------------------------------------------------------|
| .shape                 | Get the schema of a key                                                             |
| .keyof()               | Get Zod enum of keys of an object                                                   |
| .extend(ObjSchema)     | Used to add additional fields to an object schema. Can be used to overwrite fields. |
| .merge(ObjSchema)      | Combines 2 object schemas. A.extend(B.shape)                                        |
| .pick()/.omit()        | used to keep or remove certain fields.                                              |
| .partial()             | Makes all properties optional                                                       |
| .partial({ key: true}) | Makes just those keys optional                                                      |
| .deepPartial()         | Partials any nested object schemas as well                                          |
| .required()            | Makes all properties required                                                       |
| .passthrough().parse() | Unknown properties aren't stripped, but passed through                              |
| .strict()              | Any unknown keys .parse() with throw error                                          |
| .strip()               | Reset object schema to default behavior when parsing                                |
| .catchall(schema)      | Allows anything of the type schema to pass through                                  |

## [Arrays](#table-of-contents)

| Array methods | Description                         |
|---------------|-------------------------------------|
| .element      | Access the schema of an element     |
| .noempty()    | Doesn't allow the array to be empty |
| .min(#)       |                                     |
| .max(#)       |                                     |
| .length(#)    |                                     |