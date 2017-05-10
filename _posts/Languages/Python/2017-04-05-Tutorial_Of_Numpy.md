---
layout: post
title: Tutorial of Numpy with Stanford python tutorial
subtitle: I will let you know the basics of Numpy.
category: Python
tags: [language, python]
permalink: /2017/04/05/Tutorial_Of_Numpy/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
---
{% include MathJax.html %}
<!--
$$
\begin{bmatrix}
aaa & b\cr
c   & ddd
\end{bmatrix}
$$
-->
<!-- <a href="http://www.codecogs.com/eqnedit.php?latex=a&space;=&space;\begin{bmatrix}&space;1&space;&&space;&&space;\\&space;&&space;&&space;\\&space;&&space;&&space;\end{bmatrix}" target="_blank"><img src="http://latex.codecogs.com/gif.latex?a&space;=&space;\begin{bmatrix}&space;1&space;&&space;&&space;\\&space;&&space;&&space;\\&space;&&space;&&space;\end{bmatrix}" title="a = \begin{bmatrix} 1 & & \\ & & \\ & & \end{bmatrix}"
/></a> -->

# Tutorial of Numpy

This is based on stanford tutorial of python. 

in here, we will look over Numpy Linbrary of python. 

If you know this Library, You will have a powerful skill about scientific computing!

So if you find something wrong in here. let me know to fix it.

Ahead of progressing Numpy, If you're not used to python, 

I recommend you to read the followings :

[Tutorial of python with Stanford tutorial of python](https://hyunyoung2.github.io/2017/04/01/Tutorial_Of_Python_In_Stanford/)

[Tutorial of python with Jump to python, open-book](https://hyunyoung2.github.io/2017/03/30/Jump_To_Python_Tutorial/)

# Numpy

 - Arrays
 - Array indexing
 - Datatypes
 - Array math
 - Broadcasting

## [Numpy](http://www.numpy.org/)

[Numpy](http://www.numpy.org/) is the funndamental package for Scientific computing with Python. i.e [NumPy](http://www.numpy.org/) is the core Library for Scientific computing. 

in particular, it provides a powerful multi-dimensional object like multi-dimensional array objects.

### Arrays

A Numpy array is a grid of value, all of the same type like the following :

<!-- example of Array -->
<div align="center">
$$
a = \begin{bmatrix}
1 & 2 & 3
\end{bmatrix}
$$
</div>

when I express the above matrix with numpy, Let's see an example code.

```python 
>>> import numpy as np
>>>                       ## Also, You can create array with a tuple of python, a = np.array((1,2,3))
>>> a = np.array([1,2,3]) ## Conversion from the different type of python strutures(e.g. list, tuple). 
                          ## Normally, I will use list structure of python.
>>> print (type(a))       ## prints "<class 'numpy.ndarray'>"
>>> print (a.shape)       ## the shape means how to make the matrix, what the matrix looks like. 
(3,)
>>> print (np.rank(a))    ## a matrix's rank, the rank means the number of dimension of the matrix.
1
>>> print (np.ndim(a))    ## As you can see, ndim is equal to rank value, 
1
>>> print (len(a.shape))  ## Also, In numpy, the rank means the length of a.shape. 
1
>>> print (a[0], a[1], a[2])
1 2 3

>>> a                     ## this shows you what the matrix look like
array([1, 2, 3])
>>> print (a)
[1 2 3]
```

As you can see **a.shape**, **np.rank(a)**, **np.ndim(a)**, and **len(a.shape)**, In Numpy, the rank is different from the rank of Linear algebra in column space of a matrix.

In linear algebra, the rank means the number of elements in a basis for column space of a matrix. You can find the meaning of what I'm saying here In [khan academy's Linear algebra.](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/null-column-space/v/dimension-of-the-column-space-or-rank)

In Numpy, the rank means the number of dimensions is the rank of the array; the shape of an array is a tuple of integers giving the size of th array along each dimension. you can also find out what I mean in [this stack overflow.](http://stackoverflow.com/questions/16997880/puzzled-on-the-ndim-from-numpy)

I will also make 2 X 3 matrix ilke the follwoing. 

<!-- example of Array -->
<div align="center">
$$
b = \begin{bmatrix}
1 & 2 & 3\cr
4 & 5 & 6
\end{bmatrix}
$$
</div>

```python
>>> import numpy as np
>>> b = np.array([[1,2,3],[4,5,6]])    ## Create 2 X 2 matrix 
>>> print (b.shape)
(2, 3)
>>> print (type(b))     ## prints "<class 'numpy.ndarray'>"
>>> print (np.rank(b))
2
>>> print (b.ndim)
2
>>> print (len(b.shape))
2
>>> b
array([[1, 2, 3],
       [4, 5, 6]])
>>> print (b)
[[1 2 3]
 [4 5 6]]
 
>>> print (b[0,0], b[0,1], b[1,0])    ## how to index arrary
1 2 4
```

**Before entering into numpy more deeply**

I think I have to organize this concept of Numpy. i.e about one-dimension array.

As You can see the above two examples. there is a little strange thing.

When you make 2 X 2 matrix, I could verify the shape of 2 X 2 matrix with **b.shape**

let's check it with code.

```python
>>> import numpy as np
>>> a = np.array([[1,2,3],[4,5,6]])
>>> a
array([[1, 2, 3],
       [4, 5, 6]])
>>> print (a)
[[1 2 3]
 [4 5 6]]
>>> a.shape
(2, 3)
```

The above **a.shape** shows me exactly what I expected about the shape of matrix **a**,that is 2 X 3 matrix like this :

$$
a = \begin{bmatrix}
1 & 2 & 3\cr
4 & 5 & 6
\end{bmatrix}
$$

But in the case of 1 X N matrix. i.e. 1 row matrix is different from what I expected about the shape of matrix like the following. 

$$
a = \begin{bmatrix}
1 & 2 & 3
\end{bmatrix}\ \ \ Looks like \ \ \ 
\vec a = \begin{bmatrix}
1 \cr 2 \cr 3
\end{bmatrix}
$$     

Like the above two matrices, when I create 1 row matrix with Numpy, Numpy thinks of 1 row matrix as column vector, the number of column X 1 matrix. 

i.e. one dimension array looks like column vector.

Let's check it with code.

```python 
>>> import numpy as np
>>> a = np.array([1,2,3])
>>> a
array([1, 2, 3])
>>> print (a)
[1 2 3]
>>> a.shape
(3,)
```

Through the above code,**a.shape**. Numpy thinks of 1 X 3 matrix as 3 X 1 column vector. 

When you print **a** matrix, evne though output looks like 1 X 3 matrix. 

When you implement **dot product**, I will need to think of it as 3 X 1 matrix or column vector in 3 dimensions.

**Also,** Numpy provides many functions to create arrays :

```python
>>> import numpy as np
>>> a = np.zeros((2,2))
>>> a
array([[ 0.,  0.],
       [ 0.,  0.]])
>>> print (a)
[[ 0.  0.]
 [ 0.  0.]]
>>> a.shape
(2, 2)
```

In the case of **np.zeros** function, All of terms in a matrix is zeros.

$$
a = \begin{bmatrix}
0 & 0 \cr
0 & 0
\end{bmatrix}
$$   

```python
>>> import numpy as np
>>> b = np.ones((1,2))
>>> b
array([[ 1.,  1.]])
>>> print (b)
[[ 1.  1.]]
>>> b.shape
(1, 2)
```
In the case of **np.ones** function, All of terms in a matrix is ones.

$$
b = \begin{bmatrix}
1 & 1 
\end{bmatrix}
$$   

```python
>>> import numpy as np
>>> c = np.full((2,2), 7)
>>> c
array([[7, 7],
       [7, 7]])
>>> print (c)
[[7 7]
 [7 7]]
>>> c.shape
(2, 2)
```

In the case of **np.full** function, all of terms in a matrix is a constant of what I want. 

$$
c = \begin{bmatrix}
7 & 7 \cr
7 & 7
\end{bmatrix}
$$   

```python 
>>> import numpy as np
>>> d = np.eye(2)
>>> d
array([[ 1.,  0.],
       [ 0.,  1.]])
>>> d.shape
(2, 2)
>>> print (d)
[[ 1.  0.]
 [ 0.  1.]]
```

In the case of **np.eye(2)** function, this creates 2 X 2 identity matrix.

$$
d = \begin{bmatrix}
1 & 0 \cr
0 & 1
\end{bmatrix}
$$ 

```python 
>>> e = np.random.random((2,2))
>>> e
array([[ 0.50650121,  0.14590102],
       [ 0.06640179,  0.21940847]])
>>> print (e)
[[ 0.50650121  0.14590102]
 [ 0.06640179  0.21940847]]
>>> e.shape
(2, 2)
```

In the case of **np.random.random** function, this fills an array with random values.

$$
e = \begin{bmatrix}
0.50650121 & 0.14590102 \cr
0.06640179 & 0.21940847
\end{bmatrix}
$$ 

you can read about other methods of array creation in [the documentation.](https://docs.scipy.org/doc/numpy/user/basics.creation.html#arrays-creation)

### Array Indexing 

Numpy offers several ways to index into arrays. 

**Slicing**

Let me create the rank 2 array with shape (3,4)

$$
a = \begin{bmatrix}
1 & 2 & 3 & 4\cr
5 & 6 & 7 & 8\cr
9 & 10 & 11 & 12\cr
\end{bmatrix}
$$ 

```python 
>>> import numpy as np
>>> a = np.array([[1,2,3,4],[5,6,7,8],[9,10,11,12]])
>>> a
array([[ 1,  2,  3,  4],
       [ 5,  6,  7,  8],
       [ 9, 10, 11, 12]])
>>> print (a)
[[ 1  2  3  4]
 [ 5  6  7  8]
 [ 9 10 11 12]]
>>> a.shape
(3, 4)
>>> a.ndim
2
```

I will use slicing to pull out the subarray consisting of the first 2 rows. that matrix is as follows :

$$
b = \begin{bmatrix}
2 & 3\cr
6 & 7\cr
\end{bmatrix}
$$

```python
>>> b = a[:2, 1:3]
>>> b
array([[2, 3],
       [6, 7]])
>>> print (b)
[[2 3]
 [6 7]]
>>> b.shape
(2, 2)
>>> b.ndim
2
>>> np.rank(b)
2
```

A slice of an entry is a view into the same data, So modifying it will modify the original array.

$$
b = \begin{bmatrix}
77 & 3\cr
6 & 7\cr
\end{bmatrix}\ \ \ means \ \ \ 
b = \begin{bmatrix}
1 & 77 & 3 & 4\cr
5 & 6 & 7 & 8\cr
9 & 10 & 11 & 12\cr
\end{bmatrix}
$$

```python
>>> print (a[0,1])
2
>>> b[0, 0] = 77
>>> b
array([[77,  3],
       [ 6,  7]])
>>> print (b)
[[77  3]
 [ 6  7]]
>>> a
array([[ 1, 77,  3,  4],
       [ 5,  6,  7,  8],
       [ 9, 10, 11, 12]])
>>> print (a)
[[ 1 77  3  4]
 [ 5  6  7  8]
 [ 9 10 11 12]]
```

I can also mix integer indexing with slicing indexing. However, doing that will yield an array of lower rank than the original array.

let's do it, first, I wil careate the following rank 2 with shape (3,4) as follows :

$$
a = \begin{bmatrix}
1 & 2 & 3 & 4\cr
5 & 6 & 7 & 8\cr
9 & 10 & 11 & 12\cr
\end{bmatrix}
$$ 

```python 
>>> import numpy as np
>>> a = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])
>>> a
array([[ 1,  2,  3,  4],
       [ 5,  6,  7,  8],
       [ 9, 10, 11, 12]])
>>> print (a)
[[ 1  2  3  4]
 [ 5  6  7  8]
 [ 9 10 11 12]]
```

there are two ways to access the data in middle row of the array.

Mixing integer indexing with slices yields lower rank than the the original array.

While using only slices yields an array of the same rank as the original array.

```python 
>>> row_r1 = a[1, :]
>>> row_r2 = a[1:2, :]
>>> print (row_r1, row_r1.shape)
[5 6 7 8] (4,)
>>> print (row_r2, row_r2.shape)
[[5 6 7 8]] (1, 4)
```

Also, when you get column of an array is the same from the above row's process. 

```python
>>> col_r1 = a[:, 1]
>>> col_r2 = a[: , 1:2]
>>> print (col_r1, col_r1.shape)
[ 2  6 10] (3,)
>>> print (col_r2, col_r2.shape)
[[ 2]
 [ 6]
 [10]] (3, 1)
```

**Integer array indexing**

When you index into numpy arrays using slicing, the resulting array view will always be a subarray of the original array. In contrast, Integer array  indexing allows you to construct arbitrary arrays using the data from another arrary.

as an example, let's make a matrix  :

$$
a = \begin{bmatrix}
1 & 2 \cr
3 & 4 \cr
5 & 6 \cr
\end{bmatrix}\ \ \ is\ said\ to\ \ \ 
a = \begin{bmatrix}
a_{00} & a_{01} \cr
a_{10} & a_{11} \cr
a_{20} & a_{21} \cr
\end{bmatrix}
$$ 

```python 
>>> import numpy as np
>>> a = np.array([[1,2],[3,4],[5,6]])
>>> a
array([[1, 2],
       [3, 4],
       [5, 6]])
>>> print (a)
[[1 2]
 [3 4]
 [5 6]]
>>> a.shape
(3, 2)
```

$$
In\ a = \begin{bmatrix}
1 & 2 \cr
3 & 4 \cr
5 & 6 \cr
\end{bmatrix},\ \ \ a[[0,1,2],[0,1,0]]\ is\  
a = \begin{bmatrix}
1 & 4 & 5
\end{bmatrix}\ \ \ from\ \ \ 
a = \begin{bmatrix}
a_{00} & 2 \cr
3 & a_{11} \cr
a_{20} & 6 \cr
\end{bmatrix}
$$ 

```python 
>>> print (a[[0,1,2],[0,1,0]])   ## [0,1,2] means the number of matrix row, 
[1 4 5]                          ## [0,1,0] means the correspoding number of the row number.
>>> print (a[[0,1,2],[0,1,0]].shape)
(3,)

>>> print (np.array([a[0,0], a[1,1], a[2,0]])) ## the above is equivalent to this array.
[1 4 5]
>>> print (np.array([a[0,0], a[1,1], a[2,0]]).shape)
(3,)

>>> print (a[[0,0], [1,1]])
[2 2]
>>> print (a[[0,0], [1,1]].shape)
(2,)
>>> print (np.array([a[0,1],a[0,1]]))
[2 2]
>>> print (np.array([a[0,1],a[0,1]]).shape)
(2,)
````

Another way to use integer array indexing : 

```python 
>>> a = np.array([[1,2,3],[4,5,6],[7,8,9],[10,11,12]])
>>> a
array([[ 1,  2,  3],
       [ 4,  5,  6],
       [ 7,  8,  9],
       [10, 11, 12]])
>>> print (a)
[[ 1  2  3]
 [ 4  5  6]
 [ 7  8  9]
 [10 11 12]]

>>> b = np.array([0,2,0,1])
>>> b
array([0, 2, 0, 1])
>>> print (b)
[0 2 0 1]
print (a[np.arange(4), b])
[ 1  6  7 11]
```

$$
In\ a = \begin{bmatrix}
1 & 2 & 3 \cr
4 & 5 & 6 \cr
7 & 8 & 9 \cr
10 & 11 & 12 \cr
\end{bmatrix}\ \ \ and\ \ \
b = \begin{bmatrix}
0 & 2 & 0 & 1 \cr
\end{bmatrix} 
$$

> a[np.arange(4), b]

$$
a[np.arange(4),b] = 
\begin{bmatrix}
1 & 6 & 7 & 11\cr
\end{bmatrix}\ \ \ From\ \ \
a = \begin{bmatrix}
a_{00} & 2 & 3 \cr
4 & 5 & a_{12} \cr
a_{30} & 8 & 9 \cr
10 & a_{31} & 12 \cr
\end{bmatrix} 
$$

**Boolean array indexing**

Boolean array indexing lets you pick out arbitrary elements of an array, Frequently this type of indexing is used to select the elements of an array that satisfy some condition.

```python
>>> import numpy as np
>>> a = np.array([[1,2],[3,4],[5,6]])       ## 2 X 3 matrix
>>> bool_idx = (a> 2)                       ## Find elements bigger than 2 in 2 X 3 matrinx
>>> print (bool_idx)                        ## bool_idx got the same shape as a, where each slot of bool_idx tells
[[False False]                              ## whether that element of a is a > 2
 [ True  True]
 [ True  True]]
>>> bool_idx.shape                          ## the shape of a is the same from the shape of bool_idx 
(3, 2)
>>> a.shape
(3, 2)
>>> print (a[bool_idx])                     ## with Bool array indexing, you construct array in rank 1, 
[3 4 5 6]                                   ## the elements of the array is a > 2 like true values in bool_idx
>>> print (a[a > 2])                        ## a [a > 2] is the same from a[bool_idx]
[3 4 5 6]
```

$$
as\ example,\ a = \begin{bmatrix}
1 & 2 \cr
3 & 4 \cr
5 & 6 \cr
\end{bmatrix},\ \ \ \ After\ (a>2)\ \ \  is\ \ \ 
\begin{bmatrix}
False & False \cr
True & True \cr
True & True \cr
\end{bmatrix}
$$

if you want to know more about indexing, you should read [the documentation](https://docs.scipy.org/doc/numpy/reference/arrays.indexing.html) 


### Datatypes

Every numpy array is a grid of element of the same type. when you create an array, Numpy tries to guess what type the elements of array are.

Functions that construct arrays usually also include an optional argument to explicilty specify the datatype.

```python
>>> import numpy as np
>>> x = np.array([1,2])
>>> print (x.dtype)
int32
>>>
>>> x = np.array([1.0, 2.0])
>>> print (x.dtype)
float64
>>>
>>> x = np.array([1,2], dtype=np.int64)
>>> print (x.dtype)
int64
```
you can read all about Numpy datatype in [the documentation](https://docs.scipy.org/doc/numpy/reference/arrays.dtypes.html)

### Array math

Basic mathematical fucntions operate elementwise on arrays, and are available both as operator overloads and as functions in the numpy module.

$$
\begin{bmatrix}
a_{00} & a_{01} \cr
a_{10} & a_{11} \cr
a_{20} & a_{21} \cr
\end{bmatrix}\ (+,-,*,/)\ 
\begin{bmatrix}
b_{00} & b_{01} \cr
b_{10} & b_{11} \cr
b_{20} & b_{21} \cr
\end{bmatrix}\ =
\begin{bmatrix}
a_{00}(+,-,*,/)b_{00} & a_{01}(+,-,*,/)b_{01} \cr
a_{10}(+,-,*,/)b_{10} & a_{11}(+,-,*,/)b_{11} \cr
a_{20}(+,-,*,/)b_{20} & a_{21}(+,-,*,/)b_{21} \cr
\end{bmatrix}
$$

Let's see sample of math code in numpy. 

```python
>>> import numpy as n
>>> x = np.array([[1,2],[3,4]], dtype=np.float64)
>>> y = np.array([[5,6],[7,8]], dtype=np.float64)
```

$$
x = \begin{bmatrix}
1 & 2 \cr
3 & 4 \cr
\end{bmatrix}\ \ \ 
y = \begin{bmatrix}
5 & 6 \cr
7 & 8 \cr
\end{bmatrix}
$$

**Elemetwise sum**

```python
>>> print (x + y)         ## operator overloading
[[  6.   8.]
 [ 10.  12.]]
>>> print (np.add(x, y))  ## function call in Numpy module
[[  6.   8.]
 [ 10.  12.]]
```

$$
\begin{bmatrix}
1. & 2. \cr
3. & 4. \cr
\end{bmatrix}\ +\ 
\begin{bmatrix}
5. & 6. \cr
7. & 8. \cr
\end{bmatrix}\  =\ 
\begin{bmatrix}
6.(1.+5.) & 8.(2.+6.) \cr
10.(3.+7.) & 12(4.+8.) \cr
\end{bmatrix}
$$

**Elementwise difference**

```python
>>> print (x-y)               ## operator overloading
[[-4. -4.]
 [-4. -4.]]
>>> print (np.subtract(x,y))  ## function call in Numpy module
[[-4. -4.]
 [-4. -4.]]
```

$$
\begin{bmatrix}
1. & 2. \cr
3. & 4. \cr
\end{bmatrix}\ \ \ -\ \ \  
\begin{bmatrix}
5. & 6. \cr
7. & 8. \cr
\end{bmatrix}\ \ \ =\ \ \
\begin{bmatrix}
-4.(1.-5.) & -4.(2.-6.) \cr
-4.(3.-7.) & -4.(4.-8.) \cr
\end{bmatrix}
$$

**Elementwise product**

```python
>>> print (x * y)                ## operation overloading
[[  5.  12.]
 [ 21.  32.]]
>>> print (np.multiply(x,y))     ## function call in Numpy module.
[[  5.  12.]
 [ 21.  32.]]
```

$$
\begin{bmatrix}
1. & 2. \cr
3. & 4. \cr
\end{bmatrix}\ \ \ *\ \ \  
\begin{bmatrix}
5. & 6. \cr
7. & 8. \cr
\end{bmatrix}\ \ \ =\ \ \
\begin{bmatrix}
5.(1.*5.) & 12.(2.*6.) \cr
21.(3.*7.) & 32.(4.*8.) \cr
\end{bmatrix}
$$

**Elementwise division**

```python 
>>> print (x / y)                 ## operation overloading
[[ 0.2         0.33333333]
 [ 0.42857143  0.5       ]]
>>> print (np.divide(x,y))        ## function call in Numpy module
[[ 0.2         0.33333333]
 [ 0.42857143  0.5       ]]
```

$$
\begin{bmatrix}
1. & 2. \cr
3. & 4. \cr
\end{bmatrix}\ \ \ /\ \ \  
\begin{bmatrix}
5. & 6. \cr
7. & 8. \cr
\end{bmatrix}\ \ \ =\ \ \
\begin{bmatrix}
0.2(1./5.) & 0.33333333(2./6.) \cr
0.42857143(3./7.) & 0.5(4./8.) \cr
\end{bmatrix}
$$


**Elementwise square root**

```python
>>> print (np.sqrt(x))
[[ 1.          1.41421356]
 [ 1.73205081  2.        ]]
```

$$
a = \begin{bmatrix}
1. & 2. \cr
3. & 4. \cr
\end{bmatrix},\ \ \ \sqrt a\ \ \ is\ \ \ 
\begin{bmatrix}
 1.(\sqrt 1.) & 1.41421356(\sqrt 2.) \cr
1.73205081(\sqrt 3.) & 2(\sqrt 4.) \cr
\end{bmatrix}
$$

In the case of the above math codes, Note that unlike MATLAB, **\*** is elementwise multiplication, not matrix multiplication. 

If you want to matrix multiplication, you stead use the **dot** function to compute inner products of vectors, to multiply a vector by a matrix, and to multiply matrices.

**dot** is available both as a function in the Numpy module and as an instance method of array objects :

```python
>>> x = np.array([[1,2],[3,4]])
>>> y = np.array([[5,6],[7,8]])
>>> v = np.array([9,10])
>>> w = np.array([11,12])
>>> print (x)
[[1 2]
 [3 4]]
>>> print (y)
[[5 6]
 [7 8]]
>>> print (v)
[ 9 10]
>>> print (w)
[11 12]
>>> x.shape
(2, 2)
>>> y.shape
(2, 2)
>>> v.shape
(2,)
>>> w.shape
(2,)
```

$$
x = \begin{bmatrix}
1 & 2 \cr
3 & 4 \cr
\end{bmatrix}\ \ \ 
y = \begin{bmatrix}
5 & 6 \cr
7 & 8 \cr
\end{bmatrix}\ \ \ 
v = \begin{bmatrix}
9 & 10 \cr
\end{bmatrix}\ \ \ 
w = \begin{bmatrix}
11 & 12 \cr
\end{bmatrix}
$$

About the above v, w arrays, let's think of those(v, w arrays) as column vectors.

**inner product of vectors OR dot product of vectors**

**vector-vector multiplication**

if both of column vectors implement **dot** product.

by definition like this.

$$
\vec a,\ \vec b\ \in\ \rm I\! R^2,\ \vec a^T\cdot\vec b\ = \begin{bmatrix}
x_1 & \dots & x_n  
\end{bmatrix}\ \begin{bmatrix}
y_1 \cr \dots \cr y_n  
\end{bmatrix}\ = \sum_{k=1}^n x_k y_k
$$

$$
sum_{k=1}^n x_k y_k\ = x_1y_1+\ x_2y_2+ \dots + x_ny_n  
$$

by the above definition, If I multiply a vector by another vector,

ahead of entering the process of vector-vector multiplication, you will have to think of **v, w** as column vector as follows :

$$
\vec v = \begin{bmatrix}
9 \cr 10 \cr
\end{bmatrix}\ \ \ 
\vec w = \begin{bmatrix}
11 \cr 12 \cr
\end{bmatrix}
$$

With above vectors. Let's do dot product as follows. 

$$
\vec v^T = \begin{bmatrix}
9 & 10 \cr
\end{bmatrix},\ 
\vec w = \begin{bmatrix}
11 \cr 12 \cr
\end{bmatrix}\ ,So\ that\ \vec v^T\cdot\vec w\ =\ 219(9*11+10*12)
$$

If you make the above dot product of two vector with numpy.


```python
>>> v.dot(w)
219
>>> np.dot(v,w)
219
```

**Matrix-vector product**

```python 
>>> x
array([[1, 2],
       [3, 4]])
>>> v
array([ 9, 10])
>>> x.dot(v)
array([29, 67])
>>> np.dot(x,v)
array([29, 67])
```

Let's see how the product between matrix and vector(column vector) is calculated.

$$
X\cdot\vec v = \begin{bmatrix}
1 & 2 \cr
3 & 4 \cr
\end{bmatrix}\cdot\begin{bmatrix}
9 \cr 10 \cr
\end{bmatrix}\ =\   \begin{bmatrix}
39(1*9+2*10) & 67(3*9+4*10) \cr
\end{bmatrix}
$$

**Matrix-Matrix product**

Let's see example of the product.

```python 
>>> x
array([[1, 2],
       [3, 4]])
>>> y
array([[5, 6],
       [7, 8]])
>>> x.dot(y)
array([[19, 22],
       [43, 50]])
>>> np.dot(x, y)
array([[19, 22],
       [43, 50]])
```

$$
X\cdot Y = \begin{bmatrix}
1 & 2 \cr
3 & 4 \cr
\end{bmatrix}\cdot\begin{bmatrix}
5 & 6 \cr
7 & 8 \cr
\end{bmatrix}\ =\ \begin{bmatrix}
19(1*5+2*7) & 22(1*6+2*8) \cr
43(3*5+4*7) & 50(3*6+4*8) \cr
\end{bmatrix}
$$

As you see the total dot product in Numpy, You will have to be careful about how numpy calculate depending on argument pair of dot product.

**Keep in mind once again, if You use dot product, one-dimesion matrix need to be thought of as column vector.**

in the case of dot producnt with column vector which is placed on firt element.

$$
\vec a^T\cdot\ (matrix\ or\ colum vector) 
$$

like the above, you need to think vector **a** as the transpose of vector **a**

**Sum function**

In addition to this, Numpy provides many useful functions for performing computations on arrays, one of the most useful is **sum**.

```python 
>>> import numpy as np
>>> x = np.array([[1,2],[3,4]])
>>>
>>> print (np.sum(x))                   ## Compute sum of all elements
10
>>> print (np.sum(x, axis=0))           ## axis = 0 is column, i.e. Compute sum of each column
[4 6]
>>> print (np.sum(x, axis=0).shape)
(2,)
>>> print (np.sum(x, axis=1))           ## axis = 1 is row, i.e. Compute sum of each row
[3 7]
>>> print (np.sum(x, axis=1).shape)
(2,)
```

> np.sum(x)

$$
X = \begin{bmatrix}
1 & 2 \cr
3 & 4 \cr
\end{bmatrix},\ \  
np.sum(x) = 10(1+2+3+4)
$$

> np.sum(x, axix = 0) ## column

$$
X = \begin{bmatrix}
1 & 2 \cr
3 & 4 \cr
\end{bmatrix},\ \  
np.sum(x,\ axis=0) = \begin{bmatrix}
4(1+3) \cr 6(2+4) \cr
\end{bmatrix}
$$

> np.sum(x, axix = 1) ## row

$$
X = \begin{bmatrix}
1 & 2 \cr
3 & 4 \cr
\end{bmatrix},\ \  
np.sum(x,\ axis=1) = \begin{bmatrix}
3(1+2) \cr 7(3+4) \cr
\end{bmatrix}
$$

You can also find out the mathematical function in [the documentation.](https://docs.scipy.org/doc/numpy/reference/routines.math.html)

Apart from computing mathematical functions using arrays, we frequently need to reshape or otherwise manipulate data in arrarys. 

The simplest example of this type of operation is transposing a matrix; to transpose a matrix, simply use the **T** attribute of an array object.

Let's see an example of code.

```python 
>>> x = np.array([[1,2],[3,4]])  
>>> print (x)
[[1 2]
 [3 4]]
>>> print (x.T)
[[1 3]
 [2 4]]
>>> v = np.array([1,2,3])        ## Note that taking the transpose of a rank 1 array does nothing in Numpy
>>> print (v)
[1 2 3]
>>> print (v.T)
[1 2 3]
```

**Transpose(T)** means exchange of the location, by changing the location of row and column. 

$$
X = \begin{bmatrix}
1 & 2 \cr
3 & 4 \cr
\end{bmatrix},\ \ \ 
X^T =  \begin{bmatrix}
1 & 3 \cr
2 & 4 \cr
\end{bmatrix}
$$

more exactly, 

$$
(X^T)_{ij} = X_{ji}
$$

I will explain to you with an example, the transpose of column vector is row vector. 

$$
\vec x = \begin{bmatrix}
x_{1} \cr
x_{2} \cr
\vdots \cr
x_{n} \cr
\end{bmatrix},\ \ \
\vec x^T = \begin{bmatrix}
x_{1} & x_{2} & \ldots & x_{n} \cr
\end{bmatrix}
$$

let's look over an example of the transpose of a rank 1 array in Numpy.

```python
>>> v = np.array([1,2,3])        ## Note that taking the transpose of a rank 1 array does nothing in Numpy
>>> print (v)
[1 2 3]
>>> print (v.T)
[1 2 3]
>>> v.shape
(3,)
>>> (v.T).shape
(3,)
```

**As you can see, there is no change in the shape of v and v.T**

You can also read about other methods of array creation in [the documentation](https://docs.scipy.org/doc/numpy/user/basics.creation.html#arrays-creation)

### Broadcasting

Broadcasting is a powerful mechanism that allows numpy to work with arrays of different shapes when performing arithmetic operations, Frequently we have a smaller array and  a larger array, and we want to use the smaller array multiple times to perform some operation on the larger array.

For example, suppose that we want to add a constant vector to each row of a matrix. We would do it like this :

```python 
>>> import numpy  as np
>>> x = np.array([[1,2,3],[4,5,6],[7,8,9],[10,11,12]])   
>>> print (x)                      ## Create 4 X 3 matrix
[[ 1  2  3]
 [ 4  5  6]
 [ 7  8  9]
 [10 11 12]]
>>> v = np.array([1,0,1])
>>> print (v)
[1 0 1]
>>> x[0]
array([1, 2, 3])
>>> x[0].shape
(3,)
>>> x[:, 1].shape
(4,)
>>> x[:, 1]
array([ 2,  5,  8, 11])
>>> y = np.empty_like(x)  ## Create an empty matrix with the same shape as matrix x
>>> print (y)
[[0 0 0]
 [0 0 0]
 [0 0 0]
 [0 0 0]]
>>> for i in range(4) :   ## Add the vector v to each row of the matrix x with an explicit loop      
...     y[i, :] = x[i, :] + v
...
>>> print (y)
[[ 2  2  4]
 [ 5  5  7]
 [ 8  8 10]
 [11 11 13]]
>>> y[0][1]               ## another way to access the element of array using y[row][colnum]
2                         ## But normally, use y[row, colum] when you access the element of an array
>>> y[0][2]
4
>>> y[0][:]
array([2, 2, 4])
```

computing with looping in python could be slow. 

Therefore, let's see another way to implement the above code. 

Before explaining another way to calculate the above code. 

let's notice about the above code

> First let's see Arrays, X, V, and Y.

$$
X = \begin{bmatrix}
1 & 2 & 3 \cr
4 & 5 & 6 \cr
7 & 8 & 9 \cr
10 & 11 & 12 \cr
\end{bmatrix},\ \ \
Y = \begin{bmatrix}
0 & 0 & 0 \cr
0 & 0 & 0 \cr
0 & 0 & 0 \cr
0 & 0 & 0 \cr
\end{bmatrix},\ \ \
V = \begin{bmatrix}
1 & 0 & 1 \cr
\end{bmatrix}\ \ \
$$

> for i in range(4) :  y[i, :] = x[i, :] + v is the same from X + VV

> y[0, :] + v

$$
X[0,:]\ +\ v = \begin{bmatrix}
1 & 2 & 3 \cr
\end{bmatrix}\ +
\begin{bmatrix}
1 & 0 & 1 \cr
\end{bmatrix}\ = \begin{bmatrix}
2(1+1) & 2(2+0) & 4(3+1) \cr
\end{bmatrix}
$$

> y[1, :] + v

$$
X[0,:]\ +\ v = \begin{bmatrix}
4 & 5 & 6 \cr
\end{bmatrix}\ +
\begin{bmatrix}
1 & 0 & 1 \cr
\end{bmatrix}\ = \begin{bmatrix}
5(4+1) & 5(5+0) & 7(6+1) \cr
\end{bmatrix}
$$

> y[2, :] + v

$$
X[0,:]\ +\ v = \begin{bmatrix}
7 & 8 & 9 \cr
\end{bmatrix}\ +
\begin{bmatrix}
1 & 0 & 1 \cr
\end{bmatrix}\ = \begin{bmatrix}
8(7+1) & 8(8+0) & 10(9+1) \cr
\end{bmatrix}
$$

> y[3, :] + v

$$
X[0,:]\ +\ v = \begin{bmatrix}
10 & 11 & 12 \cr
\end{bmatrix}\ +
\begin{bmatrix}
1 & 0 & 1 \cr
\end{bmatrix}\ = \begin{bmatrix}
11(10+1) & 11(11+0) & 13(12+1) \cr
\end{bmatrix}
$$

> Finally,  the result of "for i in range(4) :  y[i, :] = x[i, :] + v is the same from X + VV"

$$
result = \begin{bmatrix}
2 & 2 & 4 \cr
5 & 5 & 7 \cr
8 & 8 & 10 \cr
11 & 11 & 13 \cr
\end{bmatrix}
$$

From now on, let's see another way to implement the above process without for statement. 

that is making **vv** by stacking multiple copies of **v** vertically like the same shape of matrix **x**.

And then perform the sum of **x** and **vv** element by element.

> First generate VV by stacking multiple copies of v 

$$
V = \begin{bmatrix}
1 & 0 & 1 \cr
\end{bmatrix},\ \ 
VV = \begin{bmatrix}
1 & 0 & 1 \cr
1 & 0 & 1 \cr
1 & 0 & 1 \cr
1 & 0 & 1 \cr
\end{bmatrix}
$$

>> Second, x + vv

$$
X\ +\ VV = \begin{bmatrix}
1 & 2 & 3 \cr
4 & 5 & 6 \cr
7 & 8 & 9 \cr
10 & 11 & 12 \cr
\end{bmatrix}\ \ \ +\ \ \
\begin{bmatrix}
1 & 0 & 1 \cr
1 & 0 & 1 \cr
1 & 0 & 1 \cr
1 & 0 & 1 \cr
\end{bmatrix}\ \ \ =\ \ \
\begin{bmatrix}
2 & 2 & 4 \cr
5 & 5 & 7 \cr
8 & 8 & 10 \cr
11 & 11 & 13 \cr
\end{bmatrix}
$$

now is turn of making the code with Numpy.

> What can the sum of x and vv do programming in Numpy ? 

```python
>>> import numpy as np
>>> x = np.array([[1,2,3],[4,5,6],[7,8,9],[10,11,12]])
>>> v = np.array([1,0,1])
>>> vv = np.tile(v, (4,1))      ## generate vv
>>> print (vv)
[[1 0 1]
 [1 0 1]
 [1 0 1]
 [1 0 1]]
>>> print (v)
[1 0 1]
>>> y = np.empty_like(x)
>>> print (y)
[[0 0 0]
 [0 0 0]
 [0 0 0]
 [0 0 0]]
>>> y = x + vv
>>> print (y)
[[ 2  2  4]
 [ 5  5  7]
 [ 8  8 10]
 [11 11 13]]
```

Numpy broadcasting allows us to perform this computation withou actually creating multiple copies of v. 

Consider this version operation, using broadcasting.

```python 
>>> import numpy as np
>>> x = np.array([[1,2,3],[4,5,6],[7,8,9],[10,11,12]])
>>> v = np.array([1,0,1])     ## you don't need to make VV matrix. 
>>> y = np.empty_like(x)
>>> x
array([[ 1,  2,  3],
       [ 4,  5,  6],
       [ 7,  8,  9],
       [10, 11, 12]])
>>> v
array([1, 0, 1])

>>> y
array([[0, 0, 0],
       [0, 0, 0],
       [0, 0, 0],
       [0, 0, 0]])
>>> y = x + v
>>> print (y)
[[ 2  2  4]
 [ 5  5  7]
 [ 8  8 10]
 [11 11 13]]
```

As you can see the above code, if you use numpy broadcasting, it is powerful to compute arrays of different shapes array,

Numpy broadcasting automatically fit smaller shape to larger shape,and then compute. If some condition is met. 

i.e. The line **y=x+v** works even though x has shape (4,3) and v has shape (3,) due to broadcasting; this line works as if v actually had shape (4,3), where each row was a copy of v, and the sum was performed elementwise. 

> y = x + v literally means as follows.

$$
Y = X\ +\ V = \begin{bmatrix}
1 & 2 & 3 \cr
4 & 5 & 6 \cr
7 & 8 & 9 \cr
10 & 11 & 12 \cr
\end{bmatrix}\ \ \ +\ \ \
\begin{bmatrix}
1 & 0 & 1 \cr
\end{bmatrix}\ \ \ =\ \ \
\begin{bmatrix}
2 & 2 & 4 \cr
5 & 5 & 7 \cr
8 & 8 & 10 \cr
11 & 11 & 13 \cr
\end{bmatrix}
$$

> BUT, due to broadcasting, v works as if v actually had shape (4,3) as follows.

$$
Y = X\ +\ V = \begin{bmatrix}
1 & 2 & 3 \cr
4 & 5 & 6 \cr
7 & 8 & 9 \cr
10 & 11 & 12 \cr
\end{bmatrix}\ \ \ +\ \ \
\begin{bmatrix}
1 & 0 & 1 \cr
1 & 0 & 1 \cr
1 & 0 & 1 \cr
1 & 0 & 1 \cr
\end{bmatrix}\ \ \ =\ \ \
\begin{bmatrix}
2 & 2 & 4 \cr
5 & 5 & 7 \cr
8 & 8 & 10 \cr
11 & 11 & 13 \cr
\end{bmatrix}
$$

Owing to numpy broadcasting, you don't need to chang vector v into matrix vv.

If you want to know more about numpy broadcasting. try to read the explanation from [the documentation](https://docs.scipy.org/doc/numpy/user/basics.broadcasting.html) and [this explanation.](http://scipy.github.io/old-wiki/pages/EricsBroadcastingDoc)

functions that support broadcasting are know as universal functions, you can find the list of all universal functions in [the documentaion.](https://docs.scipy.org/doc/numpy/reference/ufuncs.html#available-ufuncs)

The broadcasting rule : 

> the size of each dimensions must be the same or one of them must be one!

Let's See some applicaiton of broadcasting. 

> First, Outer product

$$
\vec x\ \in \rm I\! R^n,\ \vec y\ \rm I\! R^m,\ 
\vec x \vec y^T\ \in \rm I\! R^{n*m}
$$

$$
\vec x \vec y^T\ \in \rm I\! R^{n*m}\ is\ called\ outer\ product\ of\ two\ vectors(\vec x,\ \vec y)
$$

I will implement the outer product with an actual example code.

the number of shape of array in numpy is iterally numeral on each dimension of the array. 

Especially, the shape of  1 X N matrix is noramlly (N,), but, in the broadcasting, you will have to think of it as (1, 3). 

let's example. 

```python
## Compute outer product of vectors
>>> import numpy as np    
>>> v = np.array([1,2,3])     ## v has shpae (3,)
>>> w = np.array([4,5])       ## w has shape (2,)
## In order to compute an outer product, first I will reshape vector v into (3,1)
## We can then broadcastin it against w to yeild an output of shape (3,2), which is the outer product of v and w :
##[[4 5]
## [8 10]
## [12 15]]
>>>
>>> print (np.reshape(v,(3,1)) * w)
[[ 4  5]
 [ 8 10]
 [12 15]]
>>> print ((np.reshape(v,(3,1)) * w).ndim)
2
>>> print ((np.reshape(v,(3,1)) * w).shape)
(3, 2)
```

> np.reshape(v,(3,1)) * w

$$
\vec v\ \vec w^T = \begin{bmatrix}
1 \cr
2 \cr
3 \cr
\end{bmatrix}
\begin{bmatrix}
4 & 5 \cr
\end{bmatrix}\ = \ 
\begin{bmatrix}
4(1*4) & 5(1*5) \cr
8(2*4) & 10(2*5) \cr
12(3*4) & 15(3*5) \cr
\end{bmatrix}\ \ \
$$

> Another Broadcasting, v + x that v has shape (3,) and x has shape (2,3)

```python
## Add a vector to each row of a matrix
>>> import numpy as np
>>> v = np.array([1,2,3])
>>> x = np.array([[1,2,3],[4,5,6]])      ## X has shape (2,3) and v has shape (3,)so they broacasting to (2,3)
>>> print (x + v)
[[2 4 6]
 [5 7 9]]
>>> print ((x + v).shape)
(2, 3)
>>> print ((x + v).ndim)
2
>>> v.shape
(3,)
>>> x.shape
(2, 3)
>>> v.ndim
1
>>> x.ndim
2
```

> if we literally see what x + v means, that is as follows 

$$
x\ +\ v = \begin{bmatrix}
1 & 2 & 3 \cr
4 & 5 & 6 \cr
\end{bmatrix}\ +\ 
\begin{bmatrix}
1 & 2 & 3 \cr
\end{bmatrix}
$$


**However, according to the Broadcasting of Numpy. vector v become broadcasting.**

> let's see the broadcasting of x + v, which is how numpy calculate matrix element by element

The following is after application of broadcasting.

$$
x\ +\ v = \begin{bmatrix}
1 & 2 & 3 \cr
4 & 5 & 6 \cr
\end{bmatrix}\ +\ 
\begin{bmatrix}
1 & 2 & 3 \cr
1 & 2 & 3 \cr
\end{bmatrix}\ = \
\begin{bmatrix}
2(1+1) & 4(2+2) & 6(3+3) \cr
5(4+1) & 7(5+2) & 8(6+3) \cr
\end{bmatrix}
$$

As you can see, vector **v** stretched into the same shape of matrix **x**, and then vector **v** and matrix **x** were added. The result of the sum of them is 2 X 3 matrix.

i.e. that is how to add vector v to each row of a matrix x.

in here, something you need to recognize is stretching vector v is only conceptual !

Let's see another an example of broadcasting.

The following is adding a vector to each colum of a matrix. 

```python 
>>> import numpy as np
>>> x = np.array([[1,2,3],[4,5,6]])   ## x has shpae (2,3)
>>> w = np.array([4,5])               ## w has shape (2,)
>>> print ((x.T + w).T)          ## first, the transpose of matrix x, and then plus vector w, 
[[ 5  6  7]                      ## finally, you need to transpose of the transpos of matrix x plus vector w.
 [ 9 10 11]]                     ## So the last result is adding vector w to eaxh colum of matrix x. 
>>> print (((x.T + w).T).shape)  ## As you can see here, The transpose of matrix x has shape (3,2)
(2, 3)                           ## The transpose of matrix x plus vector w has (3,2). 
>>> print (((x.T + w).T).ndim)   ## (x.T + w).T make the final matrix as what I meant. 
2                                ## That is matrix with the vector w added to each column of matrix x
>>> print (x.T)
[[1 4]
 [2 5]
 [3 6]]
>>> print ((x.T).shape)
(3, 2)
>>> print ((x.T).ndim)
2
>>> print (x.T + w)
[[ 5  9]
 [ 6 10]
 [ 7 11]]
>>> print ((x.T + w).shape)
(3, 2)
>>> print ((x.T + w).ndim)
2
## But in adding a vector to each column of a matrix, another way exist. 
>>> print (x + np.reshape(w, (2,1)))         ## i.e. after vector w become row vector, and then plus matrix x. 
[[ 5  6  7]
 [ 9 10 11]]
>>> print ((x + np.reshape(w, (2,1))).ndim)
2
>>> print ((x + np.reshape(w, (2,1))).shape)
(2, 3)

```

> Let's see determinant about the above code

At First,  

$$
x.T\ +\ w = \begin{bmatrix}
1 & 4 \cr
2 & 5 \cr
3 & 6 \cr
\end{bmatrix}\ +\ 
\begin{bmatrix}
4 & 5  \cr
\end{bmatrix}\ 
$$

After the broadcasting in the above code. 

$$
x.T\ +\ w = \begin{bmatrix}
1 & 4 \cr
2 & 5 \cr
3 & 6 \cr
\end{bmatrix}\ +\ 
\begin{bmatrix}
4 & 5  \cr
4 & 5  \cr
4 & 5  \cr
\end{bmatrix}\ =\ 
\begin{bmatrix}
5(1+4) & 9(4+5) \cr
6(2+4) & 10(5+5) \cr
7(3+4) & 11(6+5) \cr
\end{bmatrix}
$$

> (x.T + w).T 

$$
(x.T\ +\ w).T =\begin{bmatrix}
5(1+4) & 6(2+4) & 7(3+4) \cr
9(4+5) & 10(5+5) & 11(6+5) \cr
\end{bmatrix}
$$

**keep in mind, the broadcasting of vector w is only conceptual, the actual way is using looping in C.**

Let's see the final example of broadcasting.

> multiplication between a matrix and a constant

```python 
>>> import numpy as np
>>> x = np.array([[1,2,3],[4,5,6]])    ## x has shape (2,3). Numpy treats scalars as array of shape();
>>> print (x*2)                        ## these can be broadcast together to shape (2,3)
[[ 2  4  6]
 [ 8 10 12]]
>>> print ((x*2).shape)
(2, 3)
>>> print ((x*2).ndim)
2
```

>  Let's see the broadcasting of constant 2.

The following is literally matrix x times 2. 

$$
x.T\ *\ 2 =\begin{bmatrix}
1 & 2 & 3 \cr
4 & 4 & 5 \cr
\end{bmatrix}*2
$$

in application of the broadcasting, the result is as follows.

$$
x.T\ *\ 2 = \begin{bmatrix}
1 & 2 & 3 \cr
4 & 4 & 5 \cr
\end{bmatrix}*\begin{bmatrix}
2 & 2 & 2 \cr
2 & 2 & 2 \cr
\end{bmatrix} = 
\begin{bmatrix}
2(1*2) & 4(2*2) & 6(3*2) \cr
8(4*2) & 10(5*2) & 12(6*2) \cr
\end{bmatrix}
$$

As you have seen for a while about broadcasting, Broadcasting typically makes your code more concise and faster, So You should strive to use it where it's possible.

## Numpy Documentation 

this brief overview has touched on many of the important things that you need to know about numpy, But now is far from understaning completely.

So If you want to know more details. check out [the numpy reference](https://docs.scipy.org/doc/numpy/reference/) to find out much more about numpy.

# Reference 

  - [Standford university's tutorial of python](http://cs231n.github.io/python-numpy-tutorial/) 
  
  - [github of CS288 python Tutorial of stanford](https://github.com/kuleshov/cs228-material/blob/master/tutorials/python/cs228-python-tutorial.ipynb)
  
  - [Numpy for Matlab Users](http://scipy.github.io/old-wiki/pages/NumPy_for_Matlab_Users)
  
  - [matplotlib for graph with python](https://matplotlib.org/index.html)
  
  if you continue to python more, I recommend you some library of python, numpy, scipy, matplolib
  
  For designs of this page 
  
  - [Stackedit](https://stackedit.io/editor)
  
  - [addition of MathJax](http://gastonsanchez.com/visually-enforced/opinion/2014/02/16/Mathjax-with-jekyll/)
  
  - [The basic Syntax of MathJax](http://www.onemathematicalcat.org/MathJaxDocumentation/MathJaxKorean/TeXSyntax_ko.html#matrix)
