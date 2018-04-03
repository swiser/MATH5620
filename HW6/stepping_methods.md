# Stepping Method Comparison

### Last Mod Date
April 2, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Compare different functions capable of solving the intial value problem _u'=f(u,t), u(t0)=u0_. Many outputs are listed, and a conclusion is presented at the bottom.

### Funcitons Used

* [Explicit Euler](https://swiser.github.io/MATH5620/HW4/explicit_euler)
* [Implicit Euler](https://swiser.github.io/MATH5620/HW5/implicit_euler)
* [Runge Kutta Methods](https://swiser.github.io/MATH5620/HW5/runge_kutta)
* [Adams Bashforth/Moulton](https://swiser.github.io/MATH5620/HW5/predictor_corrector)



<img src="https://latex.codecogs.com/gif.latex?\dpi{200}&space;f(x)=\int_{x}^{y}=4=\varepsilon&space;\zeta&space;\rho&space;\beta&space;\frac{\frac{\partial&space;}{\partial&space;x}}{4}" title="f(x)=\int_{x}^{y}=4=\varepsilon \zeta \rho \beta \frac{\frac{\partial }{\partial x}}{4}" />


### Problem 1

#### Problem 1, Example Input

The following code was used multiple times. Using different initial values, and testing different points in the for loop, some examples of stability/accuracy can be seen. The predictor-corrector is used in condition 3, but was left out for much of problem 1 due to delta_t being too large to find 3 startup values between T0 and T_Final on the intervals tested. 

```python
## First test problem
t0=0
alpha=100
gamma=-100
deltaT=.001

u_prime=lambda u_eq,time_eq : gamma*u_eq
newton_derivative= lambda t1,t2,u2:1-(t2-t1)*gamma
u_exact=lambda alpha_eq,gamma_eq,t_eq: alpha_eq*math.exp(gamma_eq*t_eq)

print "Problem 1"
print "Conditions: alpha={:<8.3f} gamma={:<8.3f} delta_t={:<8.3f}".format(alpha,gamma,deltaT)
print "{:7s} | {:^9s} | {:^9s} | {:^9s} | {:^9s} | {:^9s}".format('u(t)','Exact','Explicit','Implicit','RK2','RK4')
for t_final in [.01,.02,.03,.04,.05]:
    u_explicit=explicit_euler(u_prime,alpha,t0,t_final,deltaT)
    u_implicit=implicit_euler(u_prime,newton_derivative,alpha,t0,t_final,deltaT)
    u_rk2=RK_2(u_prime,alpha,t0,t_final,deltaT)
    u_rk4=RK_4(u_prime,alpha,t0,t_final,deltaT)
    print "u({:4.2f}) | {:9.4f} |".format(t_final,u_exact(alpha,t_final,gamma)),
    print "{:9.4f} | {:9.4f} |".format(u_explicit,u_implicit),
    print "{:9.4f} | {:9.4f} |".format(u_rk2,u_rk4)
```

#### Problem 1 Condition 1

```python
Problem 1
Conditions: alpha=10.000   gamma=1.000    delta_t=0.010   
u(t)    |   Exact   | Explicit  | Implicit  |    RK2    |    RK4   
u(0.50) |   16.4872 |   16.4463 |   16.5288 |   16.4871 |   16.4872 |
u(1.00) |   27.1828 |   27.0481 |   27.3200 |   27.1824 |   27.1828 |
u(1.50) |   44.8169 |   44.4842 |   45.1566 |   44.8158 |   44.8169 |
u(2.00) |   73.8906 |   73.1602 |   74.6382 |   73.8881 |   73.8906 |
u(2.50) |  121.8249 |  121.5248 |  124.6138 |  123.0442 |  123.0493 |
u(3.00) |  200.8554 |  199.8635 |  205.9712 |  202.8639 |  202.8740 |
```

```python
Problem 1
Conditions: alpha=10.000   gamma=1.000    delta_t=0.200   
u(t)    |   Exact   | Explicit  | Implicit  |    RK2    |    RK4   
u(0.50) |   16.4872 |   17.2800 |   19.5312 |   18.1585 |   18.2211 |
u(1.00) |   27.1828 |   24.8832 |   30.5176 |   27.0271 |   27.1825 |
u(1.50) |   44.8169 |   42.9982 |   59.6046 |   49.0771 |   49.5294 |
u(2.00) |   73.8906 |   74.3008 |  116.4153 |   89.1165 |   90.2479 |
u(2.50) |  121.8249 |  106.9932 |  181.8989 |  132.6410 |  134.6334 |
u(3.00) |  200.8554 |  154.0702 |  284.2171 |  197.4229 |  200.8486 |
```

```python
Problem 1
Conditions: alpha=10.000   gamma=1.000    delta_t=0.400   
u(t)    |   Exact   | Explicit  | Implicit  |    RK2    |    RK4   
u(0.50) |   16.4872 |   19.6000 |   27.7778 |   21.9040 |   22.2527 |
u(1.00) |   27.1828 |   27.4400 |   46.2963 |   32.4179 |   33.1951 |
u(1.50) |   44.8169 |   38.4160 |   77.1605 |   47.9785 |   49.5182 |
u(2.00) |   73.8906 |   53.7824 |  128.6008 |   71.0082 |   73.8679 |
u(2.50) |  121.8249 |  105.4135 |  357.2245 |  155.5364 |  164.3760 |
u(3.00) |  200.8554 |  147.5789 |  595.3742 |  230.1939 |  245.2051 |
```

Notice here that the implicit method blows up:

```python
Problem 1
Conditions: alpha=10.000   gamma=1.000    delta_t=0.800   
u(t)    |   Exact   | Explicit  | Implicit  |    RK2    |    RK4   
u(0.50) |   16.4872 |   18.0000 |   50.0000 |   21.2000 |   22.2240 |
u(1.00) |   27.1828 |   32.4000 |  250.0000 |   44.9440 |   49.3906 |
u(1.50) |   44.8169 |   32.4000 |  250.0000 |   44.9440 |   49.3906 |
u(2.00) |   73.8906 |   58.3200 | 1250.0000 |   95.2813 |  109.7657 |
u(2.50) |  121.8249 |  104.9760 | 6250.0000 |  201.9963 |  243.9433 |
u(3.00) |  200.8554 |  104.9760 | 6250.0000 |  201.9963 |  243.9433 |
```

#### Problem 1 Condition 2

```python
Problem 1
Conditions: alpha=10.000   gamma=-1.000   delta_t=0.100   
u(t)    |   Exact   | Explicit  | Implicit  |    RK2    |    RK4   
u(0.50) |    6.0653 |    5.9049 |    6.2092 |    6.0708 |    6.0653 |
u(1.00) |    3.6788 |    3.1381 |    3.5049 |    3.3353 |    3.3287 |
u(1.50) |    2.2313 |    2.0589 |    2.3939 |    2.2373 |    2.2313 |
u(2.00) |    1.3534 |    1.2158 |    1.4864 |    1.3582 |    1.3534 |
u(2.50) |    0.8208 |    0.7179 |    0.9230 |    0.8245 |    0.8209 |
u(3.00) |    0.4979 |    0.4239 |    0.5731 |    0.5006 |    0.4979 |
```

```python
Problem 1
Conditions: alpha=10.000   gamma=-1.000   delta_t=0.500   
u(t)    |   Exact   | Explicit  | Implicit  |    RK2    |    RK4   
u(0.50) |    6.0653 |    5.0000 |    6.6667 |    6.2500 |    6.0677 |
u(1.00) |    3.6788 |    2.5000 |    4.4444 |    3.9062 |    3.6817 |
u(1.50) |    2.2313 |    1.2500 |    2.9630 |    2.4414 |    2.2340 |
u(2.00) |    1.3534 |    0.6250 |    1.9753 |    1.5259 |    1.3555 |
u(2.50) |    0.8208 |    0.3125 |    1.3169 |    0.9537 |    0.8225 |
u(3.00) |    0.4979 |    0.1562 |    0.8779 |    0.5960 |    0.4991 |
```

Here explicit Euler becomes virtually useless:

```python
Problem 1
Conditions: alpha=10.000   gamma=-1.000   delta_t=0.950   
u(t)    |   Exact   | Explicit  | Implicit  |    RK2    |    RK4   
u(0.50) |    6.0653 |    0.5000 |    5.1282 |    5.0125 |    3.9229 |
u(1.00) |    3.6788 |    0.0250 |    2.6298 |    2.5125 |    1.5389 |
u(1.50) |    2.2313 |    0.0250 |    2.6298 |    2.5125 |    1.5389 |
u(2.00) |    1.3534 |    0.0013 |    1.3486 |    1.2594 |    0.6037 |
u(2.50) |    0.8208 |    0.0013 |    1.3486 |    1.2594 |    0.6037 |
u(3.00) |    0.4979 |    0.0001 |    0.6916 |    0.6313 |    0.2368 |
```

#### Problem 1 Condition 3

The predictor-corrector wasn't added for values where delta_t was too large to obtain 3 values between T0 and T_final for multistepping. It is shown on the first example.

```python
Problem 1
Conditions: alpha=10.000   gamma=-100.000 delta_t=0.0001   
u(t)    |   Exact   | Explicit  | Implicit  |    RK2    |    RK4    |    P/C   
u(0.01) |    3.6788 |    3.6237 |    3.6605 |    3.6423 |    3.6422 |    3.6788
u(0.02) |    1.3534 |    1.3264 |    1.3533 |    1.3399 |    1.3399 |    1.3534
u(0.03) |    0.4979 |    0.4855 |    0.5003 |    0.4929 |    0.4929 |    0.4979
u(0.04) |    0.1832 |    0.1795 |    0.1868 |    0.1832 |    0.1832 |    0.1850
u(0.05) |    0.0674 |    0.0657 |    0.0691 |    0.0674 |    0.0674 |    0.0681
```

```python
Problem 1
Conditions: alpha=10.000   gamma=-100.000 delta_t=0.005   
u(t)    |   Exact   | Explicit  | Implicit  |    RK2    |    RK4   
u(0.01) |    3.6788 |    2.5000 |    4.4444 |    3.9062 |    3.6817 |
u(0.02) |    1.3534 |    0.6250 |    1.9753 |    1.5259 |    1.3555 |
u(0.03) |    0.4979 |    0.1562 |    0.8779 |    0.5960 |    0.4991 |
u(0.04) |    0.1832 |    0.0391 |    0.3902 |    0.2328 |    0.1837 |
u(0.05) |    0.0674 |    0.0049 |    0.1156 |    0.0568 |    0.0410 |
```

```python
Problem 1
Conditions: alpha=10.000   gamma=-100.000 delta_t=0.010   
u(t)    |   Exact   | Explicit  | Implicit  |    RK2    |    RK4   
u(0.01) |    3.6788 |    0.0000 |    5.0000 |    5.0000 |    3.7500 |
u(0.02) |    1.3534 |    0.0000 |    2.5000 |    2.5000 |    1.4062 |
u(0.03) |    0.4979 |    0.0000 |    1.2500 |    1.2500 |    0.5273 |
u(0.04) |    0.1832 |    0.0000 |    0.6250 |    0.6250 |    0.1978 |
u(0.05) |    0.0674 |    0.0000 |    0.3125 |    0.3125 |    0.0742 |
```



### Problem 2

#### Problem 2, Example Input

```python
##Second Test Problem
t0=0
gamma=.1
beta=.0001
P0=25400
deltaT=.01
u_prime=lambda p,t: gamma*p-beta*p*p

newton_derivative= lambda t1,t2,u2:1-(t2-t1)*gamma+2.0*(t2-t1)*beta*u2



print "Problem 2"
print "Conditions: gamma={:<8.3f} beta={:<8.4f} P0={:<8.0f} delta_t={:<8.3f}".format(gamma,beta,P0,deltaT)
print "{:8s} | {:^9s} | {:^9s} | {:^9s} | {:^9s} | {:^9s} | {:^9s}".format('u(t)','Exact','Explicit','Implicit','RK2','RK4','P/C')
for t_final in [1,5,10,15,20]:
    u_explicit=explicit_euler(u_prime,P0,t0,t_final,deltaT)
    u_implicit=implicit_euler(u_prime,newton_derivative,P0,t0,t_final,deltaT)
    u_rk2=RK_2(u_prime,P0,t0,t_final,deltaT)
    u_rk4=RK_4(u_prime,P0,t0,t_final,deltaT)
    u_predictorcorrector=adams_moulton3(u_prime,P0,t0,t_final,deltaT)
    print "u({:5.2f}) | {:9.4f} |".format(t_final,true_logistic_function(gamma,beta,P0,t_final)),
    print "{:9.4f} | {:9.4f} |".format(u_explicit,u_implicit),
    print "{:9.4f} | {:9.4f} |".format(u_rk2,u_rk4),
    print "{:9.4f} |".format(u_predictorcorrector)
```

#### Problem 2 Output

For this example all parameters were held constant, and delta_t was varied to see how each function reacted. Starting at a small size of 0.01 and increasing until 0.5, we can see how each method reacts.

```python
Problem 2
Conditions: gamma=0.100    beta=0.0001   P0=25400    delta_t=0.010   
u(t)     |   Exact   | Explicit  | Implicit  |    RK2    |    RK4    |    P/C   
u( 1.00) | 7646.0723 | 7582.1811 | 7709.2878 | 7646.7683 | 7646.0724 | 7697.2536 |
u( 5.00) | 2396.0791 | 2384.0208 | 2401.4359 | 2392.7994 | 2392.7403 | 2396.0790 |
u(10.00) | 1546.5416 | 1542.9104 | 1548.4772 | 1545.7128 | 1545.6973 | 1546.5416 |
u(15.00) | 1272.8241 | 1271.1774 | 1273.7739 | 1272.4836 | 1272.4771 | 1272.8241 |
u(20.00) | 1149.4347 | 1148.7305 | 1150.1375 | 1149.4379 | 1149.4347 | 1149.6066 |
```

```python
Problem 2
Conditions: gamma=0.100    beta=0.0001   P0=25400    delta_t=0.200   
u(t)     |   Exact   | Explicit  | Implicit  |    RK2    |    RK4    |    P/C   
u( 5.00) | 2396.0791 | 2207.0520 | 2568.1455 | 2434.3150 | 2396.1081 | 2455.7589 |
u(10.00) | 1546.5416 | 1472.2204 | 1583.1150 | 1539.4257 | 1529.9908 | 1544.2287 |
u(15.00) | 1272.8241 | 1238.9747 | 1291.0004 | 1269.9342 | 1265.9879 | 1271.8732 |
u(20.00) | 1149.4347 | 1131.4534 | 1159.6639 | 1148.0159 | 1146.0450 | 1148.9641 |
```

```python
Problem 2
Conditions: gamma=0.100    beta=0.0001   P0=25400    delta_t=0.300   
u(t)     |   Exact   | Explicit  | Implicit  |    RK2    |    RK4    |    P/C   
u( 5.00) | 2396.0791 | 2014.5509 | 2613.0405 | 2470.0576 | 2362.5644 | 2415.3559 |
u(10.00) | 1546.5416 | 1422.0985 | 1609.5513 | 1556.7904 | 1529.8111 | 1542.9150 |
u(15.00) | 1272.8241 | 1221.6876 | 1311.3079 | 1284.3051 | 1272.7502 | 1278.3391 |
u(20.00) | 1149.4347 | 1120.8629 | 1168.3805 | 1153.3409 | 1147.6920 | 1150.4155 |
```

```python
Problem 2
Conditions: gamma=0.100    beta=0.0001   P0=25400    delta_t=0.400   
u(t)     |   Exact   | Explicit  | Implicit  |    RK2    |    RK4    |    P/C   
u( 5.00) | 2396.0791 |  716.8300 | 2654.6639 | 2570.0711 | 2324.5715 | 2271.7501 |
u(10.00) | 1546.5416 |  804.3769 | 1656.4462 | 1609.1587 | 1544.6187 | 1529.9672 |
u(15.00) | 1272.8241 |  874.4723 | 1315.9682 | 1290.6304 | 1265.2184 | 1259.3444 |
u(20.00) | 1149.4347 |  921.9816 | 1169.3900 | 1154.6268 | 1142.3675 | 1139.5143 |
```

```python
Problem 2
Conditions: gamma=0.100    beta=0.0001   P0=25400    delta_t=0.410   
u(t)     |   Exact   | Explicit  | Implicit  |    RK2    |    RK4    |    P/C   
u( 5.00) | 2396.0791 |  -16.5552 | 2610.9920 | 2537.7366 | 2284.0511 | 2211.1905 |
u(10.00) | 1546.5416 |  -27.0795 | 1633.7684 | 1589.8961 | 1523.7379 | 1503.5081 |
u(15.00) | 1272.8241 |  -44.5756 | 1318.4396 | 1293.6126 | 1266.0643 | 1257.4681 |
u(20.00) | 1149.4347 |  -74.1578 | 1176.1890 | 1161.1907 | 1147.4293 | 1143.0992 |
```

```python
Problem 2
Conditions: gamma=0.100    beta=0.0001   P0=25400    delta_t=0.500   
u(t)     |   Exact   | Explicit  | Implicit  |    RK2    |    RK4    |    P/C   
u( 5.00) | 2396.0791 |      -inf | 2824.7895 | 2961.7996 | 2353.0307 | 1695.3451 |
u(10.00) | 1546.5416 |      -inf | 1684.1015 | 1674.9737 | 1535.5444 | 1331.1153 |
u(15.00) | 1272.8241 |      -inf | 1337.0816 | 1323.8845 | 1268.2900 | 1177.6818 |
u(20.00) | 1149.4347 |      -inf | 1184.3573 | 1174.3471 | 1147.1884 | 1100.7273 |
```

### Conclusion

The various functions used presented pros and cons for each. The implicit Euler, for example, was much harder to code than explicit Euler. Coming up with a tailored function and derivative to run a Newton solve on was painful and presented many places to mess up or have code singularities. That being said, explicit Euler was very unstable for both the problems given when the step size reached a certain point. 

RK2 and RK4 perform very well, but just from observation you can see that many function calls and floating point operations are done in each call of RK_4() or RK_2(). When approximating values that are 1000+ timesteps down the line, this becomes extremely expensive. The predictor-corrector method solves this problem by reusing U values that have already been computed. The code was pretty simple for both the Adams-Bashforth and Adams-Moulton steps, and as an added bonus making the algorithm non-autonomous was very easy.

It is also worth noting that increased accuracy in respect to shrinking timesteps does not always indicate increased overall accuracy. In the first problem, just from observation of the first set of conditions, there were times the RK2 method was more accurate than the RK4 method, or times where implicit Euler was much further off than implicit. Being careful not to rely on one method as the end-all be-all is important in these numerical approximations, because many things influence how the final approximation comes out.  Depending on how a given derivative behaves, certain numerical methods do a poor job even if their truncation error is finer than other methods. This appears to become less true as you force the step size smaller and smaller.
