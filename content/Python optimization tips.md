---
Title: Python optimization tips
Slug: Python-optimization-tips
Date: 2017-04-07 09:50
Category: Python
Tags: Python
Author: Chih-Hsu Lin
Summary: A few tips to optimize python
---

Here I listed and timed a few tips with `%timeit` function in Jupyter notebook (iPython notebook)
##1. [List comprehension](http://treyhunner.com/2015/12/python-list-comprehensions-now-in-color/) and [dictionary comprehension](https://www.python.org/dev/peps/pep-0274/) is faster than for loop

###For loop
```
a=[1,2,3]
b=[]
%timeit for i in a: b.append(i)
1000000 loops, best of 3: 733 ns per loop
```
###List comprehension (1.4x faster)
```
a=[1,2,3]
%timeit b=[i for i in a]
1000000 loops, best of 3: 515 ns per loop
```

##2. Iterating/indexing `list` or `set` is faster than `numpy.array`
###Iterating/indexing over a numpy array
```
import numpy as np
a = np.array([1,2,3])
%timeit b=[i for i in a]
1000000 loops, best of 3: 1.49 µs per loop
%timeit a[0]
1000000 loops, best of 3: 186 ns per loop
```
###Iterating/indexing over a list (2.8x/1.6x faster)
```
a=[1,2,3]
%timeit b=[i for i in a]
1000000 loops, best of 3: 523 ns per loop
%timeit a[0]
10000000 loops, best of 3: 117 ns per loop
```

##3. To get unique element, `set` is faster than `numpy.unique`
###`numpy.unique`
```
import numpy as np
a=[1,2,3]*10000
%timeit b=np.unique(a)
1000 loops, best of 3: 1.55 ms per loop
```

###`set` (2.9x faster)
```
a=[1,2,3]*10000
%timeit b=list(set(a))
1000 loops, best of 3: 535 µs per loop
```