

```python
import numpy as np
import matplotlib.pyplot as plt
```


```python
points = np.array([[1,1.4],[2.1,2],[2.7,3],[4.5,4.1]])
points.shape
```




    (4, 2)




```python
plt.scatter(points[:,0], points[:,1])
plt.show()
```


![png](output_2_0.png)



```python
def computDeltas ( model, point ):
    (m,b) = model; (x,y) = point
    error = x*m + b - y
    norm = np.linalg.norm([x * error, error])
    return ( error, x * error / norm, error/ norm)
```


```python
def doStep ( model, points, stepSize = 0.05 ):
    (m,b) = model
    e = 0
    for (x,y) in points:
        (_e,dm,db) = computDeltas((m,b), (x,y))
        m -= dm * stepSize * abs(_e); b -= db * stepSize * abs(_e)
        e += _e
    return (e/len(points),m,b)
```


```python
def render (errors,model) :
    (m,b) = model
    plt.scatter(points[:,0], points[:,1])
    plt.plot([0,5], [b,5*m+b], color='red')
    plt.show()
    if len(errors) is not 0:
        plt.plot(range(len(errors)), errors, color='red')
        plt.show()
```


```python
def runRandomModel ():
    model = (np.random.rand(2) - 0.5) * 3
    (m,b) = (model[0], model[1])
    errors = []
    render([], (m,b) )
    for i in range(200):
        (e,m,b) = doStep((m,b),points)
        errors.append(e**2)
    render(errors, (m,b) )
```


```python
runRandomModel()
```


![png](output_7_0.png)



![png](output_7_1.png)



![png](output_7_2.png)



```python

```


```python

```


```python

```
