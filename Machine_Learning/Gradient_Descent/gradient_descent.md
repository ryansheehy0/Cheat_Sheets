# Gradient Descent

An algorithm used to iteratively update the input variables of a function in order to find a local minimum. Such functions can have variable number of inputs such as $f(x_1, x_2, ...)$.

## Steps for Gradient Descent:
1. Find the derivative functions with respect to each input a.k.a partial derivatives. 

$\frac{df(x_1, x_2, ...)}{dx_1} , \frac{df(x_1, x_2, ...)}{dx_2}, ...$

- If there is a function within a function like $f(g(x))$ then the chain rule can be used to find the derivative.

	$\frac{df(g(x))}{dx} = \frac{df(g(x))}{dg(x)} * \frac{dg(x)}{dx}$

	Example:

	$f(x) = 2x^2$

	$g(x) = x^3$

	$\frac{dg(x)}{dx} = 3x^2$

	$\frac{df(x)}{dx} = 4x$

	$\frac{df(g(x))}{dx} = 4g(x) * 3x^2 = 4x^3 * 3x^2 = 12x^5$

2. Put some guess into each of the partial derivative functions.

guesses: $\qquad x_1 = a_1 \qquad x_2 = b_1$

$\frac{df(a_1, b_1, \ldots)}{dx_1} = slope \text{_} {x_1}$

$\frac{df(a_1, b_1, \ldots)}{dx_1} = slope \_ x_1$

$, \qquad \frac{df(a_1, b_1, \ldots)}{dx_2} = slope \text{\_} x_2, \qquad \ldots$

3. Calculate the step size for each input. Where $step \_ size = slope * learning \_ rate$.

$step \text{_} size \_ x_1 = slope \_ x_1 * learning \_ rate$

$step \_ size \_ x_2 = slope \_ x_2 * learning \_ rate$

$...$

- If the learning rate is set too high then it can overshoot local minimums.
- If the learning rate is set too low then it may take long to find local minimums.
- It is advised the learning rate be set high and if the step size doesn't decrease in a reasonable amount of cycles then the learning rate can be decreased.

4. Calculate the new guess for each input. Where $new \_ guess = old \_ guess - step \_ size$.

$a_2 = a_1 - step \_ size \_ x_1$

$b_2 = b_1 - step \_ size \_ x_2$

$...$

5. Repeat/cycle to step 2 with the new guess.
- If cycled for too many times or the step size is very small then end.