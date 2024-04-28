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

# Extensible Markup Language(XML)
XML is markup language that allows you to define your own elements in order to be both human readable and machine readable. It is often used to communicate information between systems.

## Table of Contents

<!-- TOC -->

- [Extensible Markup LanguageXML](#extensible-markup-languagexml)
	- [Table of Contents](#table-of-contents)
	- [Rules](#rules)
	- [Comments](#comments)
	- [Attributes](#attributes)
	- [Character References](#character-references)
	- [Prolog](#prolog)
	- [Namespaces](#namespaces)
	- [Vocabularies or Domains](#vocabularies-or-domains)

<!-- /TOC -->

## [Rules](#table-of-contents)
- XML must contain one root element that is the parent of all other elements.
- All elements in XML must have a closing tag
- Tags are case sensitive. `<Letter>` is different from `<letter>`
- Elements must be properly nested.
  - `<b><i>Test</i></b>` and not `<b><i>Test</b></i>`
- Whitespace is preserved

## [Comments](#table-of-contents)
`<!-- Comment -->`

## [Attributes](#table-of-contents)
Attributes are used to provide additional information about your element.
`<element attribute="contents of attribute"></element>`

- The attributes `xmlns` and `id` are used to mean something else.
- Attribute names cannot contain spaces

## [Character References](#table-of-contents)

|        |   |
|--------|---|
| &lt\;   | < |
| &gt\;   | > |
| &amp\;  | & |
| &apos\; | ' |
| &quot\; | " |

## [Prolog](#table-of-contents)
The prolog is used to define the version of XML, the character encoding, and other optional attributes.

The prolog is optional. If it is there it needs to be at the start of the document

`<?xml version="1.0" encoding="UTF-8"?>`

- Or you can add an optional stylesheet which changes how the elements look like.
  - Extendible Stylesheet Language(XSL) is a language to convert XML to other formats such as HTML.
`<?xml-stylesheet type="text/xsl" href="styles.xsl"?>`

## [Namespaces](#table-of-contents)
XML namespaces are used to avoid naming conflict between different elements in different vocabularies or domains.

You can declare a XML namespace like this
```xml
<element xmlns:namespace="http://example.com/namespace">
  <namespace:child>Element from namespace</namespace:child>
</element>
```

- Namespaces can also be applied to attributes for the same reasons

## [Vocabularies or Domains](#table-of-contents)
Vocabularies are different protocols for specific xml element names. For example: HTML or SVGs have their own vocabularies.

Domains are just different domains of information. Just used for categorizing information. For example: You might want to separate information about Science and Math.