# Examples 7.1, 7.2 and 7.3

### Last Mod Date
May 3, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Compare different methods of solving initial value problems. 

The initial value problem given is:

```
u'(t)= -sin(t)
u(0)=1
```

which has an exact solution

```
u(t)=cos(t)
```
The following methods solving for T0=0, T_final=2:

7.1 attempts to solve directly using a numerical metho
7.2 attemps to solve by modifying the equation to be:

```
u'(t)= lambda(u-cos(t)) - sin(t)
```
 which has the same solution with the given initial condition, but has a different stability.


### Functions Used

* [Explicit Euler](https://swiser.github.io/MATH5620/HW4/explicit_euler)
* [Implicit Euler](https://swiser.github.io/MATH5620/HW5/implicit_euler)
* [Predictor-Corrector](https://swiser.github.io/MATH5620/HW5/predictor_corrector)
* [Runge Kutta](https://swiser.github.io/MATH5620/HW5/runge_kutta)

### Code

#### Explicit Euler Prompt

```python
################################
##########  Explicit ###########
################################

print "*** Explicit Euler Methods ***"
### Example 7.1 Explicit

u_prime=lambda u,t: -1.0*math.sin(t)
u0=1
delta_t=(10**-3)

estimate=explicit_euler(u_prime,u0,0,2,delta_t)
exact=math.cos(2)

print "Example 7.1, explicit Euler"
print "-cos(2) | Exact: {: 10.6f}| Euler: {: 10.6f} ".format(exact,estimate)
print " Error = {: .4e}".format(estimate-exact)


### Example 7.2 Explicit

LAMBDA=-10
u_prime=lambda u,t: LAMBDA*(u-math.cos(t))-math.sin(t)
u0=1
delta_t=(10**-3)

estimate=explicit_euler(u_prime,u0,0,2,delta_t)
exact=math.cos(2)

print "Example 7.2, explicit Euler"
print "-cos(2) | Exact: {: 10.6f} | Euler: {: 10.6f} ".format(exact,estimate)
print " Error = {: .4e}".format(estimate-exact)


### Example 7.3 Explicit

LAMBDA=-2100
u_prime=lambda u,t: LAMBDA*(u-math.cos(t))-math.sin(t)
u0=1
delta_t=(10**-3)

estimate=explicit_euler(u_prime,u0,0,2,delta_t)
exact=math.cos(2)

print "Example 7.3, explicit Euler"
print "-cos(2) | Exact: {: 10.6f} | Euler: {: .6e} ".format(exact,estimate)
print " Error = {: .4e}".format(estimate-exact)
```

#### Explicit Euler Output

```
*** Explicit Euler Methods ***
Example 7.1, explicit Euler
-cos(2) | Exact:  -0.416147| Euler:  -0.415692 
 Error =  4.5477e-04
 
Example 7.2, explicit Euler
-cos(2) | Exact:  -0.416147 | Euler:  -0.416163 
 Error = -1.6116e-05
 
Example 7.3, explicit Euler
-cos(2) | Exact:  -0.416147 | Euler: -1.452516e+76 
 Error = -1.4525e+76
 ```

We can see here that for a given lamda (stiffness), the explicit Euler method does terribly.

#### Implicit Euler Prompt

```python
################################
#########   Implicit   #########
################################


print "*** Implicit Euler ***"

### Example 7.1 Implicit

u_prime=lambda u,t: -1.0*math.sin(t)
u0=1
delta_t=(10**-3)
## Newton function: F(u2)=u2-u1-delta_t*u'2
newton_derivative= lambda t1,t2,u2:1
estimate=implicit_euler(u_prime,newton_derivative,u0,0,2,delta_t)
exact=math.cos(2)

print "Example 7.1, implicit Euler"
print "-cos(2) | Exact: {: 10.6f}| Euler: {: 10.6f} ".format(exact,estimate)
print " Error = {: .4e}".format(estimate-exact)


### Example 7.2 Implicit

LAMBDA=-10
u_prime=lambda u,t: LAMBDA*(u-math.cos(t))-math.sin(t)
u0=1
delta_t=(10**-3)

newton_derivative= lambda t1,t2,u2:1-delta_t*LAMBDA


estimate=implicit_euler(u_prime,newton_derivative,u0,0,2,delta_t)
exact=math.cos(2)

print "Example 7.2, implicit Euler"
print "-cos(2) | Exact: {: 10.6f} | Euler: {: 10.6f} ".format(exact,estimate)
print " Error = {: .4e}".format(estimate-exact)

### Example 7.3 Implicit

LAMBDA=-2100
u_prime=lambda u,t: LAMBDA*(u-math.cos(t))-math.sin(t)
u0=1
delta_t=(10**-3)

newton_derivative= lambda t1,t2,u2:1-delta_t*LAMBDA


estimate=implicit_euler(u_prime,newton_derivative,u0,0,2,delta_t)
exact=math.cos(2)

print "Example 7.3, implicit Euler"
print "-cos(2) | Exact: {: 10.6f} | Euler: {: 10.6f} ".format(exact,estimate)
print " Error = {: .4e}".format(estimate-exact)
```

#### Implicit Euler Output

```
*** Implicit Euler ***
Example 7.1, implicit Euler
-cos(2) | Exact:  -0.416147| Euler:  -0.416601 
 Error = -4.5453e-04
 
Example 7.2, implicit Euler
-cos(2) | Exact:  -0.416147 | Euler:  -0.416131 
 Error =  1.6084e-05
 
Example 7.3, implicit Euler
-cos(2) | Exact:  -0.416147 | Euler:  -0.416147 
 Error =  9.8907e-08
```

This method seems much more stable than the explicit form. But what if we decrease the timestep into the regions we know are unstable?

#### Implicit Euler, Shrinking Timestep Prompt

```python
################################
#########   Implicit   #########
################################

for delta_t in [10**-3,10**-2,10**-1,1]:

    print "*** Implicit Euler ***"
    print "Delta T:",delta_t
    ### Example 7.1 Implicit

    u_prime=lambda u,t: -1.0*math.sin(t)
    u0=1

    ## Newton function: F(u2)=u2-u1-delta_t*u'2
    newton_derivative= lambda t1,t2,u2:1
    estimate=implicit_euler(u_prime,newton_derivative,u0,0,2,delta_t)
    exact=math.cos(2)

    print "Example 7.1, implicit Euler"
    print "-cos(2) | Exact: {: 10.6f}| Euler: {: 10.6f} ".format(exact,estimate)
    print " Error = {: .4e}\n".format(estimate-exact)


    ### Example 7.2 Implicit

    LAMBDA=-10
    u_prime=lambda u,t: LAMBDA*(u-math.cos(t))-math.sin(t)
    u0=1


    newton_derivative= lambda t1,t2,u2:1-delta_t*LAMBDA


    estimate=implicit_euler(u_prime,newton_derivative,u0,0,2,delta_t)
    exact=math.cos(2)

    print "Example 7.2, implicit Euler"
    print "-cos(2) | Exact: {: 10.6f} | Euler: {: 10.6f} ".format(exact,estimate)
    print " Error = {: .4e}\n".format(estimate-exact)

    ### Example 7.3 Implicit

    LAMBDA=-2100
    u_prime=lambda u,t: LAMBDA*(u-math.cos(t))-math.sin(t)
    u0=1


    newton_derivative= lambda t1,t2,u2:1-delta_t*LAMBDA


    estimate=implicit_euler(u_prime,newton_derivative,u0,0,2,delta_t)
    exact=math.cos(2)

    print "Example 7.3, implicit Euler"
    print "-cos(2) | Exact: {: 10.6f} | Euler: {: 10.6f} ".format(exact,estimate)
    print " Error = {: .4e}".format(estimate-exact)
    print "\n\n\n"
```

#### Implicit Euler, Shrinking Timestep Output

```
*** Implicit Euler ***
Delta T: 0.001
Example 7.1, implicit Euler
-cos(2) | Exact:  -0.416147| Euler:  -0.416601 
 Error = -4.5453e-04

Example 7.2, implicit Euler
-cos(2) | Exact:  -0.416147 | Euler:  -0.416131 
 Error =  1.6084e-05

Example 7.3, implicit Euler
-cos(2) | Exact:  -0.416147 | Euler:  -0.416147 
 Error =  9.8907e-08




*** Implicit Euler ***
Delta T: 0.01
Example 7.1, implicit Euler
-cos(2) | Exact:  -0.416147| Euler:  -0.420682 
 Error = -4.5347e-03

Example 7.2, implicit Euler
-cos(2) | Exact:  -0.416147 | Euler:  -0.415987 
 Error =  1.5937e-04

Example 7.3, implicit Euler
-cos(2) | Exact:  -0.416147 | Euler:  -0.416146 
 Error =  9.8257e-07




*** Implicit Euler ***
Delta T: 0.1
Example 7.1, implicit Euler
-cos(2) | Exact:  -0.416147| Euler:  -0.460431 
 Error = -4.4285e-02

Example 7.2, implicit Euler
-cos(2) | Exact:  -0.416147 | Euler:  -0.414699 
 Error =  1.4478e-03

Example 7.3, implicit Euler
-cos(2) | Exact:  -0.416147 | Euler:  -0.416138 
 Error =  9.1680e-06




*** Implicit Euler ***
Delta T: 1
Example 7.1, implicit Euler
-cos(2) | Exact:  -0.416147| Euler:  -0.750768 
 Error = -3.3462e-01

Example 7.2, implicit Euler
-cos(2) | Exact:  -0.416147 | Euler:  -0.415015 
 Error =  1.1314e-03

Example 7.3, implicit Euler
-cos(2) | Exact:  -0.416147 | Euler:  -0.416124 
 Error =  2.2356e-05
```

We can see that the implicit method still holds up fairly well, for giant timesteps.

#### Predictor Corrector Method Prompt

```python
################################
####  Predictor Corrector   ####
################################

print "*** Predictor Corrector ***"
### Example 7.1 Implicit

u_prime=lambda u,t: -1.0*math.sin(t)
u0=1
delta_t=(10**-3)

estimate=adams_moulton3(u_prime, u0, 0,2,delta_t)
exact=math.cos(2)

print "Example 7.1, Predictor Corrector"
print "-cos(2) | Exact: {: 10.6f}| PC: {: 10.6f} ".format(exact,estimate)
print " Error = {: .4e}\n".format(estimate-exact)


### Example 7.2 Implicit

LAMBDA=-10
u_prime=lambda u,t: LAMBDA*(u-math.cos(t))-math.sin(t)
u0=1
delta_t=(10**-3)

estimate=adams_moulton3(u_prime, u0, 0,2,delta_t)
exact=math.cos(2)

print "Example 7.2, Predictor Corrector"
print "-cos(2) | Exact: {: 10.6f} | PC: {: 10.6f} ".format(exact,estimate)
print " Error = {: .4e}\n".format(estimate-exact)

### Example 7.3 Implicit

LAMBDA=-2100
u_prime=lambda u,t: LAMBDA*(u-math.cos(t))-math.sin(t)
u0=1
delta_t=(10**-3)


estimate=adams_moulton3(u_prime, u0, 0,2,delta_t)
exact=math.cos(2)

print "Example 7.3, Predictor Corrector"
print "-cos(2) | Exact: {: 10.6f} | PC: {: .6e} ".format(exact,estimate)
print " Error = {: .4e}".format(estimate-exact)
print "\n\n\n"
```

#### Predictor Corrector Output

```
*** Predictor Corrector ***
Example 7.1, Predictor Corrector
-cos(2) | Exact:  -0.416147| PC:  -0.816287 
 Error = -4.0014e-01

Example 7.2, Predictor Corrector
-cos(2) | Exact:  -0.416147 | PC:  -0.506983 
 Error = -9.0836e-02

Example 7.3, Predictor Corrector
-cos(2) | Exact:  -0.416147 | PC:  2.826734e+291 
 Error =  2.8267e+291
```

We can see here that the same problems with explicit Euler find their way into the explicit predictor step of the Adams-Bashforth.

#### RK4 Prompt

```python
################
####  RK4   ####
################

print "*** RK4 ***"
### Example 7.1 Implicit

u_prime=lambda u,t: -1.0*math.sin(t)
u0=1
delta_t=(10**-3)

estimate=RK_4(u_prime, u0, 0,2,delta_t)
exact=math.cos(2)

print "Example 7.1, RK4"
print "-cos(2) | Exact: {: 10.6f}| RK4: {: 10.6f} ".format(exact,estimate)
print " Error = {: .4e}\n".format(estimate-exact)


### Example 7.2 Implicit

LAMBDA=-10
u_prime=lambda u,t: LAMBDA*(u-math.cos(t))-math.sin(t)
u0=1
delta_t=(10**-3)

estimate=RK_4(u_prime, u0, 0,2,delta_t)
exact=math.cos(2)

print "Example 7.2, RK4"
print "-cos(2) | Exact: {: 10.6f} | RK4: {: 10.6f} ".format(exact,estimate)
print " Error = {: .4e}\n".format(estimate-exact)

### Example 7.3 Implicit

LAMBDA=-2100
u_prime=lambda u,t: LAMBDA*(u-math.cos(t))-math.sin(t)
u0=1
delta_t=(10**-3)


estimate=RK_4(u_prime, u0, 0,2,delta_t)
exact=math.cos(2)

print "Example 7.3, RK4"
print "-cos(2) | Exact: {: 10.6f} | RK4: {: 10.6f} ".format(exact,estimate)
print " Error = {: .4e}".format(estimate-exact)
print "\n\n\n"
```

#### RK4 Output

```
*** RK4 ***
Example 7.1, RK4
-cos(2) | Exact:  -0.416147| RK4:  -0.416147 
 Error =  3.8858e-16

Example 7.2, RK4
-cos(2) | Exact:  -0.416147 | RK4:  -0.416147 
 Error =  3.6909e-13

Example 7.3, RK4
-cos(2) | Exact:  -0.416147 | RK4:  -0.416147 
 Error =  6.3732e-08
```

With the given timestep, RK4 performs very well.



