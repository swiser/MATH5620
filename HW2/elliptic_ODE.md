# Function Name: elliptic_ODE()

### Last Mod Date

February 7, 2018

### Author

Skyler Wiser

### Written For

Python 2.7.13

### Description

Approximates a solution for the simple elliptic equation _u''=f(x)_, given a function and initial conditions.

### Inputs

* function: The function _f(x)_
* a,b : Left and right bounds of interval
* ua, ub: Initial condions _u(a)=ua_ and _u(b)=ub_
* n= Number of intervals on range to approximate _u(x)_

### Outputs

* u_list: A list of _u(x)_ approximations on [a,b], inclusive.

### Modules Used

* math
* [Thomas Algorithm code](https://swiser.github.io/MATH5620/HW2/Thomas_alg)

### Code

```python
def elliptic_ODE(function,a,b,ua,ub,n):
    ################################################
    ## Solves u''=f(x)
    ## function=f(x)
    ## a,b = interval bounds
    ## ua,ub = initial Dirichlet boundary condition
    ## n= number of intervals to approximate on
    ################################################

    ## n= intervals, n+1=points
    h=abs(a-b)/float(n)
    x_list=[(a+h*i) for i in xrange(n+1)]
    

    ## Form tri-diagonal system of coefficients
    upper=[1.0]*(n-2)
    lower=[1.0]*(n-2)
    diag=[-2.0]*(n-1)
    ## Generate right hand side of problem F, remove a and b
    F=[function(x)*h*h for x in x_list[1:-1]]

    ## Reattach ua and ub to first and last end conditions
    F[0]=F[0]-ua
    F[-1]=F[-1]-ub

    u_list=Thomas_alg(upper,lower,diag,F)

    ## Reattach ua and ub to u_solution
    u_list=[ua]+u_list+[ub]
    return u_list
```

### Examples
#### Prompt

```python
function= lambda x: math.sin(math.pi*x)
function_answer=lambda x: 2.5*x-math.sin(math.pi*x)/(math.pi**2)+2.5

a=0
b=1
ua=2.5
ub=5.0
n=15
x_list=[(a+abs(a-b)/float(n)*i) for i in xrange(n+1)]

ux=[function_answer(x) for x in x_list]
Ux=elliptic_ODE(function,a,b,ua,ub,n)


print "u(x) is exact solution, U(x) is approximate."
print "{:^10s}|{:^10s}|{:^10s}".format('x value', 'u(x)', 'U(x)')
print "-------------------------------"
for i in xrange(len(x_list)):
    print "{: 10.5f}|{: 10.5f}|{: 10.5f}".format(x_list[i],ux[i],Ux[i])
```

#### Output

```
u(x) is exact solution, U(x) is approximate.
 x value  |   u(x)   |   U(x)   
-------------------------------
   0.00000|   2.50000|   2.50000
   0.06667|   2.64560|   2.64552
   0.13333|   2.79212|   2.79197
   0.20000|   2.94044|   2.94023
   0.26667|   3.09137|   3.09109
   0.33333|   3.24559|   3.24527
   0.40000|   3.40364|   3.40328
   0.46667|   3.56590|   3.56553
   0.53333|   3.73257|   3.73220
   0.60000|   3.90364|   3.90328
   0.66667|   4.07892|   4.07860
   0.73333|   4.25804|   4.25776
   0.80000|   4.44044|   4.44023
   0.86667|   4.62546|   4.62530
   0.93333|   4.81227|   4.81219
   1.00000|   5.00000|   5.00000
```