# Function Name: power_method()

### Last Mod Date
February 21, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Uses power iteration to find the largest eigenvalue of a matrix.
### Inputs

* A: The matrix to be searched
* v0: An initial guess of the dominant eigenvector
* tolerance: Smallest variation between eigenvalue estimates in each iteration
* max_iters: Maximum iterations to perform before exiting

### Outputs

* lambda: The largest eigenvalue of matrix A

### Modules Used

* numpy


### Code

```python
def power_method(A,v0,tolerance,max_iters):
    ## Check matrix and eigenvector shapes,
    ## matrix must be square, must match the eigenvector length.
    if len(A) != len(A[0]) or len(A) != len(v0):
        print "A is {:d}x{:d}, v is {:d}x1.".format(len(A),len(A[0]),len(v0))
        print "Bad matrix/vector shapes. Exiting."
        return

    ## Initialize variables, use list comprehension to do matrix-vector math
    n=len(A)
    y=[sum([A[row][col]*v0[col]for col in xrange(n)])for row in xrange(n)]
    error=10*tolerance
    lambda_old=0.0
    count=0
    while error>tolerance and count<max_iters:
        # Calculate magnitude of v_k, normalize v_k and store as x
        y_magnitude=float(sum([y[i]**2 for i in xrange(n)])**.5)
        x=[y[i]/y_magnitude for i in xrange(n)]

        # Calculate A*v_k, store as s
        s=[sum([A[row][col]*x[col]for col in xrange(n)])for row in xrange(n)]

        # Calculate new lambda using v_k(transposed)*A*v_k
        lambda_new=sum([x[i]*s[i] for i in xrange(n)])
        error=abs(lambda_old-lambda_new)
        y=s
        lambda_old=lambda_new
        count+=1
    
    if error>tolerance:
        print "Maximum iterations met."
        print "took {:d} iterations".format(count)

    return lambda_old
```
### Helper Code

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
    
def hilbert_matrix(n):
    return [[1/float(row+col+1) for col in xrange(n)] for row in xrange(n)]
    
def elliptic_matrix(n):
    A=[[0.0 for i in xrange(n)] for j in xrange(n)]
    A[0][0]=-2.0
    A[0][1]=1.0
    A[n-1][n-1]=-2.0
    A[n-1][n-2]=1.0

    for row in xrange(1,n-1,1):
        for col in xrange(n):
            A[row][row-1]=1.0
            A[row][row]=-2.0
            A[row][row+1]=1.0
    return A

```

### Examples
#### Hilbert Matrix Prompt

```python
###########################################                   
### Test power method on Hilbert Matrix ###
###########################################

hilbert_5=hilbert_matrix(5)
print "5x5 Hilbert Matrix:\n"
print_matrix(hilbert_5)
print "Largest eigenvalue: {: 10.6f}".format(power_method(hilbert_5,[1.0]*5,10**-15,100))

```

#### Hilbert Matrix Output

```
5x5 Hilbert Matrix:

|     1.00     0.50     0.33     0.25     0.20 |
|     0.50     0.33     0.25     0.20     0.17 |
|     0.33     0.25     0.20     0.17     0.14 |
|     0.25     0.20     0.17     0.14     0.12 |
|     0.20     0.17     0.14     0.12     0.11 |


Largest eigenvalue:   1.567051
```
#### Elliptic Matrix Prompt

While using the power method for the elliptic matrix, the answers were checked using numpy. It was discovered for this particular matrix, the second largest eigenvalue was often found when using the initial guess of [1.0]*n. It was discovered by alternating between 1.0 and -1.0 in the initial guess, convergence to the dominant eigenvalue was more steady.

An example of this sensitivity is shown at the end of the prompt, using a 4x4 elliptic matrix.

```python
############################################                  
### Test power method on Elliptic Matrix ###
############################################

print "Elliptic ODE matrix A vs Largest Eigenvalue of A"
print "{:^10s}|{:^13s}|{:^13s}".format('Size','Largest Eig','Numpy')
print "---------------------------------------------------"
for n in xrange(2,10,1):
    guess=[(-1.0)**i for i in xrange(n)]
    elliptic=elliptic_matrix(n)
    elliptic_eig=power_method(elliptic,guess,10**-6,1000)
    print "{:10d}|{:13.7f}|{:13.7f}".format(n,elliptic_eig,max(np.linalg.eig(elliptic)[0],key=abs))
    
for n in xrange(10,50,5):
    guess=[(-1.0)**i for i in xrange(n)]
    elliptic=elliptic_matrix(n)
    elliptic_eig=power_method(elliptic,guess,10**-6,1000)
    print "{:10d}|{:13.7f}|{:13.7f}".format(n,elliptic_eig,max(np.linalg.eig(elliptic)[0],key=abs))


############################################################################                 
### Test power method on Elliptic Matrix, show initial guess sensitivity ###
############################################################################

    
print "\n\n\nGuess Sensitivity:"
sensitivity_test=elliptic_matrix(4)
print_matrix(sensitivity_test)
guess=[.372,.601,-.372,-.601]
numpy_data=np.linalg.eig(sensitivity_test)
print "i | Numpy Eigenvalues | Associated Eigenvector"
for i in xrange(len(numpy_data[0])):
    print i, '|', numpy_data[0][i], "|", numpy_data[1][i]
    
print ""
print "Power method, guess [1.0 ,1.0 ,1.0  ,1.0  ]:",power_method(sensitivity_test,[1.0]*4,10**-8,400)
print "Power method, guess [.372,.601,-.372,-.601]:",power_method(sensitivity_test,guess,10**-8,400)
print "Power method, guess [1.0 ,-1.0,  1.0,-1.0 ]:",power_method(sensitivity_test,[1.0,-1.0]*2,10**-8,400)

```

#### Elliptic Matrix Output

```
Elliptic ODE matrix A vs Largest Eigenvalue of A
   Size   | Largest Eig |    Numpy    
---------------------------------------------------
         2|   -3.0000000|   -3.0000000
         3|   -3.4142136|   -3.4142136
         4|   -3.6180340|   -3.6180340
         5|   -3.7320507|   -3.7320508
         6|   -3.8019373|   -3.8019377
         7|   -3.8477584|   -3.8477591
         8|   -3.8793842|   -3.8793852
         9|   -3.9021115|   -3.9021130
        10|   -3.9189836|   -3.9189859
        15|   -3.9615649|   -3.9615706
        20|   -3.9776512|   -3.9776617
        25|   -3.9854013|   -3.9854177
        30|   -3.9897152|   -3.9897386
        35|   -3.9923577|   -3.9923894
        40|   -3.9940903|   -3.9941316
        45|   -3.9952849|   -3.9953375



Guess Sensitivity:
|    -2.00     1.00     0.00     0.00 |
|     1.00    -2.00     1.00     0.00 |
|     0.00     1.00    -2.00     1.00 |
|     0.00     0.00     1.00    -2.00 |


i | Numpy Eigenvalues | Associated Eigenvector
0 | -3.61803398875 | [ 0.37174803  0.60150096 -0.37174803 -0.60150096]
1 | -2.61803398875 | [-0.60150096 -0.37174803 -0.60150096 -0.37174803]
2 | -0.38196601125 | [ 0.60150096 -0.37174803 -0.60150096  0.37174803]
3 | -1.38196601125 | [-0.37174803  0.60150096 -0.37174803  0.60150096]

Power method, guess [1.0 ,1.0 ,1.0  ,1.0  ]: -2.61803398867
Power method, guess [.372,.601,-.372,-.601]: -3.61803398169
Power method, guess [1.0 ,-1.0,  1.0,-1.0 ]: -3.61803398821
```