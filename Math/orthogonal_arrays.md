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

# Orthogonal Arrays

Used to more efficiently optimize a function when you have multiple input variables.

Instead of testing each input on its own, just changing that variable, you can instead test multiple inputs at once and combine their results to effectively give you the same information. Give the same information with much less tests.

Only tells you directly to make changes and doesn't tell you how far.

Ex: A recipe's input is the amount of each ingredient and the time to cook it.

- If you just change one variable at a time you will have to do a lot of experiments in order to test all you variables/inputs.
- 

Rules:
- All inputs must be tested an equal number of times.
- All inputs must be tested against all other tests equally.



I1 = Input 1
I2 = Input 2
I3 = Input 3
O  = Output

| I1 | I2 | I3 | O |
|----|----|----|-|
| 0  | 0  | 0  | 
| 0  | 1  | 1  |
| 1  | 0  | 1  |
| 1  | 1  | 0  |

How can I write a program to generate these tables?
What if the inputs aren't boolean, but analog?
	- You can convert them with break points to boolean.
		- What if I want finer control?
			- You can add more breakpoints and use trinary, quaternary, etc.
How can I write a program to generate these tables with any base inputs?

How do you extract the important information form the output of these tests?
	- Maybe make a simplification where all the inputs have the same base number.

Inputs are trinary.

| I1 | I2 | I3 | I4 |
|----|----|----|----|
| 0  | 0  | 0  | 0  |
| 0  | 1  | 1  | 1  |
| 0  | 2  | 2  | 2  |
| 1  | 0  | 1  | 2  |
| 1  | 1  | 2  | 0  |
| 1  | 2  | 0  | 1  |
| 2  | 0  | 2  | 1  |
| 2  | 1  | 0  | 2  |
| 2  | 2  | 1  | 0  |

- All input need the same base number
- Start with all 0s
- 

Ex: Making the best cookies.
Inputs:
	- Butter
	- Sugar
	- Eggs
	- Flour
	- time to bake at 350F
	
	Base 3
	
	0 1 2
	0 2 1

Algorithm:
- 1st row start with all 0s
- 2nd row increment all other columns by 1 except the 1st column
	- repeat for more rows until you reach the end of your base number
- Increment column 1 by 1. 

1/16 teaspoon of salt, 1/8 tablespoon vanilla extract
Flip at 4 min. Done at 4+3.
Butter:
	0 = 1 tablespoon
	1 = 0.5 tablespoon
	2 = 1.5 tablespoon
Sugar:
	0 = 0.5 tablespoon
	1 = 0.25 tablespoon
	2 = 1 tablespoon
Eggs:
	0 = 0.5 egg
	1 = .25 egg
	2 = .75 egg
Flour:
	0 = 3 tablespoons
	1 = 2.5 tablespoons
	2 = 3.5 tablespoons

| Index | Butter | Sugar | Eggs | Flour | O rob | O ryan | O Ed |
|-------|--------|-------|------|-------|-------|--------|------|
| 1     | 0      | 0     | 0    | 0     |  1     |  1      |   1   |
| 2     | 0      | 1     | 1    | 1     |  1     |   1.75     |  1.5    |
| 3     | 0      | 2     | 2    | 2     |  2     |   2     |   2   |
| 4     | 1      | 0     | 1    | 2     |  2     |    1.5    |   2   |
| 5     | 1      | 1     | 2    | 0     |  1     |    1.75    |  1    |

| 6     | 1      | 2     | 0    | 1     |       |        |      |

| 7     | 2      | 0     | 2    | 1     |       |        |      |
| 8     | 2      | 2     | 1    | 0     |       |        |      |
| 9     | 2      | 1     | 0    | 2     |       |        |      |


