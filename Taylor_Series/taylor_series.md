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

# Taylor Series

Taking non polynomial functions and finding polynomials which approximate the function near some value of $x$.

## Equation:
Polynomials: $ax^0 + bx^1 + cx^2 + ...$

$f(x)$ $=$ function wanting to approximate

$p(x)$ $=$ polynomial that approximates $f(x)$

$p(x) = f(a) + \frac{df(a)}{dx} \frac{(x-a)}{1!} + \frac{d^2f(a)}{dx^2} \frac{(x-a)^2}{2!} + ... = \frac{d^nf(a)}{dx^n} \frac{(x-a)^n}{n!} + ...$

- If $x$ lies within the radius of convergence for $f(x)$ and $a$, then the more terms added to $p(x)$ the more accurate the approximation.

## Example:

$\qquad f(x)=cos(x)$ approximate at $a = 0$

$\qquad \frac{df}{dx} = -sin(x) \qquad \frac{d^2f}{dx^2} = -cos(x) \qquad \frac{d^3f}{dx^3} = sin(x)$

$\qquad f(0) = 1 \qquad \frac{df(0)}{dx} = 0 \qquad \frac{d^2f(0)}{dx^2} = -1 \qquad \frac{d^3f(0)}{dx^3} = 0$

$\qquad p(x) = 1 + 0 \frac{x}{1} + -1 \frac{x^2}{2} + 0 \frac{x^3}{6}$

$\qquad p(x) = 1 - \frac{x^2}{2} \approx cos(x)$

![](./taylor_series_diagram.png)
