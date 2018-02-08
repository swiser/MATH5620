# Function Name: LU_tridiag()

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
def LU_tridiag(upper_list,lower_list,diagonal_list,b_list):
    ## Deep copy all 3 lists
    upper=[x for x in upper_list]
    lower=[x for x in lower_list]
    diag=[x for x in diagonal_list]

    n=len(diag)
    
    ## Create 3 lists for LU
    ## L contains L
    ## U contains U_diag, U_superdiag
    L=[0]*(n-1)
    U_diag=[0]*n

    ## Factorize
    U_diag[0]=diag[0]
    for k in xrange(1,n,1):
        L[k-1]=lower[k-1]/float(U_diag[k-1])
        U_diag[k]=diag[k]-L[k-1]*upper[k-1]

    y=[x for x in b_list]
    

    ## Forward sub, solve for Ly=b
    for k in xrange(1,n,1):
        y[k]=y[k]-L[k-1]*y[k-1]
        
    ## Back sub, solve Ux=y
    answer=[x for x in y]

    answer[n-1]=y[n-1]/U_diag[n-1]
    for k in xrange(n-2,-1,-1):
        answer[k]=(y[k]-upper[k]*answer[k+1])/float(U_diag[k])
    return answer
```

### Examples
#### Prompt

```python
n=10
upper=[4]*(n-1)
diag=[16]*n
lower=[2]*(n-1)

b=[i for i in xrange(n)]

test1=LU_tridiag(upper,lower,diag,b)

print test1[4:8]

```

#### Output

```
[0.17755026512445843, 0.22365903833417383, 0.2665887141010755, 0.32181562442861106]
```