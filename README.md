# tidesmaster

## Constrained Optimization

- Introduction
- Optimization with Equality Constraint
- Linear Programming

## Introduction to constraint optimization


$$
\begin{aligned}
&\text{optimize} && f(x) \\
&\text{subject to} && c_i(x) \leq (\geq,=)\, 0, \quad i = 1, \ldots, m \\
& && x_j \in \mathcal{X}_j, \quad j = 1, \ldots, n
\end{aligned}
$$
## Constrained Optimization

-Sometimes, the optimization problem has constraints that the solution must satisfy

-A constrained optimization problem involves minimizing or maximizing a function subject to constraints

- Constraints can be expressed as equations or inequalities that the solution must satisfy

### Example: Constrained Optimization in Tourism

- A tour company wants to plan a route for a bus that visits a set of tourist attractions

- The company wants to minimize the distance traveled by the bus subject to the constraint that each attraction must be visited exactly once

- This is an example of a constrained optimization problem, where the objective is to minimize distance traveled subject to the constraint of visiting each attraction once.
---

## Optimization with Equality Constraint

Sometimes we need to optimize a function subject to the constraint that one or more of the parameters must satisfy an equality constraint.

$$
\begin{aligned}
&\text{Max.} && f(x) \\
&\text{subject to} && c_i(x) =\, 0, \quad i = 1, \ldots, m \\
& && x_j \in \mathcal{X}_j, \quad j = 1, \ldots, n
\end{aligned}
$$


## `Rsolnp::solnp()`

### Example:

$$
\begin{aligned}
&\text{Opt.} && f(x_1,x_2)=(x_1-2)^2+(x_2-3)^2 \\
&\text{subject to} && x_1+2x_2 =\, 5\\
& && x_1,x_2 \in \mathbb{R}
\end{aligned}
$$

```{r}
# Define the function to be optimized
fn <- function(x) (x[1] - 2)^2 + (x[2] - 3)^2

# Define the equality constraint
eqfun <- function(x) 2*x[1]+x[2] - 5

# Find the optimal values subject to the constraint
Rsolnp::solnp(pars = c(2, 1), fun = fn, eqfun = eqfun, eqB=0)

```
