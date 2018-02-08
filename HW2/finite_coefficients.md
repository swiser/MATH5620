# Function Name: finite_coefficients()

### Last Mod Date

February 7, 2018

### Author

Skyler Wiser

### Written For

Python 2.7.13

### Description

Computes the coefficients for finite difference approximations of an arbitrary order of accuracy for a given derivative. Uses LU factorization with scaled partial pivoting to solve.

### Inputs

* k: The order of the derivative to be approximated
* xbar: The x location the derivative is being approximated at
* x: A list of trace points near x to approximate the derivative

### Outputs

* A list of finite difference coefficients

### Code Used

* [LU Factorization](https://swiser.github.io/MATH5620/HW2/LU_factorization)
* [LU Solve](https://swiser.github.io/MATH5620/HW2/LU_solve)

### Code

```python
def finite_coefficients(k,xbar,x):
    '''
    k=order of derivative to approximate
    xbar= x location derivative is being approximated at
    x= list of trace points near x to approximate
    '''
    n=len(x)
    # Initialize A as 1's
    A=[[1 for row in xrange(n)]for col in xrange(n)]
    
    xrow=[(x[i]-xbar) for i in xrange(n)]
    factorial=1
    # Fill out Vandermonde matrix, from 2nd row to end
    for i in xrange(1,n,1):
        factorial=factorial*i
        #populate every cell in row
        for col in xrange(n):
            A[i][col]=(xrow[col]**i)/float(factorial)
    
    # Generate B matrix, all terms 0 except B[k]=1
    b=[0 for row in xrange(n)]
    b[k]=1
    A_factored, P=LU_factorization(A)
    coeff=LU_solve(A_factored,P,b)
    
    return coeff
```

### Examples
#### Prompt

```python
## Approximating the 6th derivative of x, 
## using 11 trace points centered about x.

k=6
xbar=5
x=[0,1,2,3,4,5,6,7,8,9,10]

computed_coefficients=finite_coefficients(k,xbar,x)


wikipedia_coefficients=[]
wikipedia_coefficients+=[13.0/240.0,-19.0/24.0,87.0/16.0]
wikipedia_coefficients+=[-39.0/2.0,323.0/8.0,-1023.0/20.0]
wikipedia_coefficients+=[323.0/8.0,-39.0/2.0,87.0/16.0]
wikipedia_coefficients+=[-19.0/24.0,13.0/240.0]

print "{:10s} | {:10s}".format('Wikipedia','Computed')
for i in xrange(len(wikipedia_coefficients)):
    print "{: 10.5f} |".format(wikipedia_coefficients[i]),
    print "{: 10.5f}".format(computed_coefficients[i])
```

#### Output

```
Wikipedia  | Computed  
   0.05417 |    0.05417
  -0.79167 |   -0.79167
   5.43750 |    5.43750
 -19.50000 |  -19.50000
  40.37500 |   40.37500
 -51.15000 |  -51.15000
  40.37500 |   40.37500
 -19.50000 |  -19.50000
   5.43750 |    5.43750
  -0.79167 |   -0.79167
   0.05417 |    0.05417
```
