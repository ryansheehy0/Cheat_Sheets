[Home](./README.md)

# Zod
Zod is a typescript validator which checks for types at runtime.

`npm install zod`

When using zod just include `import { z } from 'zod'`

## Table of Contents
<!-- TOC -->

- [Zod](#zod)
  - [Table of Contents](#table-of-contents)
  - [Coerce](#coerce)
  - [Parsing](#parsing)
  - [String validations](#string-validations)

<!-- /TOC -->

```javascript
// primitive values
z.string()
z.number()
z.bigint()
z.boolean()
z.date()
z.symbol()

// empty types
z.undefined()
z.null()
z.void() // accepts undefined

// catch-all types
// allows any value
z.any()
z.unknown()

// never type
// allows no values
z.never()


z.object()
  .optional()

// Convert to typescript type
type Type = z.infer<typeof schema>
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
  // returns invalid object when wrong
```

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
