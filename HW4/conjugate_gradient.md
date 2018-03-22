# Function Name: conjugate_gradient()

### Last Mod Date
December 12, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Use the Conjugate Gradient method to iteratively solve an size *n* square matrix.
### Inputs

* A: Coefficient matrix A
* B: Solution vector B
* guess: Initial guess *x<sub>o</sub>*
* tolerance: Smallest residual error before returning
* max_iters: Maximum iterations before returning

### Outputs

* x: Final iterative approximation of *x*

### Modules Used

* None

### Notes

A contained function *inner_product()* is used to quickly calculate inner products of vectors for multiple steps of the method.

### Code

#### Function

```python
def conjugate_gradient(A,B,guess,tolerance,max_iters):
    def inner_product(vector1,vector2):
        return float(sum([vector1[i]*vector2[i] for i in xrange(len(vector1))]))
        
    n=len(A)    
    x_old=guess[:]
    error=10*tolerance
    count=0
    if (n!=len(A[0])):
        print "Non square A matrix, returning."
        return
    elif (n!=len(B)):
        print "A and B shape mismatch, returning."
        return

    ## Compute residual B-A*x_0
    residual=[B[i]-sum([A[i][j]*guess[j] for j in xrange(n)]) for i in xrange(n)]

    ## Compute deltaK_old and b_delta
    deltaK_old=inner_product(residual,residual)
    b_delta=inner_product(B,B)
    
    p_k=residual[:]
    while error>(tolerance*tolerance*b_delta) and count <max_iters:
        ## Set s_k, matrix-vector math
        s_k=[sum([A[i][j]*p_k[j] for j in xrange(n)]) for i in xrange(n)]
        ## Determine Alpha
        alpha=deltaK_old/inner_product(p_k,s_k)
        ## Update x vector
        x_old=[x_old[i]+alpha*p_k[i] for i in xrange(n)]
        ## Update residual, recalculate new deltaK
        residual=[residual[i]-alpha*s_k[i] for i in xrange(n)]
        deltaK_new=inner_product(residual,residual)
        ## Update p_k vector
        p_k=[residual[i]+deltaK_new/float(deltaK_old)*p_k[i] for i in xrange(n)]
        error=deltaK_new
        deltaK_old=deltaK_new
        count+=1
    return x_old
```

#### Helper Functions

```python
def print_matrix(A):
    rows=len(A)
    cols=len(A[0])
    for row in xrange(rows):
        print '|',
        for col in xrange(cols):
            print "{:8.2f}".format(A[row][col]),
        print '|'
    print "\n"

def print_column(b):
    rows=len(b)
    for row in xrange(rows):
        print "|{: 14.10f}|".format(b[row])
```

### Example
#### Prompt

```python   
### Answer is [1,1,1]
A=[[10,1,1],[1,10,1],[1,1,10]]
B=[12,12,12]
guess=[15,-.5,3]

print "Conjugate_gradient:",conjugate_gradient(A,B,guess,10**-10,5)
```

#### Output

```python
Conjugate_gradient: [0.9999999999999998, 1.0, 0.9999999999999996]
```










