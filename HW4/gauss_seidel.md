# Function Name: gauss_seidel()

### Last Mod Date
December 12, 2017
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Use the Gauss-Seidel method to iteratively solve an size *n* square matrix.
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
def gauss_seidel(A,B,guess,tolerance,max_iters):
    n=len(A)    
    x_old=guess[:]
    error=10*tolerance
    count=0
    x_new=[0.0]*n

    while error>tolerance and count<max_iters:
        #initialize next guess as B-vector
        # update x_k, all rows
        for i in xrange(n):
            #do both inner summations,preserve x_new
            first_sum=0.0
            second_sum=0.0
            
            #loop before diagonal
            for j in xrange(0,i,1):
                first_sum+=A[i][j]*x_new[j];
            #loop after diagonal
            for j in xrange(i+1,n,1):
                second_sum+=A[i][j]*x_old[j];

            #update x_new[i] to be used in next iteration
            x_new[i]=(B[i]-first_sum-second_sum)/float(A[i][i])
        

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

print "Gauss_seidel:",gauss_seidel(A,B,guess,10**-10,5)
```

#### Output

```python
Gauss_seidel: [0.99999941898245, 1.000000108648705, 1.0000000472368844]
```










