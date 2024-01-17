[Home](./README.md)

# Regular Expressions(Regex)
The purpose of a regex is to find character patterns. It stands for regular expression. This can be used to replace them with something or to delete them.

You can test regexes at this [site](https://regex101.com/).

## Table of Contents

<!-- TOC -->

- [Regular ExpressionsRegex](#regular-expressionsregex)
  - [Table of Contents](#table-of-contents)
  - [Regex Components](#regex-components)
    - [Anchors](#anchors)
      - [Examples](#examples)
    - [Quantifiers](#quantifiers)
      - [Examples](#examples)
    - [OR Operator](#or-operator)
      - [Examples](#examples)
    - [Character Classes](#character-classes)
      - [Examples](#examples)
    - [Bracket Expressions](#bracket-expressions)
      - [Examples](#examples)
    - [Flags](#flags)
    - [Grouping and Capturing](#grouping-and-capturing)
      - [Back-references](#back-references)
      - [Examples](#examples)
    - [Greedy and Lazy Match](#greedy-and-lazy-match)
    - [Boundaries](#boundaries)
      - [Examples](#examples)
    - [Look-ahead and Look-behind](#look-ahead-and-look-behind)
      - [Examples](#examples)
    - [Metacharacters](#metacharacters)
  - [Regex Examples](#regex-examples)
  - [Backus-Naur form grammerBNF](#backus-naur-form-grammerbnf)
    - [Examples](#examples)
  - [Command line tools](#command-line-tools)

<!-- /TOC -->

## [Regex Components](#table-of-contents)
- All characters, except special character, match themselves
  - Special characters: ., +, -, *, ?, ^, $, (, ), [, ], {, }, \|, \\, and [metacharacters](#metacharacters)
  - In general you can use \s to escape special characters.

### [Anchors](#table-of-contents)
Anchors are special characters that match with position instead of matching the actual character.

| Example | Description                                         |
|---------|-----------------------------------------------------|
| ^string | Selects "string" if it is the start of the line     |
| string$ | Selects "string" if it start at the end of the line |

#### [Examples](#table-of-contents)
- "^abc$" selects
  - Only lines that are entirely composed of "abc"

### [Quantifiers](#table-of-contents)
Quantifiers decide how many times a character can occur for it to be selected.

| Example | Description                                                                   |
|---------|-------------------------------------------------------------------------------|
| a+      | Selects "a" one or more times.                                                |
| a*      | Selects "a" zero or more times, including an empty string if no "a" is found. |
| a?      | Selects "a" one or zero times, including an empty string if no "a" is found.  |
| a{X}    | Selects X number of "a"s                                                      |
| a{X,Y}  | Selects X to Y "a"s                                                           |
| a{X,}   | Selects at least X number of "a"s                                             |

#### [Examples](#table-of-contents)
- "a+" will select
  - "aaa" as one selection in the line "aaa"
  - the 3 "a"s will be selected in the line "ababab"
  - nothing will be selected in the line "b"
- "a*" will select
  - "aa", "" between "a" and "b", and "" at the end in the line "aab"
- "a?" will select
  - "a", "a", "" between "a" and "b", and "" at the end in the line "aab"

### [OR Operator](#table-of-contents)
The or operator "\|" allows you to select one pattern or another.

#### [Examples](#table-of-contents)
- "cat\|dog" will select
  - "dog" and "cat" in the line "dogabccat"

### [Character Classes](#table-of-contents)
Character classes are used to match or not match what is in the "[]"s

Character classes are often used with [quantifiers](#quantifiers) to allow quantifiers to be applied to multiple characters.

| Example | Description                                |
|---------|--------------------------------------------|
| [abc]   | Selects "a", "b", or "c".                  |
| [^abc]  | Selects everything except "a", "b", or "c" |

#### [Examples](#table-of-contents)
- "[abc]" will select
  - "a", "b", and "c" in the line "abc"

### [Bracket Expressions](#table-of-contents)
Bracket expressions are used to find a range of characters using []s

| Example | Description                                |
|---------|--------------------------------------------|
| [0-9]   | Find any digit                             |
| [a-z]   | Find any lower case characters             |
| [A-Z]   | Find any upper case characters             |

#### [Examples](#table-of-contents)
- "[a-c]" will select
  - All "a"s, "b"s, and "c"s

### [Flags](#table-of-contents)
Flags are optional settings put after the regex to change certain matching behavior.

| Flag symbol | Description                                                                           |
|-------------|---------------------------------------------------------------------------------------|
| g           | global. Allows for multiple matches rather than just the first occurrence.            |
| m           | multi line. ^ and $ match to each line instead of the whole input string.             |
| i           | case insensitivity. "abc" is treated the same as "ABC"                                |
| x           | ignores whitespace within the regex                                                   |
| s           | Allows the dot "." to match newline characters                                        |
| u           | Used to match with full unicode. This is useful when working outside the ASCII range. |

### [Grouping and Capturing](#table-of-contents)
Capturing groups allow you to create references which can be used later on.

| Example | Description                                               |
|---------|-----------------------------------------------------------|
| (abc)   | This captures the group "abc" and can be referenced later |
| (?:abc) | This creates a group, but is not added to the references  |

#### [Back-references](#table-of-contents)
To reference a capturing group you can do so with \1, \2, \3, etc.

#### [Examples](#table-of-contents)
- "(ab)+" will select
  - "ababab" in the line "ababab"
- "(abc)\1" will select
  - "abcabc" in the line "abcabc"

### [Greedy and Lazy Match](#table-of-contents)
Quantifiers are greedy by default, meaning they match as much as they can. Adding ? after the quantifier makes it lazy, meaning it matches as little as possible.

| Example | Description                                      |
|---------|--------------------------------------------------|
| a+?     | Selects "a" only one time instead of one or more |

### [Boundaries](#table-of-contents)
Boundaries allow you to find strings at the begging of words or at the end of words.

| Example  | Description                                 |
|----------|---------------------------------------------|
| \bstring | Find "string" if it at the begging of words |
| string\b | Find "string" if it at the end of words     |

#### [Examples](#table-of-contents)
- "\babc" will select
  - the 1st "abc" and the last "abc" in the line "abc anotherabc word abc"
- "abc\b" will select
  - the middle "abc" in the line "abc anotherabc word abc"
- "\bword\b" will select
  - only "word" in the line "word words sword"

### [Look-ahead and Look-behind](#table-of-contents)
Used to see if a pattern matches ahead or behind the current position without changing the position.

| Example     | Description                                                                                     |
|-------------|-------------------------------------------------------------------------------------------------|
| abc(?=def)  | Selects "abc" only if it is followed by another "def", but doesn't match the following "def"    |
| abc(?!def)  | Select "abc" only if it is not followed by another "def", but doesn't match the following "def" |
| (?<=def)abc | Select "abc" only if it is in front of "def", but doesn't match the "def"                       |
| (?<!def)abc | Select "abc" only if it is not in front of "def", but doesn't match the "def"                   |

#### [Examples](#table-of-contents)
- "\d(?=\D)" will select
  - only a digital character followed by a non-digital character

### [Metacharacters](#table-of-contents)
Special characters with specific meanings.

| Metacharacters | Description                                                                       |
|----------------|-----------------------------------------------------------------------------------|
| .              | Find any single character except new line                                         |
| .*             | Find any character 0 or more. Useful for selecting everything in front or behind. |
| \w             | Find a lower case, upper case, or digit.                                          |
| \W             | Find anything that isn't lower case, upper case, or digit.                        |
| \d             | Find any digit                                                                    |
| \D             | Find any non-digit character                                                      |
| \s             | Find a whitespace character                                                       |
| \S             | Find any non-whitespace character                                                 |
| \0             | Find null character                                                               |
| \n             | Find new line character                                                           |
| \f             | Find form feed character                                                          |
| \r             | Find carriage return character                                                    |
| \t             | Find tab character                                                                |
| \v             | Find vertical tab character                                                       |
| \ddd           | Find the octal number with ddd                                                    |
| \xYY           | Find a hexadecimal number with YY                                                 |
| \uYYYY         | Find the unicode character with the hex number nnnn                               |

## [Regex Examples](#table-of-contents)

| What it's matching | Regex                                                            |
|--------------------|------------------------------------------------------------------|
| Hex value          | /^#?([a-f0-9]{6}\|[a-f0-9]{3})$/                                 |
| Email              | /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/                |
| URL                | /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/ |
| HTML Tag           | /^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>\|\s+\/>)$/                     |
| HTML Comment       | /<!--.*?-->/                                                     |
| Phone number       | /^\d{3}-\d{3}-\d{4}/                                             |

## [Backus-Naur form grammer(BNF)](#table-of-contents)
Similar to regex in that it is a language to find character patterns.
- BNF is composed of 4 parts
    - terms/variables `<term>`. Recursion is often used.
    - equal symbol `::=`
    - string literals
    - an or symbol `|`

### [Examples](#table-of-contents)

```
<number> ::= <digit> | <number> <digit>
<digit>  ::= 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
```

## [Command line tools](#table-of-contents)
See [Linux](./linux.md)
- sed