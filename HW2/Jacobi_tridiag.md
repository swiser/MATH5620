# Function Name: Jacobi_tridiag()

### Last Mod Date

February 7, 2018

### Author

Skyler Wiser

### Written For

Python 2.7.13

### Description

Uses the Thomas Algorithm approach of Gauss Elimination to solve a tri-diagonal system given by 3 vectors.

### Inputs

* upper: List of values on the superdiagonal
* lower: List of values on the subdiagonal
* diagonal: List of values on the diagonal
* b: List of right-hand values in _[A]x=b_
* tolerance: Maximum allowable error between iterations
* max_iters: Maximum iterations before exiting function

### Outputs

* List of x values that satisfy _[A]x=b_

### Notes

The prompts are take from [this](https://swiser.github.io/MATH5620/HW2/tri_solvers) tridiagonal solver comparison.

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

### Examples
#### Prompt

```python
n=10
upper=[4]*(n-1)
diag=[16]*n
lower=[2]*(n-1)

b=[i for i in xrange(n)]

test3=Jacobi_tridiag(upper,lower,diag,b,10**-12,300)

print test3[4:8]

```

#### Output

```
[0.177550265124422, 0.22365903833415132, 0.26658871410105833, 0.32181562442860234]

```