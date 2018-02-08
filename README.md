# MATH 5620
Math 5620 Numerical Solutions of Differential Equations
### Skyler Wiser

This webpage contains the functions written for the MATH 5620 class.

## Basic Computations

### 1. Basic Routines

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [SinglePrecisionEps()](https://swiser.github.io/MATH5620/HW1/SinglePrecisionEps) | Computes machine epsilon, single precision |
| 2 | [DoublePrecisionEps()](https://swiser.github.io/MATH5620/HW1/DoublePrecisionEps) | Computes machine epsilon, double precision |
| 3 | [absolute_error()](https://swiser.github.io/MATH5620/HW1/absolute_error) | Computes the absolute error between two values |
| 4 | [relative_error()](https://swiser.github.io/MATH5620/HW1/relative_error) | Computes the relative error between two values |

### 2. Vector Routines

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [one_norm_vector()](https://swiser.github.io/MATH5620/HW2/one_norm_vector) | Computes the 1-norm of a vector |
| 2 | [two_norm_vector()](https://swiser.github.io/MATH5620/HW2/two_norm_vector) | Computes the 2-norm of a vector |
| 3 | [inf_norm_vector()](https://swiser.github.io/MATH5620/HW2/inf_norm_vector) | Computes the ∞-norm of a vector |
| 4 | [vector_error_one()](https://swiser.github.io/MATH5620/HW2/vector_error_one) | Computes the vector error \|\|x-y\|\|<sub><sub>1</sub></sub> |
| 5 | [vector_error_two()](https://swiser.github.io/MATH5620/HW2/vector_error_two) | Computes the vector error \|\|x-y\|\|<sub><sub>2</sub></sub> |
| 6 | [vector_error_inf()](https://swiser.github.io/MATH5620/HW2/vector_error_inf) | Computes the vector error \|\|x-y\|\|<sub><sub>∞</sub></sub> |

### 3. Matrix Routines

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [LU_factorization()](https://swiser.github.io/MATH5620/HW2/LU_factorization) | Performs LU decomposition with scaled partial pivoting |
| 2 | [LU_solve()](https://swiser.github.io/MATH5620/HW2/LU_solve) | Solves a system [L][U]x=b |
| 3 | [LU_tridiag()](https://swiser.github.io/MATH5620/HW2/LU_tridiag) | Uses LU decomposition to solve a tridiagonal linear system |
| 4 | [Jacobi_tridiag()](https://swiser.github.io/MATH5620/HW2/Jacobi_tridiag) | Uses Jacobi iteration to solve a tridiagonal linear system |
| 5 | [Thomas_alg()](https://swiser.github.io/MATH5620/HW2/Thomas_alg) | Uses the Thomas Algorithm to solve a tridiagonal linear system |

## Differential Equations

### 1. Finite Difference Methods

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [finite_coefficients()](https://swiser.github.io/MATH5620/HW2/finite_coefficients) | Computes coefficients for arbitrary finite difference methods |

### 2. Elliptic Problems
| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [elliptic_ODE()](https://swiser.github.io/MATH5620/HW2/elliptic_ODE) | Solves a simple elliptic ODE with Dirichlet Boundary Conditions |


## Test Problems

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [true_logistic_function()](https://swiser.github.io/MATH5620/HW1/true_logistic_function) | Computes P(t) of common logistic function |
| 2 | [spring_mass()](https://swiser.github.io/MATH5620/HW1/spring_mass) | Computes y(t) of spring-mass-damper system |

## Appendix

(old book, to be updated)
Ascher, U. M., and Chen Greif. A First Course in Numerical Methods. Society for Industrial and Applied Mathematics, 2011.

