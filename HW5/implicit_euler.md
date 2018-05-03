# Function Name: implicit_euler()

### Last Mod Date
May 3, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Using the implicit Euler method, solve the general initial value problem _u'=f(u,t), u(t0)=u0_
### Inputs

* u_prime: The function _u'_
* newton_derivative: F'(u(t_2),t_2) (see Euler Newton's Method)
* u0: The initial value for _u(t)_
* t0: The initial time value
* t_final: The final time value
* delta_t: The desired time increment to step forward with

### Outputs

* u_new: The _u(t)_ value at the final time

### Modules Used

* [Euler Newton's Method](https://swiser.github.io/MATH5620/HW5/euler_newton)


### Code

```python
def implicit_euler(u_prime,newton_derivative,u0,t0,t_final,delta_t):
    time=t0
    u_old=u0
    u_new=u0
    iterator=1
    ## u_prime is f(U_i,t_i)=U'
    ## t0 is initial time
    ## u0 is u(t0)
    ## deltaT is (t_2-t_1)
    ## Newton function is in form f(u1,u2,t1,t2)=0, implicit
    ## Newton derivative is in form f'(t1,t2,u(t2))=0
    newton_function=lambda u1,u2,t1,t2: u2-u1-(t2-t1)*u_prime(u2,t2)
    #print "IMPLICIT"
    while(time<t_final):
        if((time+delta_t)>t_final):
            delta_t=t_final-time
            u_guess=u_old+delta_t*u_prime(u_old,time)
            u_new=euler_newton(newton_function,newton_derivative,u_old,u_guess,time,time+delta_t,10**-8,1000)
            return u_new


        ## Base Newton guess on explicit Euler
        u_guess=u_old+delta_t*u_prime(u_old,time)
        u_new=euler_newton(newton_function,newton_derivative,u_old,u_guess,time,time+delta_t,10**-8,1000)
        #print "time: {:8.4f} u1={:10.8f} u2={:10.8f} deltaT={:5.4f}".format(time,u_old,u_new,delta_t)

        u_old=u_new
        time=iterator*delta_t
        iterator+=1

    
    return u_new
```


### Examples

See [Stepping Method Comparison](https://swiser.github.io/MATH5620/HW5/stepping_methods) for example prompts.



