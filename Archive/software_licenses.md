
## [GPLv3 License](#programming-tips)
If you are making your code open source, then it is recommended to use the GPLv3 license in order to prevent other companies from taking your work, adding some feature/modifications, and then selling or distributing their own closed sourced version of your code.
- Why open source is good?
  - Prevent undiscovered bugs. More reliable applications.
  - Allows for anyone to contribute to your project.

### [How to add GPLv3 License](#programming-tips)
1. Include a copy of the license at the root of your project named `COPYING`
2. Add a licensing notice at the top of each of your source code files
  - Make sure to replace "THIS PROGRAM" with the name of your program.

```javascript
/*
 * This file is part of THIS PROGRAM.
 *
 * THIS PROGRAM is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * THIS PROGRAM is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with THIS PROGRAM. If not, see <https://www.gnu.org/licenses/>.
 */
```

3. Add `THIS PROGRAM is licensed under GPLv3. See the COPYING file for details.` to your README.md under `## License`
4. Include a copy of the license with the distribution of your software.