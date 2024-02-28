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

[Home](../../README.md)

Not finished

# Neural Networks:

A general purpose algorithm to create functions.

1. Get data which consists of inputs and corresponding outputs.
2. Answer the 5 questions for neural networks.
3. Randomize the weights.
4. Train

## How Neural Networks work:



## The 5 questions for Neural Networks:
	- How many layers?
	- How many neurons per layer?
	- What function should be used to squish the activations between 0 and 1?
		- Sigmoid function/logistic curve
		- Rectified linear unit
	- What function generates the cost/reward/error value?
		- Least squares
	- What function minimizes the cost/reward value by changing the weights?
		- Gradient decent
		- Evolutionary algorithm


## Questions:
	- Does each layer need to have the same number of neurons?
	- How does the algorithm know when to deactivate neurons?
		- You can start out with more neurons and layers then you need and the algorithm can deactivate neurons and layers when it knows it won't be useful.

- The more layers the increased ability to abstract.
- Instead of neurons being on or off when you wiggle a nob it may or may not effect the output. However, if you were to have a gradual on/off when you wiggle a nob it will gradually change the output allowing you to train the neural network better.
	- Wiggle each neuron to see the impact it has on the output
	- Then you do one large backwards calculation to add up all the impacts of the neurons together.
	- Then update all the neurons together
