# Function Name: euler_newton()

### Last Mod Date
April 2, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
When the implicit Euler method is solved to equal zero, a Newton-Raphson search can be performed to solve for the next U value. This takes the form of: 

```
F(U2,t2)=0=U2-U1-delta_t*U'(U2,T2)
```

And some work by hand must be done to evaluate _F'_, where the derivative of _F_ is taken with respect to _U2_. An alternative approach can be taken if U2 can be solved for explicitly, then a new iteration scheme can be formed. This was not done for this function. Note that for certain delta_t's, this method will not work.

### Inputs
function,derivative,u1,u2,t1,t2,tolerance,max_iters

* function: The function _u(t)_
* derivative: F'(t1,t2,u(t2)) 
* u1: _u(t1)_
* u2: Guess for _u(t2)_
* t1: The initial time value
* t2: The next time value to step to
* tolerance: The smallest variation in approximations before exiting
* max_iters: The maximum iterations before exiting

### Outputs

* u_new: The _u(t2)_ value

### Modules Used

* None

### Code

```python
def euler_newton(function,derivative,u1,u2,t1,t2,tolerance,max_iters):
    error=tolerance*10
    count=0
    u_old=u2
    while error>tolerance and count<max_iters:
        u_new=u_old-function(u1,u_old,t1,t2)/float(derivative(t1,t2,u_old))
        error=abs(u_new-u_old)
        u_old=u_new
        count+=1
    return u_new
```


### Examples

See the page [Stepping Method Comparison](https://swiser.github.io/MATH5620/HW5/stepping_methods) for examples.

