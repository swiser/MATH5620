# Function Name: lax_wendroff()

### Last Mod Date
May 3, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description

Solve a hyperbolic, scalar advection problem using the second order Lax-Wendroff method.

```
u_t+2*u_x=0
```

### Inputs

* x0: x-coordinate on the left boundary of _u(x,t)_
* x_final: x-coordinate on the right boundary of _u(x,t)_
* t0: The initial time value
* t_final: The final time value
* u0: Initial values for _u(x,0)_
* delta_t: mesh spacing for discretizing t
* delta_x: mesh spacing for discretizing x
* scalar: The advection velocity, in our case 2


### Outputs

* u_new: The final _u(x,t)_ array
* u_data: A multidimensional array of all _u(x,t)_ values, for graphing

### Modules Used

* import math
* import numpy as np
* import matplotlib.pyplot as plt


### Code

```python
def lax_wendroff(x0,x_final,t0,t_final,u0,delta_t,delta_x,scalar):
    i_range=int((t_final-t0)/delta_t)
    n_range=int((x_final-x0)/delta_x)
    u_data=[]
    u_data.append([cell for cell in u0])
    u_old=[cell for cell in u0]
    u_new=[cell for cell in u0]
    u_half_forward=[cell for cell in u0]
    u_half_backward=[cell for cell in u0]
    if delta_t/float(delta_x)>scalar:
        print "UNSTABLE STEP SIZE"

    ## Calculate step scalar before looping
    coeff_1=scalar*delta_t/float(2*delta_x)
    coeff_2=(scalar*delta_t/float(delta_x))**2
    for i in xrange(i_range):
        
        time=t0+delta_t*i
        for n in xrange(1,n_range,1):
            u_new[n]=u_old[n]-coeff_1*(u_old[n+1]-u_old[n-1])+0.5*coeff_2*(u_old[n-1]-2*u_old[n]+u_old[n+1])
 
        u_old=[cell for cell in u_new]

        u_data.append([cell for cell in u_new])
    return u_new,u_data
```


### Example Prompts

Lax-Wendroff with a positive scalar:

```python
fig1=plt.figure(1,figsize=(11,7))
func=lambda x: math.exp(-10*(x-2)**2)

delta_t=.01
delta_x=.01
xvals=np.arange(0,10+delta_x,delta_x)

u0=[func(x) for x in xvals]


u_result,u_data=lax_wendroff(0,10,0,250,u0,delta_t,delta_x,0.5)
plt.plot(xvals,u0,label='u({:5.1f})'.format(0))
for i in [50,100,150,200]:
    plt.plot(xvals,u_data[i],label='u({:5.1f})'.format(i))

            
fig1.suptitle("Scalar Advection vs Time")
plt.xlabel('x')
plt.ylabel('u(x)')
plt.legend(loc='best')
plt.show()
```

Lax-Wendroff with a negative scalar:

```python
fig1=plt.figure(1,figsize=(11,7))
func=lambda x: math.exp(-10*(x-8)**2)

delta_t=.01
delta_x=.01
xvals=np.arange(0,10+delta_x,delta_x)

u0=[func(x) for x in xvals]


u_result,u_data=lax_wendroff(0,10,0,250,u0,delta_t,delta_x,-0.5)
plt.plot(xvals,u0,label='u({:5.1f})'.format(0))
for i in [50,100,150,200]:
    plt.plot(xvals,u_data[i],label='u({:5.1f})'.format(i))

            
fig1.suptitle("Scalar Advection vs Time")
plt.xlabel('x')
plt.ylabel('u(x)')
plt.legend(loc='best')
plt.show()
```

### Results

![Positive Scalar](https://swiser.github.io/MATH5620/HW8/lax_wendroff_positive.png)

![Negative Scalar](https://swiser.github.io/MATH5620/HW8/lax_wendroff_negative.png)




