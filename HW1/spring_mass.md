# Function Name: spring_mass()

### Last Mod Date
January 22, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Function to solve Spring-Mass-Damper ODE
### Inputs

* r1: r1 coefficient
* r2: r2 coefficient
* y0: y(0) value
* v0: y'(0) value
* function: f(t) right hand side function
* t: time value to evaluate at



### Outputs

* y(t)

### Modules Used
Math
### Code

```python
def spring_mass(r1,r2,y0,v0,function,t):

    #y1 and y2, can be modified in future
    y1=lambda x: math.exp(r1*x)
    y2=lambda x: math.exp(r2*x)
    yprime1=lambda x: r1*math.exp(r1*x)
    yprime2=lambda x: r2*math.exp(r2*x)

    #y_particular and y_prime_particular, fill in as needed

    y_p=lambda x:x
    y_prime_particular=lambda x: x
    
    #calculate c1,c2
    determinant=float((r2-r1))
    c1=((y0-y_particular(0))+(v0-y_prime_paricular(0)))/determinant
    c2=(r1*(y0-y_particular(0))+r2*(v0-y_prime_paricular(0)))/determinant

    return c1*y1(t)+c2*y2(t)+yp(t)
```

### Example

Will be developed further as f(t), Yp, and Y'p values and ways to evaluate them are more well known. 