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
| 5 | [euler_newton()](https://swiser.github.io/MATH5620/HW5/euler_newton) | Modified Newton method for implicit Euler method |


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
| 6 | [one_norm_matrix()](https://swiser.github.io/MATH5620/HW3/one_norm_matrix) | Computes the 1-norm of a matrix |
| 7 | [inf_norm_matrix()](https://swiser.github.io/MATH5620/HW3/inf_norm_matrix) | Computes the ∞-norm of a matrix |
| 8 | [power_method()](https://swiser.github.io/MATH5620/HW3/power_method) | Computes the largest eigenvalue of a matrix |
| 9 | [inverse_power_method()](https://swiser.github.io/MATH5620/HW3/inverse_power_method) | Computes the smallest eigenvalue of a matrix |
| 10 | [jacobi()](https://swiser.github.io/MATH5620/HW4/jacobi) | Solves a matrix system [A][x]=[b] using Jacobi Iteration |
| 11 | [gauss_seidel()](https://swiser.github.io/MATH5620/HW4/gauss_seidel) | Solves a matrix system [A][x]=[b] using Gauss Seidel Iteration |
| 12 | [conjugate_gradient()](https://swiser.github.io/MATH5620/HW4/conjugate_gradient) | Solves a matrix system [A][x]=[b] using the Conjugate Gradient method |


## Differential Equations

### 1. Finite Difference Methods

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [finite_coefficients()](https://swiser.github.io/MATH5620/HW2/finite_coefficients) | Computes coefficients for arbitrary finite difference methods |

### 2. Elliptic Problems

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [elliptic_ODE()](https://swiser.github.io/MATH5620/HW2/elliptic_ODE) | Solves a simple elliptic ODE with Dirichlet Boundary Conditions |

### 3. Partial Differential Equations

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [five_point_stencil()](https://swiser.github.io/MATH5620/HW3/five_point_stencil) | Solves a Laplace equation in two dimensions using a five point stencil |
| 2 | [nine_point_stencil()](https://swiser.github.io/MATH5620/HW3/nine_point_stencil) | Solves a Laplace equation in two dimensions using a nine point stencil |

### 4. Initial Value Problems/Methods

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [explicit_euler()](https://swiser.github.io/MATH5620/HW4/explicit_euler) | Solve a general IVP using a single-step explicit Euler method |
| 2 | [explicit_euler_tracking()](https://swiser.github.io/MATH5620/HW4/explicit_euler_tracking) | Solve a general IVP using a single-step explicit Euler method for a vector of values |
| 3 | [implicit_euler()](https://swiser.github.io/MATH5620/HW5/implicit_euler) | Solve a general IVP using a single-step implicit Euler method |
| 4 | [Runge Kutta](https://swiser.github.io/MATH5620/HW5/runge_kutta) | Solve a general IVP using second and fourth order Runge-Kutta methods |
| 5 | [Predictor-Corrector](https://swiser.github.io/MATH5620/HW5/predictor_corrector) | Solve a general IVP using an Adams Bashforth/Moulton predictor-corrector method |

### 5. Parabolic Problems (Heat Equation)

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [Heat Equation: Explicit Euler](https://swiser.github.io/MATH5620/HW7/HE_explicit) | Solve the heat equation using explicit Euler |
| 2 | [Heat Equation: Implicit Euler](https://swiser.github.io/MATH5620/HW7/HE_implicit) | Solve the heat equation using implicit Euler |
| 3 | [Heat Equation: Predictor-Corrector](https://swiser.github.io/MATH5620/HW7/HE_predictor_corrector) | Solve the heat equation using Predictor-Corrector |
| 4 | [Heat Equation: RK4](https://swiser.github.io/MATH5620/HW7/HE_RK4) | Solve the heat equation using RK4 timestepping |


## Test Problems

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [true_logistic_function()](https://swiser.github.io/MATH5620/HW1/true_logistic_function) | Computes P(t) of common logistic function |
| 2 | [spring_mass()](https://swiser.github.io/MATH5620/HW1/spring_mass) | Computes y(t) of spring-mass-damper system |
| 3 | [Tridiagonal Solver Comparison](https://swiser.github.io/MATH5620/HW2/tri_solvers) | Compare tridiagonal system solvers |
| 4 | [Problem 2-9](https://swiser.github.io/MATH5620/HW2/Problem_9) | Elliptic ODE with k(x) condition |




## Comparisons and Case Studies

| # | Study | Description |
| :--- | :---: | :--- |
| 1 | [Iterative Comparison](https://swiser.github.io/MATH5620/HW4/iterative_comparison) | Compares iterative matrix solvers and the amount of iterations it takes for each to converge |
| 2 | [IVP Stepping Comparison](https://swiser.github.io/MATH5620/HW5/stepping_methods) | Compares different functions' ability to solve general initial value problems |
| 3 | [Chapter 7 IVP Testing](https://swiser.github.io/MATH5620/HW6/HW_6_comparison) | Recreate Chap. 7 stability concerns using IVP methods |



## Appendix

LeVeque, Randall J. Finite Difference Methods for Ordinary and Partial Differential Equations. Society for Industrial and Applied Mathematics, 2007.

Ascher, U. M., and Chen Greif. A First Course in Numerical Methods. Society for Industrial and Applied Mathematics, 2011.


