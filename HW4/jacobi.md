# Function Name: jacobi()

### Last Mod Date
December 12, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Use Jacobi's method to iteratively solve an size *n* square matrix.
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


### Code

#### Function

```python
def jacobi(A,B,guess,tolerance,max_iters):
    n=len(A)    
    x_old=guess[:]
    error=10*tolerance
    count=0

    while error>tolerance and count<max_iters:
        #initialize next guess as B-vector
        x_new=B[:]
        # update x_k, all rows
        for i in xrange(n):
            #loop before diagonal
            for j in xrange(0,i,1):
                x_new[i]=x_new[i]-A[i][j]*x_old[j];
            #loop after diagonal
            for j in xrange(i+1,n,1):
                x_new[i]=x_new[i]-A[i][j]*x_old[j];
        # Suedo-back sub, divide the diagonals of A over
        for i in xrange(n):
            x_new[i]=x_new[i]/float(A[i][i])

        # Calculate L2 norm difference of x_new and x_old (Root sum square)
        # x,y maps to each item in x_old and x_new, "sum" function adds all
        # squared differences that have been put into list bounded by [] created
        # using list comprehension, then is square rooted at end with **.5
        
        error=sum([abs(x-y)**2 for x,y in zip(x_old,x_new)])**.5
        
        x_old=x_new[:]
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

print "Jacobi:", jacobi(A,B,guess,10**-10,5)
```

#### Output

```python
Jacobi: [0.998545, 0.99839, 0.9984250000000001]
```










