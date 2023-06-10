# Regular Expressions(Regex)
The purpose of a regex is to find character patterns. This can be used to replace them with something or to delete them.

## How to use
- All characters except special character match themselves 
- Special characters: ., +, -, *, ?, ^, $, (, ), [, ], {, }, |, and \

| Sequence  | Description                                                                      |
|-----------|----------------------------------------------------------------------------------|
| \char     | Esxape sequence                                                                  |
| \|        | or                                                                               |
| [...]     | Any character in the brackets                                                    |
| [.-.]     | Range [0-9] is any number, [A-Za-z] is any letter.                               |
| [^...]    | Not in brackets                                                                  |
| char+     | One or more chars                                                                |
| char*     | Zero or more chars                                                               |
| char?     | one or zero                                                                      |
| char{m,n} | m to n inclusive. With m and n being ints.                                       |
| char{m}   | m chars                                                                          |
| char{m,}  | m or more                                                                        |
| .         | Any char except new line                                                         |
| ^char     | Does char start the line                                                         |
| char$     | Does char end the line                                                           |
| \b        | boundary of word. Ex: `\bword\b` would match `word`, but not `words` or `sword`. |
| \<        | start of word                                                                    |
| \>        | end of word                                                                      |
| ()        | back reference or substring                                                      |
| $1        | 1st back reference. $2 for 2nd back reference                                    |
| \d        | Any digit. [0-9]                                                                 |
| \w        | Any word character. [A-Za-z]                                                     |
| \D        | Any non-digit                                                                    |
| \W        | Any non word character                                                           |

## Backus-Naur form grammer(BNF)
Similar to regex in that it is a language to find character patterns.
- BNF is composed of 4 parts
    - terms/variables `<term>`. Recursion is often used.
    - equal symbol `::=`
    - string literals
    - an or symbol `|`

### Examples

```
<number> ::= <digit> | <number> <digit>
<digit>  ::= 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
```

## Command line tools
See [Linux](./linux.md)
- sed
