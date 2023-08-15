[Home](./README.md)

# Extensible Markup Language(XML)
XML is markup language that allows you to define your own elements in order to be both human readable and machine readable. It is often used to communicate information between systems.

## Rules
- XML must contain one root element that is the parent of all other elements.
- All elements in XML must have a closing tag
- Tags are case sensitive. `<Letter>` is different from `<letter>`

## Prolog
The prolog is used to define the version of XML, the character encoding, and other optional attributes.

The prolog is optional. If it is there it needs to be at the start of the document

`<?xml version="1.0" encoding="UTF-8"?>`

- Or you can add an optional stylesheet which changes how the elements look like.
  - Extendible Stylesheet Language(XSL) is a language to convert XML to other formats such as HTML.
`<?xml-stylesheet type="text/xsl" href="styles.xsl"?>`

## Namespaces