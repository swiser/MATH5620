# Function Name: heat_equation_implicit_euler

### Last Mod Date
May 3, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description

Using implicit Euler method, solve the 1-d parabolic heat equation for constant temperature boundary conditions. A matrix is solved each timestep using the [Thomas Algorithm](https://swiser.github.io/MATH5620/HW2/Thomas_alg)

### Inputs

* x0: x-coordinate on the left boundary of _u(x,t)_
* x_final: x-coordinate on the right boundary of _u(x,t)_
* t0: The initial time value
* t_final: The final time value
* u0: Initial values for _u(x,0)_
* delta_t: mesh spacing for discretizing t
* delta_x: mesh spacing for discretizing x


### Outputs

* u_new: The final _u(x,t)_ array
* u_data: A multidimensional array of all _u(x,t)_ values, for graphing

### Modules Used

* import math
* import numpy as np
* import matplotlib.pyplot as plt


### Code

```python
def heat_equation_implicit_euler(x0,x_final,t0,f_tinal,u0,delta_t,delta_x):
    i_range=int((t_final-t0)/delta_t)
    print i_range
    n_range=int((x_final-x0)/delta_x)
    stability=delta_t/delta_x**2
    middle=n_range/2
    u_old=[cell for cell in u0]
    u_new=[cell for cell in u0]
    u_data=[]
    if n_range!=len(u0)-1:
        print "Initial boundary u0 doesnt match delta_x discretization"
        return

    for i in xrange(i_range):
        ## Iterate over every time, predict next time value
        time=i*delta_t+t0

        coeff=delta_t/float(delta_x**2)
        upper_diag=[-coeff]*(n_range-2)
        lower_diag=[-coeff]*(n_range-2)
        diag=[1+2.0*coeff]*(n_range-1)
        b=u_old[1:-1]
        b[0]+=coeff*u0[0]
        b[-1]+=coeff*u0[-1]

        u_new[1:-1]=Thomas_alg(upper_diag,lower_diag,diag,b)
            

        u_data.append([item for item in u_old])
            
        u_old=[cell for cell in u_new]
        
    return u_new, u_data
```


### Example Prompts

A course, 11 point mesh from 0 to 1 is used:

```python
fig1=plt.figure(1,figsize=(11,7))

## Set all u(x,0) values to 0.0
## Set left boundary to 100 degrees
## Set right boundary to 45 degrees
u0=[0.0]*11
u0[0]=100.0
u0[-1]=45.0
t0=0
t_final=.4
x0=0
x_final=1



#Set delta x and t
delta_t=.001
delta_x=.1

## Calculate results
u2,u_data=heat_equation_implicit_euler(x0,x_final,t0,t_final,u0,delta_t,delta_x)
xvals=np.arange(0,1+delta_x,delta_x)

## Graph 10 results from t0 to t_final
divisions=10
for i in xrange(divisions):
    plt.plot(xvals,u_data[i*len(u_data)/divisions],label='u({:5.3f})'.format(i*len(u_data)/divisions*delta_t))
plt.plot(xvals,u_data[-1],label='u({:5.3f})'.format(len(u_data)*delta_t))
            
fig1.suptitle("Temp vs time\nImplicit Euler Method\ndel_T: 0.001 del_x: 0.1")
plt.xlabel('x')
plt.ylabel('Temp')
plt.legend(loc='best')
plt.show()

```

A finer, 101 point mesh from 0 to 1 is also used:

```python
fig1=plt.figure(1,figsize=(11,7))

## Set all u(x,0) values to 0.0
## Set left boundary to 100 degrees
## Set right boundary to 45 degrees
u0=[0.0]*101
u0[0]=100.0
u0[-1]=45.0
t0=0
t_final=.4
x0=0
x_final=1



#Set delta x and t
delta_t=.001
delta_x=.01

## Calculate results
u2,u_data=heat_equation_implicit_euler(x0,x_final,t0,t_final,u0,delta_t,delta_x)
xvals=np.arange(0,1+delta_x,delta_x)

## Graph 10 results from t0 to t_final
divisions=10
for i in xrange(divisions):
    plt.plot(xvals,u_data[i*len(u_data)/divisions],label='u({:5.3f})'.format(i*len(u_data)/divisions*delta_t))
plt.plot(xvals,u_data[-1],label='u({:5.3f})'.format(len(u_data)*delta_t))
            
fig1.suptitle("Temp vs time\nImplicit Euler Method\ndel_T: 0.001 del_x: 0.01")
plt.xlabel('x')
plt.ylabel('Temp')
plt.legend(loc='best')
plt.show()
```

### Results

![coarse](https://swiser.github.io/MATH5620/HW7/implicit_euler_coarse.png)

![fine](https://swiser.github.io/MATH5620/HW7/implicit_euler_fine.png)

We can see that even with a very course time mesh, implicit still converges to the correct solution:

![fine_fail](https://swiser.github.io/MATH5620/HW7/implicit_euler_fine_test.png)




