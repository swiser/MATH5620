# Function Name: Thomas_alg()

### Last Mod Date

February 7, 2018

### Author

Skyler Wiser

### Written For

Python 2.7.13

### Description

Uses the Thomas Algorithm approach of Gauss Elimination to solve a tri-diagonal system given by 3 vectors.

### Inputs

* upper_list: List of values on the superdiagonal
* lower_list: List of values on the subdiagonal
* diagonal_list: List of values on the diagonal
* b_list: List of right-hand values in _[A]x=b_

### Outputs

* List of x values that satisfy _[A]x=b_

### Notes

The first lines of code explicitly copy the four lists into new lists, so that python doesn't pass by reference and overwrite the original lists.

The prompts are take from [this](https://swiser.github.io/MATH5620/HW2/tri_solvers) tridiagonal solver comparison.

### Code

```python
def Thomas_alg(upper_list,lower_list,diagonal_list,b_list):
    upper=[x for x in upper_list]
    lower=[x for x in lower_list]
    diag=[x for x in diagonal_list]
    b=[x for x in b_list]
    n=len(diag)
    x=[0]*n
    flop=0;

    #for a1,b1,c1 syntax: diag[k]=upper[k]=lower[k-1]
    

    #forward sweep
    upper[0]=upper[0]/float(diag[0])
    b[0]=b[0]/float(diag[0])
    flop+=2
    for k in xrange(1,n):
        if(k<n-1):
            upper[k]=upper[k]/float(diag[k]-lower[k-1]*upper[k-1])
        b[k]=(b[k]-lower[k-1]*b[k-1])/float(diag[k]-lower[k-1]*upper[k-1])
        flop+=2
        
    # back sub
    x[n-1]=b[n-1]
    flop+=1
    for k in xrange(n-2,-1,-1):
        x[k]=b[k]-upper[k]*x[k+1]
        flop+=1
    print "Size N={:d} took {:d} flops.".format(n,flop)
    return x
```

### Examples
#### Prompt

```python
n=10
upper=[4]*(n-1)
diag=[16]*n
lower=[2]*(n-1)

b=[i for i in xrange(n)]

test2=Thomas_alg(upper,lower,diag,b)

print test2[4:8]

```

#### Output

```
[0.17755026512445843, 0.22365903833417383, 0.2665887141010755, 0.32181562442861106]
```