# Iterative Method Comparison: Iteration Count

### Last Mod Date
March 21, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Solve with different iterative methods the given Laplace Equation on the unit square in two dimensions using a five point stencil. Compare the number of iterations to convergence as the size of the square matrix increases.


### Modules Used

* import math
* import numpy as np

### Code Used

* [LU Factorization](https://swiser.github.io/MATH5620/HW2/LU_factorization)
* [LU Solve](https://swiser.github.io/MATH5620/HW2/LU_solve)
* [5-Point Stencil](https://swiser.github.io/MATH5620/HW3/five_point_stencil)
* [Jacobi Solver](https://swiser.github.io/MATH5620/HW4/jacobi)
* [Gauss-Seidel Solver](https://swiser.github.io/MATH5620/HW4/gauss_seidel)
* [Conjugate Gradient Solver](https://swiser.github.io/MATH5620/HW4/conjugate_gradient)
* [Vector Error, 2-norm](https://swiser.github.io/MATH5620/HW2/vector_error_two)

### Code

Within each of the iterative methods, the count was returned alongside the solution vector. The last line of every method was modified to be:

```python
    return x_old,count
```

Now that count was being returned, within the 5-Point stencil code, the following was added:

```python
    LU,p=LU_factorization(A)
    u=LU_solve(LU,p,b)

    guess=[0.0]*size
    
    u_jacobi,iters_jacobi= jacobi(A,b,guess,10**-5,1000)
    u_GS,iters_GS= gauss_seidel(A,b,guess,10**-5,1000)
    u_CG,iters_CG=conjugate_gradient(A,b,guess,10**-5,1000)
    
    jacobi_error=vector_error_two(u,u_jacobi)
    GS_error=vector_error_two(u,u_GS)
    CG_error=vector_error_two(u,u_CG)

    print "For size {:d} matrix:".format(len(A))
    print "Jacobi took: {:6d} iterations, error from LU:{:6f}".format(iters_jacobi,jacobi_error)
    print "Gauss Seidel took: {:6d} iterations, error from LU:{:6f}".format(iters_GS,GS_error)
    print "Conjugate Gradient took: {:6d} iterations, error from LU:{:6f}".format(iters_CG,CG_error)

```


### Examples
#### Prompt

```python
m=6
n=6
delta_x=1/float(n)
delta_y=1/float(m)
u=five_point_laplace(n,m,lambda x,y:math.sin(x*y))
```

#### Output

Using a 5x5, 10x10, 15x15 and 20x20 mesh, the following output was recorded:


```python
For size 25 matrix:
Jacobi took:     48 iterations, error from LU:0.000059
Gauss Seidel took:     28 iterations, error from LU:0.000025
Conjugate Gradient took:     12 iterations, error from LU:0.000000

For size 100 matrix:
Jacobi took:    149 iterations, error from LU:0.000231
Gauss Seidel took:     85 iterations, error from LU:0.000109
Conjugate Gradient took:     25 iterations, error from LU:0.000000

For size 225 matrix:
Jacobi took:    297 iterations, error from LU:0.000502
Gauss Seidel took:    169 iterations, error from LU:0.000244
Conjugate Gradient took:     37 iterations, error from LU:0.000000

For size 400 matrix:
Jacobi took:    487 iterations, error from LU:0.000883
Gauss Seidel took:    277 iterations, error from LU:0.000439
Conjugate Gradient took:     48 iterations, error from LU:0.000000
```


