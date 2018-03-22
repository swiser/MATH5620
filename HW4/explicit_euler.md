# Function Name: explicit_euler()

### Last Mod Date
March 21, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Using the explicit Euler method, solve the general initial value problem _u'=f(u,t), u(t0)=u0_
### Inputs

* function: The function _u'_
* u0: The initial value for _u(t)_
* t0: The initial time value
* t_final: The final time value
* delta_t: The desired time increment to step forward with

### Outputs

* u_final: The _u(t)_ value at the final time

### Modules Used

* None


### Code

```python
def explicit_euler(function, u0, t0,t_final,delta_t):
    time=t0
    u_old=u0
    while(time<t_final):
        u_new=u_old+delta_t*function(u_old,time)
        u_old=u_new
        time+=delta_t

    return u_new
```


### Examples
#### Prompt

Using two known _du/dt_ functions, we check how our Explicit Euler method solves for the final _u(t)_ value.

##### Prompt 1

```python
## du/dt=(t*u)/(t^2+1)
## Answer: u=u_0*sqrt(t^2+1)

function = lambda u,t: ((t*u)/float(t*t+1))
u0=15
t0=0
t_final=10
step=1
u_final=explicit_euler(function,u0,t0,t_final,step)

answer= lambda t:u0*(t*t+1)**.5
print "Timestep: {:10f} seconds".format(step)
print "From explicit_Euler():"
print "u({:5.2f})={:10.4f}   | Exact: {:10.4f}".format(t_final,u_final,answer(t_final))
```

##### Prompt 2

```python
## du/dt=u/t
## (t0 cannot be 0)
## Answer: u=(u0/t0)*t

function = lambda u,t: u/float(t)
u0=5
t0=1
t_final=6
step=1
u_final=explicit_euler(function,u0,t0,t_final,step)

answer= lambda t:(u0/float(t0))*t
print "Timestep: {:10f} seconds".format(step)
print "From explicit_Euler():"
print "u({:5.2f})={:10.4f}   | Exact: {:10.4f}".format(t_final,u_final,answer(t_final))

```

#### Output

Using different delta_t's for the first problem, we can see that smaller delta_t's get closer to the correct value. This is not needed for the second example, as _u(t)_ in this case is linear and can be approximated exactly with any delta_t.

##### First Example

```
Timestep:   1.000000 seconds
From explicit_Euler():
u(10.00)=   99.5913   | Exact:   150.7481

Timestep:   0.100000 seconds
From explicit_Euler():
u(10.00)=  146.3769   | Exact:   150.7481

Timestep:   0.010000 seconds
From explicit_Euler():
u(10.00)=  150.3062   | Exact:   150.7481

Timestep:   0.001000 seconds
From explicit_Euler():
u(10.00)=  150.7039   | Exact:   150.7481

Timestep:   0.000100 seconds
From explicit_Euler():
u(10.00)=  150.7437   | Exact:   150.7481

Timestep:   0.000010 seconds
From explicit_Euler():
u(10.00)=  150.7477   | Exact:   150.7481

Timestep:   0.000001 seconds
From explicit_Euler():
u(10.00)=  150.7481   | Exact:   150.7481
```

##### Second Example

```python
Timestep:   1.000000 seconds
From explicit_Euler():
u( 6.00)=   30.0000   | Exact:    30.0000
```

