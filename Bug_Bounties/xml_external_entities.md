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

# XML external entity injection(XXE)

XXEs are where an attacker sends a modified XML request to the server which allows the attacker to perform their attacks. Most often this attack would be SSRFs.

## Terms:
- **Document Type Definitions(DTDs)** are a set of rules which defines the legal elements for XML. DTDs are defined using the `DOCTYPE` element. An XML can only have 1 DTD and it's set at the top.
- **Entities** are ways to define reusable content in XML. These are defined in the DTD.
	- **General entities** are like variables.
	- **Parameter entities** are entities which can take in other entities. These can only be used inside the DTD.
		- Ex: `<!ENTITY % outer "<!ENTITY inner 'John'>">` This is used to call that parameter entity. `%outer;`
	- **Predefined entities** are entities that are already defined and are used to display special characters, `<>"'&` inside XML elements.

| Character | Entity   | Unicode |
|-----------|----------|---------|
| `<`       | `&lt;`   | `&#x3C` |
| `>`       | `&gt;`   | `&#x3E` |
| `&`       | `&amp;`  | `&#x26` |
| `"`       | `&quot;` | `&#x22` |
| `'`       | `&apos;` | `&#x27` |

- **External entities** are entities that are loaded outside of the DTD. These could be other files or URLs.
	- Ex: `<!ENTITY subscribe SYSTEM "file.txt">`
- **External DTDs** are DTDs loaded outside of the main XML document.
	- Ex: `<!DOCTYPE dtd SYSTEM "external.dtd">`

## XML Ex:

```xml
<?xml version="1.0"?>
<!DOCTYPE Person [
	<!ENTITY name "John">
]>
<Person>
	<Name>&name;</Name>
	<Age>20</Age>
</Person>
```

## Types of XXEs
- Inband
	- Output of the parsed XML is shown
- Error
	- Only get to see the errors from the XML parser
- Out-of-band(OOB)
	- Don't see any output whatsoever. Have to use an out-of-band request, messages sent to attacker's server, to see the data.

Different types of XXE attacks:
- Retrieving files
- SSRF attacks
- bling XXE exfiltrate data out of band
	- Sensitive data is transmitted form server to attacker
	- How is this different from retrieving files?
- blind XXE to retrieve data via error messages

### Inband
- Add or edit the DTD to define an external entity which contains the file path.
- Edit a XML element, which shows in the response, to make use of the newly defined external entity.
	- Often times there is a lot of trial and error to know what XML entities effect the output.

Ex:
Request before the attack
```xml
<?xml version="1.0" encoding="UTF-8"?>
<stockCheck><productId>381</productId></stockCheck>
```

Request after the attack
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [
	<!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<stockCheck><productId>&xxe;</productId></stockCheck>
```

What if the DTD is loaded from a URL. How can You then add your own entities?