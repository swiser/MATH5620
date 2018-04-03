# Predictor-Corrector Method

### Last Mod Date
April 2, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Using a fourth order explicit Adams-Bashforth method to predict the next step, and the third order implicit Adams-Moulton method to correct, solve the initial value problem _u'=f(u,t), u(t0)=u0_
### Inputs

#### Adams Bashforth

* u_prime: The function _u'_
* u1,u2,u3,u4: Previous values of U(t)
* delta_t: The desired time increment to step forward with
* t: The time value of u5 that we are predicting

#### Adams Moulton

* u_prime: The function _u'_
* u0: The initial value for _u(t)_
* t0: The initial time value
* t_final: The final time value
* delta_t: The desired time increment to step forward with

### Outputs

* u_new: The _u(t)_ value at the final time

### Modules Used

* [Runge-Kutta 4th order method](https://swiser.github.io/MATH5620/HW5/runge_kutta)

### Notes

Using a fourth order Runge Kutta method, 3 values are initialized. This allows us to start up the multistep method, reusing previously computed values of _U_ to step forward.

### Code

```python
def adams_bashforth4(u_prime,u1,u2,u3,u4,delta_t,t):
    ## For use in predictor-corrector. Assume u1-u5 are already known.
    ## u_prime is a function of u,t
    ## t is assumed to be the time at the step you are predicting
    first=(55.0/24.0)*u_prime(u4,t-delta_t*1.0)
    second=(-59.0/24.0)*u_prime(u3,t-delta_t*2.0)
    third=(37.0/24.0)*u_prime(u2,t-delta_t*3.0)
    fourth=(-3.0/8.0)*u_prime(u1,t-delta_t*4.0)
    
    return u4+delta_t*(first+second+third+fourth)

def adams_moulton3(u_prime, u0, t0,t_final,delta_t):
    ## Initialize 4 values
    u1=u0
    u2=RK_4(u_prime, u0, t0,t0+delta_t*1.0,delta_t)
    u3=RK_4(u_prime, u0, t0,t0+delta_t*2.0,delta_t)
    u4=RK_4(u_prime, u0, t0,t0+delta_t*3.0,delta_t)
    time=t0+delta_t*4.0
    while time<t_final:
        predictor=adams_bashforth4(u_prime,u1,u2,u3,u4,delta_t,time)
        first=(3.0/8.0)*u_prime(predictor,t_final)
        second=(19.0/24.0)*u_prime(u4,t_final-delta_t*1.0)
        third=(-5.0/24.0)*u_prime(u3,t_final-delta_t*2.0)
        fourth=(1.0/24.0)*u_prime(u2,t_final-delta_t*3.0)
        u5=u4+delta_t*(first+second+third+fourth)
        u1=u2
        u2=u3
        u3=u4
        u4=u5
        time+=delta_t
        
    return u5
```


### Examples

See [Stepping Method Comparison](https://swiser.github.io/MATH5620/HW5/stepping_methods) for example prompts.



