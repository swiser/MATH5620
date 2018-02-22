# Function Name: inverse_power_method()

### Last Mod Date
February 21, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Uses inverse power iteration to find the smallest eigenvalue of a matrix.
### Inputs

* A: The matrix to be searched
* v0: An initial guess of the dominant eigenvector
* tolerance: Smallest variation between eigenvalue estimates in each iteration
* max_iters: Maximum iterations to perform before exiting

### Outputs

* lambda: The largest eigenvalue of matrix A

### Modules Used

* numpy

### Code Used

* [LU Factorization](https://swiser.github.io/MATH5620/HW2/LU_factorization)
* [LU Solve](https://swiser.github.io/MATH5620/HW2/LU_solve)
* [Power Method](https://swiser.github.io/MATH5620/HW3/power_method)

### Code

```python
def inverse_power_method(A,v0,tolerance,max_iters):
    ## Check matrix and eigenvector shapes,
    ## matrix must be square, must match the eigenvector length.
    if len(A) != len(A[0]) or len(A) != len(v0):
        print "A is {:d}x{:d}, v is {:d}x1.".format(len(A),len(A[0]),len(v0))
        print "Bad matrix/vector shapes. Exiting."
        return

    ## LU decompose A once, for fast solving of multiple eigenvector iterations
    LU,p=LU_factorization(A)
    ## Initialize variables
    n=len(v0)
    y=LU_solve(LU,p,v0)
    error=10*tolerance
    lambda_old=0.0
    count=0
    while error>tolerance and count<max_iters:
        # Calculate magnitude of v_k, normalize v_k and store as x
        y_magnitude=float(sum([y[i]**2 for i in xrange(n)])**.5)
        x=[y[i]/y_magnitude for i in xrange(n)]

        # Calculate A*v_k, store as s
        s=LU_solve(LU,p,x)

        # Calculate new lambda using v_k(transposed)*A*v_k
        lambda_new=sum([x[i]*s[i] for i in xrange(n)])
        error=abs(lambda_old-lambda_new)
        y=s
        lambda_old=lambda_new
        count+=1
    
    if error>tolerance:
        print "Maximum iterations met."
        print "took {:d} iterations".format(count)
    return 1/float(lambda_old)
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
#### Prompt

Using the same elliptic matrix from the power method example, the inverse power method was also applied. The condition number in the 2-norm is equal to the largest eigenvalue of the matrix multiplied by the largest eigenvalue of the inverse of the matrix.
 
Because the inverse power method effectively searches for 1/lambda of the inverse of the matrix, and the condition number requires the actual largest lambda of the inverse, we simply divide the result of the power method iteration by the value returned by the inverse power method. 

Each value was checked using numpy.

```python
############################################################                
##### Test power/inverse power method on elliptic matrix ###
############################################################

             
print "Elliptic ODE matrix A, Largest/Smallest eigenvalues"
print "{:^10s}|".format('Size'),
print "{:^10s}|".format('Largest'),
print "{:^10s}|".format('Smallest'),
print "{:^13s}|".format('Numpy Largest'),
print "{:^13s}|".format('Numpy Smallest'),
print "{:^13s}|".format('C Number'),
print "{:^13s}".format('Numpy C')

print "---------------------------------------------------",
print "---------------------------------------------------"

for n in xrange(2,10,1):
    guess=[(-1.0)**i for i in xrange(n)]
    elliptic=elliptic_matrix(n)
    elliptic_max_eig=power_method(elliptic,guess,10**-6,1000)
    elliptic_min_eig=inverse_power_method(elliptic,[1.0]*n,10**-6,1000)
    numpy_data=np.linalg.eig(elliptic)
    print "{:10d}|".format(n),
    print "{:10.7f}|".format(elliptic_max_eig),
    print "{:10.7f}|".format(elliptic_min_eig),
    print "{:13.7f}|".format(max(numpy_data[0],key=abs)),
    print "{:13.7f}|".format(min(numpy_data[0],key=abs)),
    print "{:13.7f}|".format(elliptic_max_eig/elliptic_min_eig),
    print "{:13.7f}|".format(np.linalg.cond(elliptic,p=2))
                         
                             
    
for n in xrange(10,51,5):
    guess=[(-1.0)**i for i in xrange(n)]
    elliptic=elliptic_matrix(n)
    elliptic_max_eig=power_method(elliptic,guess,10**-6,1000)
    elliptic_min_eig=inverse_power_method(elliptic,[1.0]*n,10**-6,1000)
    numpy_data=np.linalg.eig(elliptic)
    print "{:10d}|".format(n),
    print "{:10.7f}|".format(elliptic_max_eig),
    print "{:10.7f}|".format(elliptic_min_eig),
    print "{:13.7f}|".format(max(numpy_data[0],key=abs)),
    print "{:13.7f}|".format(min(numpy_data[0],key=abs)),
    print "{:13.7f}|".format(elliptic_max_eig/elliptic_min_eig),
    print "{:13.7f}|".format(np.linalg.cond(elliptic,p=2))
```

#### Output

```
Elliptic ODE matrix A, Largest/Smallest eigenvalues
   Size   |  Largest  |  Smallest | Numpy Largest| Numpy Smallest|   C Number   |    Numpy C   
--------------------------------------------------- ---------------------------------------------------
         2| -3.0000000| -1.0000000|    -3.0000000|    -1.0000000|     3.0000000|     3.0000000|
         3| -3.4142136| -0.5857864|    -3.4142136|    -0.5857864|     5.8284271|     5.8284271|
         4| -3.6180340| -0.3819660|    -3.6180340|    -0.3819660|     9.4721359|     9.4721360|
         5| -3.7320507| -0.2679492|    -3.7320508|    -0.2679492|    13.9282027|    13.9282032|
         6| -3.8019373| -0.1980623|    -3.8019377|    -0.1980623|    19.1956670|    19.1956694|
         7| -3.8477584| -0.1522409|    -3.8477591|    -0.1522409|    25.2741381|    25.2741424|
         8| -3.8793842| -0.1206148|    -3.8793852|    -0.1206148|    32.1634292|    32.1634375|
         9| -3.9021115| -0.0978870|    -3.9021130|    -0.0978870|    39.8634422|    39.8634582|
        10| -3.9189836| -0.0810141|    -3.9189859|    -0.0810141|    48.3741206|    48.3741501|
        15| -3.9615649| -0.0384294|    -3.9615706|    -0.0384294|   103.0867213|   103.0868689|
        20| -3.9776512| -0.0223383|    -3.9776617|    -0.0223383|   178.0638058|   178.0642746|
        25| -3.9854013| -0.0145823|    -3.9854177|    -0.0145823|   273.3049304|   273.3060574|
        30| -3.9897152| -0.0102614|    -3.9897386|    -0.0102614|   388.8098477|   388.8121345|
        35| -3.9923577| -0.0076106|    -3.9923894|    -0.0076106|   524.5783153|   524.5824763|
        40| -3.9940903| -0.0058684|    -3.9941316|    -0.0058684|   680.6100369|   680.6170700|
        45| -3.9952849| -0.0046625|    -3.9953375|    -0.0046625|   856.9046251|   856.9159094|
        50| -3.9961415| -0.0037933|    -3.9962067|    -0.0037933|  1053.4618254|  1053.4789912|
```
