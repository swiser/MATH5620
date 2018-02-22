# Function Name: three_point_laplace()

### Last Mod Date
February 21, 2018
### Author
Skyler Wiser
### Written For
Python 2.7.13
### Description
Solve the given Laplace Equation on the unit square in two dimensions.
### Inputs

* n: The number of mesh intervals in the x direction
* m: The number of mesh intervals in the y direction
* function: Function that the Laplace equation is set equal to, in our case it is sin(xy),


### Outputs

* lambda: The largest eigenvalue of matrix A

### Modules Used

* import math
* import numpy as np
* from mpl_toolkits.mplot3d import Axes3D
* from matplotlib import cm
from mpl_toolkits.mplot3d import axes3d
* import matplotlib.pyplot as plt

### Code Used

* [LU Factorization](https://swiser.github.io/MATH5620/HW2/LU_factorization)
* [LU Solve](https://swiser.github.io/MATH5620/HW2/LU_solve)

### Code

```python
def three_point_laplace(n,m,function):
    
    ################################################
    ## Solves del(u)=f(x)
    ## function=f(x)
    ## n,m = number of grid elements
    ## n+1=number of x points on grid
    ## m+1=number of y points on grid
    ## boundary is assumed to be unit square (0,0) to (1,1)
    ################################################

    ## Gives an iterator value associated with i,j
    ## when counting across x values first, then y
    ## but storing in a single vector
    def x_iterator(i,j):
        return (n-1)*(j-1)+(i-1)

    delta_x=1/float(n)
    delta_y=1/float(m)
    size=(n-1)*(m-1)
    A=[[0 for row in xrange(size)] for col in xrange(size)]
    b=[0 for col in xrange(size)]
    
    ## Generate A matrix for 3-point stencil
    for j in xrange(1,m,1):
        for i in xrange(1,n,1):
            #compute row value of A[]
            x_row=x_iterator(i,j)
            #print "({:d},{:d})".format(i,j)
            
            A[x_row][x_row]=(-2.0/(delta_x**2))+(-2.0/(delta_y**2))
            
            if((i-1)>0):
                x_col=x_iterator(i-1,j)
                A[x_row][x_col]=1/(delta_x**2)

            if((i+1)<n):
                x_col=x_iterator(i+1,j)
                A[x_row][x_col]=1/(delta_x**2)
                
            if((j-1)>0):
                x_col=x_iterator(i,j-1)
                A[x_row][x_col]=1/(delta_y**2)

            if((j+1)<m):
                x_col=x_iterator(i,j+1)
                A[x_row][x_col]=1/(delta_y**2)

    
    ## Generate right hand side
    for j in xrange(1,m,1):
        for i in xrange(1,n,1):
            #compute col value for i,j
            x_col=x_iterator(i,j)
            x_value=delta_x*i
            y_value=delta_y*j
            b[x_col]=function(x_value,y_value)

    LU,p=LU_factorization(A)
    u=LU_solve(LU,p,b)
    return u
```
### Helper Code

```python
def print_matrix(A):
    rows=len(A)
    cols=len(A[0])
    for row in xrange(rows):
        print '|',
        for col in xrange(cols):
            print "{:8.2f}".format(A[row][col]),
        print '|'
    print "\n"
```

### Examples
#### Prompt

```python
m=4
n=4
delta_x=1/float(n)
delta_y=1/float(m)
u=three_point_laplace(n,m,lambda x,y:math.sin(x*y))

print "{:>6s}|{:>6s}|".format('i','j'),
print "{:>10s}|{:>10s}|".format('x value','y value'),
print "{:>10s}".format('u(x,y)')
for j in xrange(1,m,1):

    for i in xrange(1,n,1):
        cell=(n-1)*(j-1)+(i-1)
        print "{:6d}|{:6d}|".format(i,j),
        print "{:10.6f}|{:10.6f}|".format(delta_x*i,delta_y*j),
        print "{:10.7f}".format(u[cell])
```

#### Output

```
     i|     j|    x value|   y value|     u(x,y)
     1|     1|   0.250000|  0.250000| -0.0060656
     2|     1|   0.500000|  0.250000| -0.0101793
     3|     1|   0.750000|  0.250000| -0.0096062
     1|     2|   0.250000|  0.500000| -0.0101793
     2|     2|   0.500000|  0.500000| -0.0172531
     3|     2|   0.750000|  0.500000| -0.0165955
     1|     3|   0.250000|  0.750000| -0.0096062
     2|     3|   0.500000|  0.750000| -0.0165955
     3|     3|   0.750000|  0.750000| -0.0166306
```
#### Graphing Prompt

A 3-d plot was generated to help visualize the results.

```python
m=4
n=4
delta_x=1/float(n)
delta_y=1/float(m)
u=three_point_laplace(n,m,lambda x,y:math.sin(x*y))

#Generate x and y values for grid
x=[delta_x*i for i in xrange(n+1)]
y=[delta_y*j for j in xrange(m+1)]
# Mesh them into a 2-d grid to plot
x_graph,y_graph=np.meshgrid(x,y)

# Insert the u(x,y) values into a 2-d 'z' matrix
z_values=[[0.0 for i in xrange(n+1)] for j in xrange(m+1)]
for j in xrange(1,m,1):
    for i in xrange(1,n,1):
        cell=(n-1)*(j-1)+(i-1)
        z_values[j][i]=(u[cell])

fig1=plt.figure(figsize=(9,7))
ax=fig1.add_subplot(111,projection='3d')
ax.set_title('3 point stencil, 3x3 internal grid')
ax.plot_surface(x_graph,y_graph,z_values,cmap=cm.coolwarm,alpha=.5)
ax.scatter(x_graph,y_graph,z_values)
ax.set_xlabel('X axis')
ax.set_ylabel('Y axis')
ax.set_zlabel('Z axis')
plt.show()
```

#### Graphing Output
3x3 grid:

![3x3](https://swiser.github.io/MATH5620/HW3/3x3_grid.png)

5x5 grid:

![5x5](https://swiser.github.io/MATH5620/HW3/5x5_grid.png)

19x19 grid:

![19x19](https://swiser.github.io/MATH5620/HW3/19x19_grid.png)

