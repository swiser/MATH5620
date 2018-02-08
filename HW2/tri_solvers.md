# TriDiag Solvers

### Last Mod Date

February 7, 2018

### Author

Skyler Wiser

### Written For

Python 2.7.13

### Description

Compare the three Tridiagonal Matrix Solvers.


### Solvers

* [LU_tridiag()](https://swiser.github.io/MATH5620/HW2/LU_tridiag)
* [Jacobi_tridiag()](https://swiser.github.io/MATH5620/HW2/Jacobi_tridiag)
* [Thomas_alg()](https://swiser.github.io/MATH5620/HW2/Thomas_alg)

### Code

```python
def Jacobi_tridiag(upper,lower,diagonal,b,tolerance,max_iters):
    error=10*tolerance
    count=0
    #initialize guess as b_vector
    x_old=[cell for cell in b]
    x_new=[cell for cell in b]
    n=len(diag)
    while error>tolerance and count<max_iters:
        # First row and last row not in loop
        x_new[0]=(b[0]-upper[0]*x_old[1])/float(diag[0])
        x_new[n-1]=(b[n-1]-lower[n-2]*x_old[n-2])/float(diag[n-1])
        # Inner rows can be looped
        for i in xrange(1,n-1,1):
            x_new[i]=(b[i]-lower[i]*x_old[i-1]-upper[i]*x_old[i+1])/float(diag[i])
        
        # Calculate L2 norm difference of x_new and x_old (Root sum square)
        # x,y map to each item in x_old and x_new, "sum" function adds all
        # squared differences that have been put into list bounded by [],
        # using list comprehension, then is square rooted at end with **.5

        error=sum([abs(x-y)**2 for x,y in zip(x_old,x_new)])**.5
        x_old=x_new[:]
        count+=1
    return x_old
```

### Output

```python
Tridiagonal Matrix size n vs time to solve in seconds
    n     |    LU     |  Thomas   |  Jacobi   
    1000.0|   0.001151|   0.001039|   0.048116
    2000.0|   0.002187|   0.002044|   0.093872
    3000.0|   0.003064|   0.003040|   0.169357
    4000.0|   0.004201|   0.004062|   0.206804
    5000.0|   0.005168|   0.005075|   0.257444
    6000.0|   0.006053|   0.006257|   0.354213
```

### Conclusion

All three of the solvers appear to run in _O(n)_ time. This makes sense because all three solve in loops that aren't nested. This shows a large advantage to rewriting the 3 methods for cases where you have tridiagonal systems, as opposed to just forcing them through solvers you already have written such as standard Gauss Elimination.