# Function Name: problem9()

### Last Mod Date

February 7, 2018

### Author

Skyler Wiser

### Written For

Python 2.7.13

### Description

Code to solve Problem 9 from Homework 2. This consists of an elliptic ODE as described in [this](https://swiser.github.io/MATH5620/HW2/Problem9.pdf) document.

### Inputs

* function: The function _f(x)_
* a,b : Left and right bounds of interval
* ua, ub: Initial condions _u(a)=ua_ and _u(b)=ub_
* n= Number of intervals on range to approximate _u(x)_
* k= List of k(x) values

### Outputs

* u_list: A list of _u(x)_ approximations on [a,b], inclusive.

### Modules Used

* math
* [Thomas Algorithm code](https://swiser.github.io/MATH5620/HW2/Thomas_alg)
* [Elliptic ODE Setup](https://swiser.github.io/MATH5620/HW2/Problem9.pdf)


### Code

```python
def problem9(function,a,b,ua,ub,n,k):
    ################################################
    ## Solves k(x)*u''=f(x)
    ## function=f(x)
    ## a,b = interval bounds
    ## ua,ub = initial Dirichlet boundary condition
    ## n= number of intervals to approximate on
    ## k= list of k(x) values 
    ################################################

    ## n= intervals, n+1=points
    h=abs(a-b)/float(n)
    x_list=[(a+h*i) for i in xrange(n+1)]
    
    ## Form tri-diagonal system of coefficients
    upper=[]
    lower=[]
    diag=[]
    ## Initialize diagonal and superdiagonal vectors with x(a+1)
    diag.append(-2.0*k[1]/(h*h))
    upper.append(k[1]/float(h*h)+(k[2]-k[0])/(2.0*h))
    ## Fill in x(a+1) to x(b-2) values
    for j in xrange(2,n-1,1):
        diag.append(-2.0*k[j]/(h*h))
        upper.append(k[j]/float(h*h)+(k[j+1]-k[j-1])/(2.0*h))
        lower.append(k[j]/float(h*h)-(k[j+1]-k[j-1])/(2.0*h))
    ## Finish vectors by adding x(b-1) row to diagonal and subdiag
    diag.append(-2.0*k[n-1]/(h*h))    
    lower.append(k[n-1]/float(h*h)-(k[n]-k[n-2])/(2.0*h))
        
    ## Generate right hand side of problem F, remove a and b
    F=[function(x)for x in x_list[1:-1]]

    ## Reattach ua and ub to first and last end conditions
    F[0]=F[0]-ua*(k[1]/float(h*h)-(k[2]-k[0])/(2.0*h))
    F[-1]=F[-1]-ub*(k[n-1]/float(h*h)+(k[n]-k[n-2])/(2.0*h))

    u_list=Thomas_alg(upper,lower,diag,F)
    
    ## Reattach ua and ub to u_solution
    u_list=[ua]+u_list+[ub]
    return u_list
```

### Examples
#### Prompt

```python
function= lambda x: math.sin(math.pi*x)
a=0
b=1
ua=2.5
ub=5.0
n=10
x_list=[(a+abs(a-b)/float(n)*i) for i in xrange(n+1)]
k_list=[random.randint(10,50) for x in x_list]

Ux=problem9(function,a,b,ua,ub,n,k_list)

print "Given f=sin(x), k(x)=ki=rand(10,50)."
print "{:^10s}|{:^10s}".format('x value','U(x)')
print "-------------------------------"
for i in xrange(len(x_list)):
    print "{: 10.5f}|{: 10.5f}".format(x_list[i],Ux[i])
```

#### Output

```
Given f=sin(x), k(x)=ki=rand(10,50).
 x value  |   U(x)   
-------------------------------
   0.00000|   2.50000
   0.10000|   2.74158
   0.20000|   2.97635
   0.30000|   3.21390
   0.40000|   3.45931
   0.50000|   3.71942
   0.60000|   3.98175
   0.70000|   4.23714
   0.80000|   4.47675
   0.90000|   4.72157
   1.00000|   5.00000
```