---
date: "2021-01-01T00:00:00Z"
url: dl0
title: DL0
---

# TOC

- [Underflow](#underflow)

- [Overflow](#overflow)

- [Softmax ](#softmax-)

    - [Problems](#problems)

- [Condition number](#condition-number)

- [Gradient-Based Optimization](#gradient-based-optimization)
**objective function**; **criterio**; **cost function**; **loss function**; **Gradient Descent**; **critical points**; **stationary points**; **local minumum**; **local maximum**; **Saddle points**; **global minimum**; **partial derivatives**; **gradient**; **directional derivative**; **method of steepest descent**; **gradient descent**; **Chain rule**; **Steepest descent proposes a new point**; **learning rate**; **line search**; **hill climbing**; **Jacobian matrix**; **second derivative**; **Hessian matrix**; **Jacobian**; **Hessian**; **second derivative test**; **Newton's method**; **first-order optimization algorithms**; **second-order optimization algorithms**; **Lipschitz continous**; **Lipschitz constant**; **convex optimization**; 
- [Constrained Optimization](#constrained-optimization)
**constrained optimization**; **feasible points**; **Karush-Kuhn-Tucker**; **generalized Lagrangian**; **equality constraints**; **inequalities constraints**; 


# Underflow

happens when small numbers are rounded to 0. 

# Overflow

happens when numbers with large magnitude are approximated as inf of -inf.


# Softmax 

also called softargmax or normalized exponential function.

basically it's function that turn real values into probabilities.
input is vector of K real numbers and ouput is a probability distribution of K probabilities.

`softmax(x)_i = exp(x_i) / \sum^n_j=1(exp(x_j))`

softmax is vulnerable to both underflow and overflow.

## Problems

if all x_i are equal to some constant c then output should be n probabilities with 1/n value. Numerically this may not occur when c has large magnitude.
If c is very negative then exp(c) will underflow and denominator will be 0.
If c is very large then exp(c) will overflow causing numerator to be inf.

Both of these difficulties can be resolved by instead evaluating softmax(z) where `z = x - max_i * x_i`. Normalization of vector results in the largest argument to exp being 0, which rules out the
possibility of overflow.

But there is still one small problem. Underflow in the numerator can still cause the expression as a whole to evaluate to zero and if we are using `log softmax(x)` we will get -inf.  So we need to
stabilize log max with same trick as above.

# Condition number

ratio of magnitude of the largest and smallest eigenvalue.

`max_i,j |\lambda_i / \lambda_j|`

When this number is large, matrix inversion is particularly sensitive to error in the input.
Conditioning refers to how rapidly a function changes with respect to small changes in its input.

# Gradient-Based Optimization

Optimization refers to the task of either minimizing or maximizing some function f(x) by altering x.
We usually phrase most optimization problems in terms of minimizing. Maximization may be accomplished via a minimization by minimizing -f(x).

The function we want to minimize or maximize is called the **objective function** or **criterio**. When we are minimizing it, we may also call it the **cost function**, **loss function** or **error
function**.

We often denote the value that minimizes or maximizes a function with a superscript ∗ (asterisk) -- it's not mutiplication operator * but slightly different star. 
eg we may write: `x^* = arg min f(x)`

**Gradient Descent** is technique that move x in small steps with oposite sign of the derivate in order to find minimum of function.

Points with 0 derivation are known as **critical points** or **stationary points**. Gradient is the zero vector at a point if and only if it is a stationary point.

A **local minumum** is a point where f(x) is lower than at all neigboring points. A **local maximum** is opposite. Some critical points are neither maximum nor minimum, these are known as **Saddle points**
A point that obtains the absolute lowest value of f(x) is a **global minimum**. There could be one or multiple global minima.

Function that have multiple local minima and saddle points surroundedd by very flat regions makes optimization very difficult, especially when the input to the function is multidimensional. We therfore
usually settle for finding a value of f that is very low, but not neccessarily minimal in any formal sense.

For functions with multiple inputs we use **partial derivatives**. Partial derivative is derivation of one variable, whereas other variables are treated like constants. 

The **gradient** generalizes the notion of derivative to the case where the derivative is with respect to a vector: the gradient of f is the vector containing all of the partial derivatives, denotes
`∇_x f(x)`. Element i of the gradient is the partial derivative of f with respect to x_i. In multiple dimensions, critical points are points where every element of the gradient is equal to zero.

where ∇ is nabla. Nabla can be interpreted as a vector of partial derivative operators.


Gradient: `grad f =  ∇ f`
Divergence: `div v =  ∇ * v`
Curl: `curl v =  ∇ x v`

`∇ = \sum e_i * ∂/∂x_i`

∂ is symbol for partial derivative (it's stylized cursive of letter d).

-----

The **directional derivative** in direction u (a unit vector) is the slope of the function f in direction u.
To minimize f, we would like to find the direction in which f decreases the fastest. We can do this using the directional derivative:

Final form of equation obtained via chain rule: `min u^T ∇_x f(x) = min ||u||_2||∇_x f(x)||_2 cos θ`
where θ is angle between u and the gradient. Substituing in ||u||_2 = 1 and ingoring dactors that do not depend on u, this simplifies to `min_u cos θ`. This is minimized when u points in the oppostite
direction as the the gradient. In the other words, the gradient points directly uphill, and the negative gradient points directly downhill. We can decrease f by moving in the direction of the negative
gradient, This is known as the **method of steepest descent** or **gradient descent**

**Chain rule** - rule about derivation of composite function (f ∘ g).
`(f ∘ g)' = (f'∘ g) * g'`

Alternatively, by letting `h = (f'∘ g)` which equivalent to `h(x) = f(g(x))` for all x, one can also write the chain rule in Lagrange's notation as follows:
`h'(x) = f'(g(x))g'(x) `

The chain rule can be also rewritten in Leibniz's notation if a variable z depends on the variable y, which itself depends on the variable x, then z via the intermediate variable od y, depends on x as
well:
`
dz   dz   dy
-- = -- * --
dx   dy   dx
`


**Steepest descent proposes a new point**

`x' = x - \eps grad_x f(x)`

where \eps is the **learning rate**, a positive scalar determining the size of the step. We can set learning rate to small constant. Sometimes, we can solve for the step size that makes the directional
derivative vanish. Another approach is to evaluate `f(x - \eps grad_x f(x))` for several values of \eps and choose the one that results in the smallest objective function value. This last
strategy is called a **line search**.

In some cases, we may be able to avoid running this iterative algorithm, and just jump directly to the critical point by solving the equation `grad_x f(x) = 0` for x

Altough gradient descent is limited to optimization in continous paces, the general concept of repreatedly making a small move towards better configutaions can be generalized to discrete space.
Ascending an objective function of discrete parameters is called **hill climbing**.

Matrix of partial derivatives of function whose input and output are both vectors is known as a **Jacobian matrix**.

Derivative of derivative is called **second derivative**. We can think of the second derivative as measuring curvature. It could tell us how big step we should take.

{{<image src="/images/curvature.png" alt="Curvatures" position="center" >}}

When our function has multiple input dimensions, there are many second derivatives. These derivatives can be collected together into a matrix called the **Hessian matrix**.

determinant of Jacobi matrix is called **Jacobian** and determinant of Hessian matrix is called **Hessian**.

The eigenvalues of the Hessian is used to determine the scale of the learning rate.


Suppose we have critical point f'(x) = 0. When the second derivative f''(x) > 0, then first derivate increase as we move to the right and decrease when moving left. This tells us that x is local minumum. 
Simmilary `f''(x) < 0` conclude local maximum. This is called **second derivative test**. When f''x = 0 the test is inconclusive and x may be saddle point or part of a flat region.

In multiple dimensions, we need to examine all of the second derivatives of the function. Using the eigendecomposition of the Hessian matrix, we can generalize the second derivative test to multiple
dimensions. At a critical point where `grad_x f(x) = 0` we can examine the eigenvalues of the Hessian to determine wheter the critical point is local minimum/maximum or saddle point. When the Hessian is
positive definite (all its eigenvalues are positive), the point is a local minimum. Likewise when the Hessian is negative definite (all its eigenvalues are negative), the point is a local maximum. The
test in multiple dimensions are inconclusive whener all of the non-zero eigenvalues have the same sign, but at least one eigen is zero. When at least one eigenvalue is positive and at least one is
negative we know that x is both a local minimum on one cross section and maximum on another cross section.


**Newton's method** is iterative method that can find critical point even faster than gradient descent however ca be harmful near saddle points. Newton's method is only approriate when the nearby
critical point is a minimum (all the eigenvalues of the Hessian are positive), whereas gradient descent is not attracted to saddle points unless the gradient points toward them.


Optimization algorithms that use only the gradient, such as gradient descent, are called **first-order optimization algorithms**. Optimization algorithms that also use the Hessian matrix, such as Newton's
method, are called **second-order optimization algorithms**.

In DL we use algorithms that have almost no guarantees. Mostly because family of functions used in DL is quite complicated. In many other fields, the dominant approach to optimization is to design
optimization algorithms for a limited family of functions.

In the context of DL, we sometimes fain some guarantees by restricting ourselves to functions that are either **Lipschitz continous** or have Lipschitz continous derivatives. a Lipschitz continous
function is a function f whose rate of change is bounded by a **Lipschitz constant** often denoted as weird capital L:

`∀x, ∀y, |f(x) - f(y)|<=L ||x-y||_2`
where L is Lipschitz constant.

This property is useful because it allow us to assume that a small change in the input will have a small change in the output. Lipschitz continuity is also a fairly weak constraint, and many optimization
problems in DL can be made Lipschitz continuos with relatively minor modifications.

Perhaps the most sucesful field of specialized optimization is **convex optimization**. Convex optimization algorithms are able to provide many more guarantees by making stronger restrictions. Convex
optimization algorithms are applicable only to convex functions -- functions for which the Hessian is positive semidefinite everywhere. Such functions are well-behaved because they lack saddle points and
all of their local minima are necessarily global minima. However most problems in DL are difficult to express in terms of convex optimization but some algorithms use it as subroutines. Ideas from the
analysis of convex optimization can be useful for proving the convergence of DL algorithms.



# Constrained Optimization

Sometimes we may with to find the maximal or minimal value of f(x) for values of x just in some set S. This is known as **constrained optimization**. Points x that lie within the set S are called
**feasible points** in constrained optimization terminology. 

There are few approaches to constrained optimization.

First approach is to modify gradient descent, with use of line search, we can search only over step sizes \eps that yields new x points that are feasible.

A more sophisticated is to design a different, unconstrained optimization problem whose solution can be converted into a solution to the original, constrained optimization problem. This approach requires
creativity; the transformation between optimization problems must be designed specifically for each case we encounter.

The **Karush-Kuhn-Tucker** (KKT) approach provides a very general solution to constrained optimization. With the KKT approach we introduce a new function called the **generalized Lagrangian** or **generalized
Lagrange function**.
To define the Lagrangian, we fist need to describe S in terms of equations and inequalities. We want a description of S in terms of m functions g^(i) and n functions h^(j) so that:
`S={x|∀i,g^(i)(x) = 0 and ∀j,h^(j)(x) <= 0}`

The equations involving g^(i) are called the **equality constraints** and the inequalities involving h^(j) are called **inequalities constraints**.

We introduce new variables \lambda_i and \alpha_j for each constrain, these are called the KKT multipliers. The generalized Lagrangian is then defined as
`L(x, \lambda, \alpha) = f(x) + \sum_i \lambda_i g^(i)(x) + \sum_j \alpha_j h^(j)(x)` 

We can now solve a constrained minimization problem using unconstrained optimization of the generalized Lagrangian. Observe that, so long as at least one feasible point exists and f(x) is not permitted
to have value inf, then

`min_x max_\lambda max_(\alpha,\alpha>=0) L(x, \lambda, \alpha)`


has the same optimal objective function value and set of optimal points x as:
`min_(x∈S) = f(x)`

This follows because any time the constains are satisfied:

`max_\lambda max_(\alpha,\alpha>=0) L(x, \lambda, \alpha) = f(x)`

while any time a constraint is violated:

`max_\lambda max_(\alpha,\alpha>=0) L(x, \lambda, \alpha) = \inf`

These properties guarantee that no infeasible point can be optimal, and that the optimum within the feasible points is unchanged.

We say that a constraint `h^(i)(x)` is active if `h^(i)(x*) = 0`. If a constraint is not active, then the solution to the problem found using would remain at least a local solution of that constraint
were removed. It's possible that an inactive constraint excludes other solutions. eg a convex problem with an entire region of globally optimal points (a wide, flat, region of equal const) could have a
subset of this region eliminated by constraints or a non-convex problem could have better local stationary points exluded by a constraint that is inactive at convergence.

We can say that either the solution is on the boundary imposed by the inequality and we must use its KKT multiplier to influence the solution to x, or the inequality has no influence on the solution and
we represent this by zeroing out its KKT multiplier.


A simple set of properties describe the optimal points of constrained optimization problems. These properties are called the KKT conditions. They are necessary conditions, but not always sufficient for a
point to be optimal. The conditions are:

 - The gradient of the generalized Lagrangian is zero.
 - All constraints on both x and the KKT multipliers are satisfied
 - The inequality constrains exhibit "complementary slackness": `\alpha ⊙ h(x) = 0`







