# Function Name: RK_2() and RK_4()

### Last Mod Date
April 2, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description

Using Runge Kutta methods, solve the general initial value problem _u'=f(u,t), u(t0)=u0_. Both 2nd order and 4th order RK methods take the same inputs and outputs, so they are both shown on this page.

### Inputs

* u_prime: The function _u'_
* u0: The initial value for _u(t)_
* t0: The initial time value
* t_final: The final time value
* delta_t: The desired time increment to step forward with

### Outputs

* u_new: The _u(t)_ value at the final time

### Modules Used

* None


### Code

```python
def RK_2(u_prime, u0, t0,t_final,delta_t):
    time=t0
    u_old=u0
    u_new=u0
    while(time<t_final):
        u_star=u_old+.5*delta_t*u_prime(u_old,time)
        u_new=u_old+delta_t*u_prime(u_star,time+delta_t/2.0)
        u_old=u_new
        time+=delta_t
    return u_new

def RK_4(u_prime, u0, t0,t_final,delta_t):
    time=t0
    u_old=u0
    u_new=u0
    while(time<t_final):
        k1=delta_t*u_prime(u_old,time)
        k2=delta_t*u_prime(u_old+0.5*k1,time+0.5*delta_t)
        k3=delta_t*u_prime(u_old+0.5*k2,time+0.5*delta_t)
        k4=delta_t*u_prime(u_old+k3,time+delta_t)
        
        u_new=u_old+(1/6.0)*(k1+2*k2+2*k3+k4)
        u_old=u_new
        time+=delta_t
    return u_new
```


### Examples

See [Stepping Method Comparison](https://swiser.github.io/MATH5620/HW5/stepping_methods) for example prompts.



