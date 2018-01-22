# MATH5620
Math 5620 Numerical Solutions of Differential Equations
### Skyler Wiser

This webpage contains the functions written for the MATH 4610 class. They are seperated by which homework they were assigned to. A full list of functions can be found here:

[**Table of Contents**](https://swiser.github.io/MATH4610/table_of_contents)

#### Homework 1

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [SinglePrecisionEps()](https://swiser.github.io/MATH4610/HW1/SinglePrecisionEps) | Computes machine epsilon, single precision |
| 2 | [DoublePrecisionEps()](https://swiser.github.io/MATH4610/HW1/DoublePrecisionEps) | Computes machine epsilon, double precision |
| 3 | [absolute_error()](https://swiser.github.io/MATH4610/HW1/absolute_error) | Computes the absolute error between two values |
| 4 | [relative_error()](https://swiser.github.io/MATH4610/HW1/relative_error) | Computes the relative error between two values |
| 5 | [Example 1.2](https://swiser.github.io/MATH4610/HW1/example1_2) | Verifies Example 1.2 from the text |
| 6 | [Taylor Series Example](https://swiser.github.io/MATH4610/HW1/TaylorSeriesExample) | Computes the derivative of e<sup>x</sup> |

#### Homework 2

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [bisection()](https://swiser.github.io/MATH4610/HW2/bisection) | Computes root of *f(x)* using bisection method |

#### Homework 3

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [bisection()](https://swiser.github.io/MATH4610/HW2/bisection) | Computes root of *f(x)* using bisection method |
| 2 | [fixed_point()](https://swiser.github.io/MATH4610/HW3/fixed_point) | Computes root of *f(x)* using fixed-point method |

#### Homework 4

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [quick_newton_method()](https://swiser.github.io/MATH4610//HW4/quick_newton_method) | Quick version of Newton-Raphson Method|
| 2 | [newton_method()](https://swiser.github.io/MATH4610/HW4/newton_method) | Newton-Raphson method of root finding |
| 3 | [secant_method()](https://swiser.github.io/MATH4610/HW4/secant_method) | Secant method of root finding |
| 4 | [Convergence Comparison](https://swiser.github.io/MATH4610/HW4/convergence_compare) | Compares the convergence of different methods|
| 5 | [Step Functions](https://swiser.github.io/MATH4610/HW4/step_functions) | Helper functions for hybrid methods |
| 6 | [hybrid_newton()](https://swiser.github.io/MATH4610/HW4/hybrid_newton) | Bisection/Newton hybrid of root finding |
| 7 | [hybrid_secant()](https://swiser.github.io/MATH4610/HW4/hybrid_secant) | Bisection/secant hybrid of root finding |

#### Homework 5

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [one_norm_vector()](https://swiser.github.io/MATH4610/one_norm_vector) | Computes the 1-Norm of a vector |
| 2 | [two_norm_vector()](https://swiser.github.io/MATH4610/two_norm_vector) | Computes the 2-Norm of a vector |
| 3 | [inf_norm_vector()](https://swiser.github.io/MATH4610/inf_norm_vector) | Computes the ∞-Norm of a vector |
| 4 | [one_norm_matrix()](https://swiser.github.io/MATH4610/one_norm_matrix) | Computes the 1-Norm of a matrix |
| 5 | [inf_norm_matrix()](https://swiser.github.io/MATH4610/inf_norm_matrix) | Computes the ∞-Norm of a matrix |
| 6 | [vector_error_one()](https://swiser.github.io/MATH4610/vector_error_one) | Computes the vector error \|\|x-y\|\|<sub><sub>1</sub></sub> |
| 7 | [vector_error_two()](https://swiser.github.io/MATH4610/vector_error_two) | Computes the vector error \|\|x-y\|\|<sub><sub>2</sub></sub> |
| 8 | [vector_error_inf()](https://swiser.github.io/MATH4610/vector_error_inf) | Computes the vector error \|\|x-y\|\|<sub><sub>∞</sub></sub> |
| 9 | [matrix_add()](https://swiser.github.io/MATH4610/matrix_add) | Adds two matrices together |
| 10 | [matrix_subtract()](https://swiser.github.io/MATH4610/matrix_subtract) | Subtracts a matrix from another matrix  |
| 11 | [matrix_scaled()](https://swiser.github.io/MATH4610/matrix_scaled) | Multiplies a matrix by a scalar |
| 12 | [vector_dot()](https://swiser.github.io/MATH4610/vector_dot) | Evaluates the dot product between two vectors |
| 13 | [matrix_vector_product()](https://swiser.github.io/MATH4610/matrix_vector_product) | Multiplies a matrix and a vector together |
| 14 | [matrix_matrix_product()](https://swiser.github.io/MATH4610/matrix_matrix_product) | Multiplies two matrices together |

#### Homework 6

##### Matrix-Matrix Multiplication

[Overview:](https://swiser.github.io/MATH4610/HW6/Matrix_matrix_optimization) Contains the explaination of code, and the graph of the results.
  * _C++ Functions_
  
  | # | Function Name and Link | Description |
  | :--- | :---: | :--- |
  | 1 | [rand_matrix()](https://swiser.github.io/MATH4610/HW6/rand_matrix_c) | Generates random matrix |
  | 2 | [matrixCompare()](https://swiser.github.io/MATH4610/HW6/matrix_compare_c) | Compares two matrices to see if they are the same |
  | 3 | [matrix_multiply()](https://swiser.github.io/MATH4610/HW6/matrix_multiply_c) | Multiplies 2 matrices, vector format |
  | 4 | [vector_openmp_matrix()](https://swiser.github.io/MATH4610/HW6/vector_openmp_matrix) | Multiplies 2 matrices, openMP with vector read |
  | 5 | [normal_openmp_matrix()](https://swiser.github.io/MATH4610/HW6/normal_openmp_matrix) | Multiplies 2 matrices, openMP with 2D array read |
  | 6 | [transposed_openmp_matrix()](https://swiser.github.io/MATH4610/HW6/transposed_openmp_matrix) | Multiplies 2 matrices, openMP with 1D array read |
  
##### LU-Factorization

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [LU_factorization()](https://swiser.github.io/MATH4610/HW6/LU_factorization) | LU-Factorizes a matrix |
| 2 | [LU_solve()](https://swiser.github.io/MATH4610/HW6/LU_solve) | Solves a Ax=b for x using an LU-Factorized matrix A |

#### Exam 1 (Take home portion)

  | # | Problem Number | Assignment (from text) |
  | :--- | :---: | :--- |
  | 1 | [Problem 1](https://swiser.github.io/MATH4610/Exam1/Problem1) | Problems 3.21 and 3.23 |
  | 2 | [Problem 2](https://swiser.github.io/MATH4610/Exam1/Problem2) | Problems 4.5 and 4.7|
  | 3 | [Problem 3](https://swiser.github.io/MATH4610/Exam1/Problem3) | Problem 5.2 |
  | 4 | [Problem 4](https://swiser.github.io/MATH4610/Exam1/Problem4) | Problems 5.17 and 5.18 |

#### Homework 7

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [jacobi()](https://swiser.github.io/MATH4610/HW7/jacobi) | Computes solution to system of equations using Jacobi's method |
| 2 | [gauss_seidel()](https://swiser.github.io/MATH4610/HW7/gauss_seidel) | Computes solution to system of equations using the Gauss-Seidel method |
| 3 | [steepest_ascent()](https://swiser.github.io/MATH4610/HW7/steepest_ascent) | Computes solution to system of equations using the steepest ascent method |
| 4 | [conjugate_gradient()](https://swiser.github.io/MATH4610/HW7/conjugate_gradient) | Computes solution to system of equations using the conjugate gradient method |
| 5 | [Iterative Comparison](https://swiser.github.io/MATH4610/HW7/iterative_compare) | Compares the 4 iterative functions |

#### Homework 8

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [parallel_jacobi()](https://swiser.github.io/MATH4610/HW8/parallel_jacobi) | Computes solution to system of equations using parallelized Jacobi's method |
| 2 | [parallel_gauss_seidel()](https://swiser.github.io/MATH4610/HW8/parallel_gauss_seidel) | Computes solution to system of equations using the parallelized Gauss-Seidel method |
| 3 | [parallel_steepest_ascent()](https://swiser.github.io/MATH4610/HW8/parallel_steepest_ascent) | Computes solution to system of equations using the parallelized steepest ascent method |
| 4 | [parallel_conjugate_gradient()](https://swiser.github.io/MATH4610/HW8/parallel_conjugate_gradient) | Computes solution to system of equations using the parallelized conjugate gradient method |
| 5 | [Parallel Comparison](https://swiser.github.io/MATH4610/HW8/parallel_compare) | Compares the 4 iterative functions in parallel vs not in parallel |

#### Homework 9

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [power_method()](https://swiser.github.io/MATH4610/HW9/power_method) | Computes the largest eigenvalue of a matrix using power iteration |
| 2 | [inverse_power_method()](https://swiser.github.io/MATH4610/HW9/inverse_power_method) | Computes the smallest eigenvalue of a matrix using inverse power iteration |

#### Homework 10

| # | Function Name and Link | Description |
| :--- | :---: | :--- |
| 1 | [difference_coefficients()](https://swiser.github.io/MATH4610/HW10/difference_coefficients) | Computes the coefficients in a divided difference table |
| 2 | [generate_from_coeff()](https://swiser.github.io/MATH4610/HW10/generate_from_coeff) | Interpolates f(x) values using the Newton form of the interpolating polynomial  |
| 3 | [Runge Phenomenon](https://swiser.github.io/MATH4610/HW10/runge_phenomenon) | Shows the problems with interpolating a Runge function |

### Textbook Used

Ascher, U. M., and Chen Greif. A First Course in Numerical Methods. Society for Industrial and Applied Mathematics, 2011.

