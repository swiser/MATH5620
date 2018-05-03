# Function Name: heat_equation_predictor_corrector()

### Last Mod Date
May 3, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description

Using the Adams-Bashforth/Adams-Moulton predictor-corrector method, solve the 1-d parabolic heat equation for constant temperature boundary conditions.

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
def heat_equation_predictor_corrector(x0,x_final,t0,f_tinal,u0,delta_t,delta_x):
    i_range=int((t_final-t0)/delta_t)
    n_range=int((x_final-x0)/delta_x)
    stability=delta_t/delta_x**2
    middle=n_range/2
    ## Generate U arrays for RK4 startup
    u_old=[cell for cell in u0]
    u_new=[cell for cell in u0]

    ## Set up pseudo uprime for timestepping
    u_prime=lambda u1,u2,u3: delta_t/(delta_x**2)*(u1-2*u2+u3)
    
    ## Convert u0 into function-evaluated
    u_func=[cell for cell in u0]
    for n in xrange(1,n_range,1):
        u_func[n]=u_prime(u0[n-1],u0[n],u0[n+1])
    
    ## Make an array of U arrays u[0]-u[3] for predictor/corrector functions
    u_pc=[]
    u_pc.append([cell for cell in u_func])
    u_pc.append([cell for cell in u_old])
    u_pc.append([cell for cell in u_old])
    u_pc.append([cell for cell in u_old])
    u_pc.append([cell for cell in u_old])
       
    ## Make array to store predicted value
    u_4=[cell for cell in u0]
    
    u_data=[]
    u_data.append([item for item in u0])
    if n_range!=len(u0)-1:
        print "Initial boundary u0 doesnt match delta_x discretization"
        return
    if delta_t/delta_x**2>=0.5:
        print "WARNING, UNSTABLE TIMESTEP"
        
    for i in xrange(i_range):
        if(i<3):
            ## Generate 4 startup numbers
            ## Iterate over every time, predict next time value
            time=i*delta_t+t0
            k1=[0.0]*(n_range+1)
            k2=[0.0]*(n_range+1)
            k3=[0.0]*(n_range+1)
            k4=[0.0]*(n_range+1)
        
            for n in xrange(1,n_range,1):
                ## Generate all k1's
                k1[n]=u_prime(u_old[n-1],u_old[n],u_old[n+1])
            for n in xrange(1,n_range,1):
                ## Generate all k2's
                k2[n]=u_prime(u_old[n-1]+0.5*k1[n-1],u_old[n]+0.5*k1[n],u_old[n+1]+0.5*k1[n+1])
            for n in xrange(1,n_range,1):
                ## Generate all k3's
                k3[n]=u_prime(u_old[n-1]+0.5*k2[n-1],u_old[n]+0.5*k2[n],u_old[n+1]+0.5*k2[n+1])
            for n in xrange(1,n_range,1):
                ## Generate all k4's
                k4[n]=u_prime(u_old[n-1]+k3[n-1],u_old[n]+k3[n],u_old[n+1]+k3[n+1])
            for n in xrange(1,n_range,1):
                ## Step all u's forward
                u_new[n]=u_old[n]+(1/6.0)*(k1[n]+2*k2[n]+2*k3[n]+k4[n])

            u_data.append([item for item in u_new])
            u_old=[cell for cell in u_new]
            for n in xrange(1,n_range,1):
                u_pc[i+1][n]=u_prime(u_new[n-1],u_new[n],u_new[n+1])
        else:
            time=i*delta_t+t0
            ## predict 5th array values
            for n in xrange(1,n_range,1):
                first=(55.0/24.0)*u_pc[3][n]
                second=(-59.0/24.0)*u_pc[2][n]
                third=(37.0/24.0)*u_pc[1][n]
                fourth=(-3.0/8.0)*u_pc[0][n]
                u_4[n]=u_new[n]+(first+second+third+fourth)
                
            for n in xrange(1,n_range,1):
                u_pc[4][n]=u_prime(u_4[n-1],u_4[n],u_4[n+1])
                
            ## Correct 5th array values
            for n in xrange(1,n_range,1):
                first=(3.0/8.0)*u_pc[4][n]
                second=(19.0/24.0)*u_pc[3][n]
                third=(-5.0/24.0)*u_pc[2][n]
                fourth=(1.0/24.0)*u_pc[1][n]
                u_4[n]=u_new[n]+(first+second+third+fourth)
            
            ## Update old values
            u_pc[0]=[cell for cell in u_pc[1]]
            u_pc[1]=[cell for cell in u_pc[2]]
            u_pc[2]=[cell for cell in u_pc[3]]
            u_pc[3]=[cell for cell in u_pc[4]]
            u_new=[cell for cell in u_4]
            ## Store values to be graphed
            u_data.append([item for item in u_4])
    
    return u_new, u_data
```


### Example Prompts

A course, 11 point mesh from 0 to 1 is used with the same timestep .001:

```python
fig1=plt.figure(1,figsize=(11,7))

## Set all u(x,0) values to 0.0
## Set left boundary to 100 degrees
## Set right boundary to 45 degrees
u0=[0.0]*11
u0[0]=100.0
u0[-1]=45.0
t0=0
t_final=.5
x0=0
x_final=1




#Set delta x and t
delta_t=10**-4
delta_x=.1

## Calculate results
u2,u_data=heat_equation_predictor_corrector(x0,x_final,t0,t_final,u0,delta_t,delta_x)
xvals=np.arange(0,1+delta_x,delta_x)

## Graph 10 results from t0 to t_final
divisions=10
for i in xrange(divisions):
    plt.plot(xvals,u_data[i*len(u_data)/divisions],label='u({:5.3f})'.format(i*len(u_data)/divisions*delta_t))
plt.plot(xvals,u_data[-1],label='u({:5.3f})'.format(len(u_data)*delta_t))
            
fig1.suptitle("Temp vs time\nPredictor-Corrector Method\ndel_T: 0.001 del_x: 0.1")
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
t_final=.5
x0=0
x_final=1




#Set delta x and t
delta_t=10**-6
delta_x=.01

## Calculate results
u2,u_data=heat_equation_predictor_corrector(x0,x_final,t0,t_final,u0,delta_t,delta_x)
xvals=np.arange(0,1+delta_x,delta_x)

## Graph 10 results from t0 to t_final
divisions=10
for i in xrange(divisions):
    plt.plot(xvals,u_data[i*len(u_data)/divisions],label='u({:5.3f})'.format(i*len(u_data)/divisions*delta_t))
plt.plot(xvals,u_data[-1],label='u({:5.3f})'.format(len(u_data)*delta_t))
            
fig1.suptitle("Temp vs time\nPredictor-Corrector Method\ndel_T: 0.000001 del_x: 0.01")
plt.xlabel('x')
plt.ylabel('Temp')
plt.legend(loc='best')
plt.show()
```

### Results

The stability of the predictor-corrector was surprisingly low, and timesteps had to be reduced for convergence.

![coarse](https://swiser.github.io/MATH5620/HW7/pc_coarse_fail.png)

![coarse](https://swiser.github.io/MATH5620/HW7/pc_coarse.png)

![fine](https://swiser.github.io/MATH5620/HW7/pc_fine.png)





