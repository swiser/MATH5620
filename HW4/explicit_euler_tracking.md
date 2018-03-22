# Function Name: explicit_euler_tracking()

### Last Mod Date
March 21, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Using the explicit Euler method, solve the general initial value problem _u'=f(u,t), u(t0)=u0_. This method returns all values of _u(t)_ on the interval, useful for graphing or finding intermediate values on the interval.
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
def explicit_euler_tracking(function, u0, t0,t_final,delta_t):
    ## Compute n steps in time interval. If interval
    ## isn't divisible by delta_t, go past the end time
    n=int((t_final-t0)/delta_t)
    if (t0+n*delta_t<t_final):
        n+=1
    time_list=[t0+i*delta_t for i in xrange(n+1)]
    
    # Set an array of all u(t) values to zeros
    u=[0.0 for cell in time_list]
    u[0]=u0

    # Go through each timestamp in timelist, use explicit Euler to
    # Generate each value of u(t)
    for t in xrange(1,len(time_list),1):
        u[t]=u[t-1]+delta_t*function(u[t-1],time_list[t-1])
    '''
    ## Optional Print every u(t) value saved
    for i in xrange(len(time_list)):
        print "u({:5.2f})={:10.4f}   |   {:10.4f}".format(time_list[i],u[i],u0*(time_list[i]**2+1)**.5)
    '''
    '''
    ## Optional Print first and last values of u(t)
    print "u({:5.2f})={:10.4f}   |   {:10.4f}".format(time_list[0],u[0],u0*(time_list[0]**2+1)**.5)
    print "u({:5.2f})={:10.4f}   |   {:10.4f}".format(time_list[-1],u[-1],u0*(time_list[-1]**2+1)**.5)
    '''
    return u
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

u_list=explicit_euler_tracking(function,u0,t0,t_final,step)

answer= lambda t:u0*(t*t+1)**.5
print "Timestep: {:10f} seconds".format(step)

print "From explicit_euler_tracking():"
print "u({:5.2f})={:10.4f}   | Exact: {:10.4f}".format(t0,u0,answer(t0))
print "u({:5.2f})={:10.4f}   | Exact: {:10.4f}".format(t_final,u_list[-1],answer(t_final))
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

u_list=explicit_euler_tracking(function,u0,t0,t_final,step)

answer= lambda t:(u0/float(t0))*t
print "Timestep: {:10f} seconds".format(step)

print "From explicit_euler_tracking():"
print "u({:5.2f})={:10.4f}   | Exact: {:10.4f}".format(t0,u0,answer(t0))
print "u({:5.2f})={:10.4f}   | Exact: {:10.4f}".format(t_final,u_list[-1],answer(t_final))
```

#### Output

Using different delta_t's for the first problem, we can see that smaller delta_t's get closer to the correct value. This is not needed for the second example, as _u(t)_ in this case is linear and can be approximated exactly with any delta_t.




##### First Example

```
Timestep:   1.000000 seconds
From explicit_euler_tracking():
u( 0.00)=   15.0000   | Exact:    15.0000
u(10.00)=   99.5913   | Exact:   150.7481

Timestep:   0.100000 seconds
From explicit_euler_tracking():
u( 0.00)=   15.0000   | Exact:    15.0000
u(10.00)=  144.9418   | Exact:   150.7481

Timestep:   0.010000 seconds
From explicit_euler_tracking():
u( 0.00)=   15.0000   | Exact:    15.0000
u(10.00)=  150.1576   | Exact:   150.7481

Timestep:   0.001000 seconds
From explicit_euler_tracking():
u( 0.00)=   15.0000   | Exact:    15.0000
u(10.00)=  150.6890   | Exact:   150.7481

Timestep:   0.000100 seconds
From explicit_euler_tracking():
u( 0.00)=   15.0000   | Exact:    15.0000
u(10.00)=  150.7422   | Exact:   150.7481

Timestep:   0.000010 seconds
From explicit_euler_tracking():
u( 0.00)=   15.0000   | Exact:    15.0000
u(10.00)=  150.7475   | Exact:   150.7481

Timestep:   0.000001 seconds
From explicit_euler_tracking():
u( 0.00)=   15.0000   | Exact:    15.0000
u(10.00)=  150.7481   | Exact:   150.7481
```

##### Second Example

```python
Timestep:   1.000000 seconds
From explicit_euler_tracking():
u( 1.00)=    5.0000   | Exact:     5.0000
u( 6.00)=   30.0000   | Exact:    30.0000
```

