# Function Name: true_logistic_function()

### Last Mod Date
January 22, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Simple function for testing differential logistic function
### Inputs

* alpha: alpha coefficient
* beta: beta coefficient
* p0: *P(0)* value
* t: time value to evaluate at



### Outputs

* P(t)

### Modules Used
Math
### Code

```python
def true_logistic_function(alpha,beta,p0,t):
    A=p0/float(alpha-p0*beta)
    numerator=A*alpha*math.exp(alpha*t)
    denominator=1+A*beta*math.exp(alpha*t)
    return numerator/float(denominator)
```

### Example
#### Prompt

```python
alpha=.2
beta=3.1
p0=100.0
print 't={:5.4f}, True: {:10.5f} '.format(.01,true_logistic_function(alpha,beta,p0,.01))
```

#### Output

```
t=0.0100, True:   24.42060 
```