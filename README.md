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
&\text{subject to} && 2x_1+x_2 =\, 5\\
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

## Economic application

### Maximize the utility of a consumer

$$
\begin{aligned}
&\text{Max.} && f(x_1,x_2)=x_1^{0.5}x_2^{0.5} \\
&\text{subject to} && 4x_1+3x_2 =\, 100\\
& && x_1,x_2 \in \mathbb{R}
\end{aligned}
$$


## `NlcOptim::solnl()`

```{r}
objective <- function(x) -x[1]^0.5*x[2]^0.5
NlcOptim::solnl(c(1,1),objective,Aeq=matrix(c(4,3),nrow = 1), Beq=100)
```
# Linear Programming

- Linear programming is a method used to optimize a linear objective function subject to linear equality and inequality constraints
- Linear programming is widely used in economics and operations research to model and optimize complex systems

### Utility in Economics

- Linear programming can be used to model and optimize supply chain management, production planning, and financial planning
- For example, a company may use linear programming to minimize production costs subject to production capacity and demand constraints

### Utility in Tourism

- In tourism, linear programming can be used to optimize tour itineraries, hotel bookings, and transportation logistics
- For example, a tour company may use linear programming to optimize a tour itinerary to maximize the number of tourist attractions visited subject to time and budget constraints

## Mathematical specification

$$
\begin{aligned}
&\text{optimize} && c^tx \\
&\text{subject to} && Ax \leq b\\
& && x \geq 0
\end{aligned}
$$

where $x=(x_1,\ldots,x_n)$ is the vector of decision variables, $c=(c_1,\ldots,c_n)$ is the vector of coefficients in the objective function an $A$ is the matrix of coefficients in the m constraints.

## Example

Consider that the capacity of Gran Canaria Hotel is 100 guests and receives requests for accommodation from Britain and Germany. The profit per guest obtained by the hotel is 40 and 30 monetary units (mu.), for British and German visitor respectively. Moreover, the accommodation of any guest requires a resource. Each season the available amount of this resource is 30000 units,and the requirement per season of each guest is 600 and 150 units of resource per British and German guest respectively. The hotel receives a high number of requests and desires to determine how many requests of each nationality must accept to maximize the profit.


- Decision variables

$x_1$ = number of British guests accommodated at the hotel every season

$x_2$ = number of German guests accommodated at the hotel every season.

- Objective function

$$ f(x_1, x_2) = 40x_1 + 30x_2=(40\quad 30)\begin{pmatrix}x_1\\x_2\end{pmatrix}$$

- Constraints

$$
\begin{aligned}
x_1+x_2&\leq 100\\
400x_1+150x_2&\leq 30000\\
x_1,x_2&\geq 0
\end{aligned}
$$

$$\begin{bmatrix}
1&1\\
400&150
\end{bmatrix}
\begin{pmatrix}
x_1\\
x_2
\end{pmatrix}\leq 
\begin{pmatrix}
100\\
30000
\end{pmatrix}
$$

## Problem formulation

$$
\begin{aligned}
&\max_{x_1,x_2} && 40x_1 + 30x_2 \\
&\text{s.t.} 
&&x_1+x_2\leq 100\\
&&&400x_1+150x_2\leq 30000\\
& && x \geq 0
\end{aligned}
$$

## `lpSolve::lp()`

```{r}
# Loading the package
library(lpSolve)

# Coefficients of objective functions
objective.in <- c(40, 30)

# Matrix of coefficients of constraints
const.mat <- matrix(c(1, 1, 400, 150), nrow=2, byrow=TRUE)

# Right hand side of inequities
const.rhs <- c(100, 30000)

# Direction of inequities
const.dir <- c("<=", "<=")

optimum <- lp(direction="max", objective.in, const.mat,
const.dir, const.rhs)

```
---

- **Optimal values** of $x_1$ and $x_2$
```{r}
optimum$solution

```

- **Objective** at minimum

```{r}
optimum$objval
```

