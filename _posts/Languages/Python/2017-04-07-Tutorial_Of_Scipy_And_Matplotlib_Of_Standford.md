---
layout: post
title: Tutorial of Scipy and Matplotlib with Stanford python tutorial
subtitle: I will let you know the basics of Scipy and MatplotLib
category: Python
tags: [language, python]
permalink: /2017/04/07/Tutorial_Of_Scipy_And_Matplotlib_Of_Standford/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
---
{% include MathJax.html %}

the table of contens in this article. 

- Scipy
  - Image operations
  - MATLAB files
  - Distance between points
  
- Matplotlib
  - Plotting
  - SubPlots
  - Images
  
Let's explore more in detail.

## Scipy

Numpy provides a high-performance mulitidimensional array and basic tools to compute with and manipulate these arrrays. [Scipy](https://docs.scipy.org/doc/scipy/reference/) builds on this, and provides a large number of functions that operate on numpy arrays and are useful for different types of scientific and engineering applications.

The best way to get familiar with Scipy is to [browse the documentation](https://docs.scipy.org/doc/scipy/reference/index.html). We will highlight some parts of Scipy that you might find useful for this class.

### Image operations

Scipy provides some basix functions to work with images. For example, it has functions to read images from disk into numpy arrays, to write numpy arrays to disk as images, and to resize images. Here is a simple example that showcases these functions :

```ptyhon
>>> import numpy as np
## call of scipy module 
>>> from scipy.misc import imread, imsave, imresize
## Read an JPEG image into a numpy array
>>> img = imread('your path of image\cat.jpg')
## img is numpy array, you can verify dtype, ndim, rank, shape and so on
>>> print (type(img))
<class 'numpy.ndarray'>
>>> print (img.dtype, img.shape)
uint8 (400, 248, 3)
>>> img
array([[[132, 128, 117],
        [155, 151, 139],
        [181, 175, 161],
        ...,
        [ 78,  68,  43],
        [ 76,  65,  43],
        [ 64,  53,  31]],

       [[134, 130, 118],
        [152, 148, 136],
        [177, 171, 157],
        ...,
        [ 75,  65,  40],
        [ 72,  61,  39],
        [ 62,  51,  29]],

       [[138, 134, 122],
        [151, 145, 131],
        [174, 168, 152],
        ...,
        [ 71,  61,  36],
        [ 68,  58,  33],
        [ 59,  51,  28]],

       ...,
       [[115, 145,  75],
        [107, 137,  67],
        [106, 135,  69],
        ...,
        [113, 101,  79],
        [106,  94,  72],
        [103,  91,  67]],

       [[107, 134,  65],
        [112, 139,  72],
        [109, 138,  72],
        ...,
        [112,  97,  78],
        [109,  94,  73],
        [101,  89,  67]],

       [[124, 151,  84],
        [116, 143,  76],
        [111, 140,  74],
        ...,
        [ 91,  76,  57],
        [ 89,  74,  55],
        [ 86,  71,  50]]], dtype=uint8)
>>>
### 
>>> img_tinted = img * [1, 0.95, 0.9]
>>> imsave('your path to store image\cat_tinted.jpg', img_tinted)
>>> img_tinted = imresize(img_tinted, (300,300))
>>> imsave('your path to store image\cat_tinted_resized.jpg', img_tinted)
```

> img = imread('your path of image\cat.jpg')
> print (img.dtype, img.shape)

Like the above code, the image read.

![](/img/Image/Languages/Python/2017-04-07-Tutorial_Of_Scipy_And_Matplotlib_Of_Standford/cat.jpg)

> img_tinted = img * [1, 0.95, 0.9]

this change RGB of Image.

![](/img/Image/Languages/Python/2017-04-07-Tutorial_Of_Scipy_And_Matplotlib_Of_Standford/cat_tinted.jpg)

> img_tinted = imresize(img_tinted, (300,300))

this resize the size of image, in my case, 300 X 300.

![](/img/Image/Languages/Python/2017-04-07-Tutorial_Of_Scipy_And_Matplotlib_Of_Standford/cat_tinted_resized.jpg)

If I compare the original image with this resized.

---

![](/img/Image/Languages/Python/2017-04-07-Tutorial_Of_Scipy_And_Matplotlib_Of_Standford/cat.jpg) [](/img/Image/Languages/Python/2017-04-07-Tutorial_Of_Scipy_And_Matplotlib_Of_Standford/cat_tinted_resized.jpg)

Left: The original Image. Right: The tinted and resized Image.
--

### MATLAB files

The function **scipy.io.ioloadmat** and **Scipy.io.savement** allow you to read and write MATLAB files. If you want to know more in detail.

you can read about the information in [the documentation.](https://docs.scipy.org/doc/scipy/reference/io.html)

### Distance between points

Scipy defines some useful functions for computing distances between sets of points.

The function **scipy.spatial.distance.pdit** computes the distance between all pairs of points in a given set :

> First of all, Create the following array where each row is a point in 2-dimension space :
> x = np.array([[0,1],[1,0],[2,0]])

$$
x = \begin{bmatrix}
0 & 1 \cr
1 & 0 \cr
2 & 0 \cr
\end{bmatrix}
$$ 

> To compute the Euclidean distance between all rows of x.
> d[i,j] is the Euclidean distance between x[i,:], and [j, :].
> d = squareform(pdist(x, 'euclidean'))

$$
In\ x = \begin{bmatrix}
0 & 1 \cr
1 & 0 \cr
2 & 0 \cr
\end{bmatrix},\ if\ \begin{bmatrix}
0 \cr 
1 \cr
\end{bmatrix} = \vec a,\ \begin{bmatrix}
1 \cr
0 \cr
\end{bmatrix} = \vec b,\ \begin{bmatrix}
2 \cr 
0 \cr
\end{bmatrix} = \vec c
$$

$$
\vec a,\ \vec b\ and\ \vec c\ are\ in\ Cartesian\ Coordinate\ of\ \\rm I\! R^2
$$

you can get each distance of them with **pdist** function.

> dis = pdist(x, 'euclidean')
> dis
> array([ 1.41421356,  2.23606798,  1.        ])

$$
pdist(x, 'euclidean') = \begin{bmatrix}
1.41421356 & 2.23606798 & 1.  \cr
\end{bmatrix}
$$

In the above case, you cannot get accurate distance, I mean you don't know what pair of points it is in **x** array.

> So, you need to use a function, squareform(pdist(x, 'euclidean'))

**Squareform** function make matrix square.

$$
squareform(pdist(x, 'euclidean')) = \begin{bmatrix}
0. & 1.41421356 & 2.23606798 \cr
1.41421356 & 0. & 1. \cr
2.23606798 & 1. & 0. \cr
\end{bmatrix}
$$

In the above matrix, each terms indicate distance between two points, you can know the location of two points.

the location of two points is the index of the above matrix term.

> if d = squareform(pdist(x, 'euclidean'))
> d[i, j] is the the Euclidean distance between x[i, :] and x[j, :]
> d[0, 0] is distance between x[0, :] and x[0, :]
> d[0, 1] is distance between x[0, :] and x[1, :]
> d[0, 2] is distance between x[0, :] and x[2, :]
> ...
> d[2, 1] is distance between x[2, :] and x[2, :]
> d[2, 2] is distance between x[2, :] and x[2, :]

> the location of Each point(thought of as a row of matrix x ) 

$$
In\ x = \begin{bmatrix}
0 & 1 \cr
1 & 0 \cr
2 & 0 \cr
\end{bmatrix},\ if\ \begin{bmatrix}
0 \cr 
1 \cr
\end{bmatrix} = \vec a,\ \begin{bmatrix}
1 \cr
0 \cr
\end{bmatrix} = \vec b,\ \begin{bmatrix}
2 \cr 
0 \cr
\end{bmatrix} = \vec c
$$

> d = squareform(pdist(x, 'euclidean'))

$$
d = squareform(pdist(x, 'euclidean')) = \begin{bmatrix}
0. & 1.41421356 & 2.23606798 \cr
1.41421356 & 0. & 1. \cr
2.23606798 & 1. & 0. \cr
\end{bmatrix}\  means\ 
$$

> d[i, j] is the the Euclidean distance between x[i, :] and x[j, :]

$$
0.(d[0, 0])\ is\ distance\ between\ \vec a = \begin{bmatrix}
0 \cr 
1 \cr
\end{bmatrix}\ and\ \vec a = \begin{bmatrix}
0 \cr 
1 \cr
\end{bmatrix}
$$


$$
1.41421356(d[1, 0])\ is\ distance\ between\ \vec b = \begin{bmatrix}
1 \cr
0 \cr
\end{bmatrix}\ and\ \vec a = \begin{bmatrix}
0 \cr 
1 \cr
\end{bmatrix}
$$


$$
2.23606798(d[2, 0])\ is\ distance\ between\ \vec c = \begin{bmatrix}
2 \cr 
0 \cr
\end{bmatrix}\ and\ \vec a = \begin{bmatrix}
0 \cr 
1 \cr
\end{bmatrix}
$$

> Finally, compare pdis(pdist(x, 'euclidean')) with squareform(pdist(x, 'euclidean'))

$$
pdist(x, 'euclidean') = \begin{bmatrix}
1.41421356 & 2.23606798 & 1.  \cr
\end{bmatrix}\  and
squareform(pdist(x, 'euclidean')) = \begin{bmatrix}
0. & 1.41421356 & 2.23606798 \cr
1.41421356 & 0. & 1. \cr
2.23606798 & 1. & 0. \cr
\end{bmatrix}
$$


If you compare both of them, 

squareform function makes the result the shape of square, and this matrix will show you distance of self-point,

if you have opints, a, b and c. in here, suquareform also calculate distance between a and a.

but only if you use pdist function. that indicate distance in order. 

For example, what I meant is as follows :

$$
pdist(x, 'euclidean') = \begin{bmatrix}
1.41421356 & 2.23606798 & 1.  \cr
\end{bmatrix}\ means,\ 
1.41421356 = dist(x[0],\ x[1]),\ 2.23606798 = dist(x[0], x[2]),\ 1. = dist(x[1], x[2])
$$

Or You can view it as the elements in the upper triangular portion of the square distance matrix.

Let's think of what I mean :

$$
pdist(x, 'euclidean') = \begin{bmatrix}
1.41421356 & 2.23606798 & 1.  \cr
\end{bmatrix}\  and
squareform(pdist(x, 'euclidean')) = \begin{bmatrix}
0. & 1.41421356 & 2.23606798 \cr
1.41421356 & 0. & 1. \cr
2.23606798 & 1. & 0. \cr
\end{bmatrix}
$$

also you can view what I mean with code :

```python 
>>> dis = pdist(x, 'euclidean')
>>> dis
array([ 1.41421356,  2.23606798,  1.        ])
>>> d = squareform(pdist(x, 'euclidean'))
>>> d
array([[ 0.        ,  1.41421356,  2.23606798],
       [ 1.41421356,  0.        ,  1.        ],
       [ 2.23606798,  1.        ,  0.        ]])
       
>>> y = np.array([[0,10],[10,10],[20,20],[10,0]])
>>> squareform(pdist(y))
array([[  0.        ,  10.        ,  22.36067977,  14.14213562],
       [ 10.        ,   0.        ,  14.14213562,  10.        ],
       [ 22.36067977,  14.14213562,   0.        ,  22.36067977],
       [ 14.14213562,  10.        ,  22.36067977,   0.        ]])
>>> pdist(y)
array([ 10.        ,  22.36067977,  14.14213562,  14.14213562,
        10.        ,  22.36067977])
```

if you know more in detail, you can read [this Stackoverflow.](http://stackoverflow.com/questions/13079563/how-does-condensed-distance-matrix-work-pdist).

Let's calculate the distance between two points in python code.

```python 
>>> import numpy as np
>>> from scipy.spatial.distance import pdist, squareform
>>> x = np.array([[0,1],[1,0],[2,0]])
>>> x
array([[0, 1],
       [1, 0],
       [2, 0]])
>>> print (x)
[[0 1]
 [1 0]
 [2 0]]
>>> d = squareform(pdist(x, 'euclidean'))
>>> d
array([[ 0.        ,  1.41421356,  2.23606798],
       [ 1.41421356,  0.        ,  1.        ],
       [ 2.23606798,  1.        ,  0.        ]])
>>> print (d)
[[ 0.          1.41421356  2.23606798]
 [ 1.41421356  0.          1.        ]
 [ 2.23606798  1.          0.        ]]
>>> d.shape
(3, 3)
>>> d.ndim
2

>>> dis = pdist(x, 'euclidean')
>>> dis
array([ 1.41421356,  2.23606798,  1.        ])
>>> print (dis)
[ 1.41421356  2.23606798  1.        ]
>>> dis.shape
(3,)
>>> dis.ndim
1
```

You can read all the detais about this function in [the documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.pdist.html)

A similar function (**scipy.spatial.distance.cdist**) computes the distance between all paris across sets of points; you can read about it in [the documentation](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.cdist.html)

## Matplotlib

Matplotlib is a plotting library. In this section, I will give you a brief introduction to **the matplotlib.pyplot** module, whiich provides a plotting system similar to that of MATLAB.

### Plotting

The most important function in matplotlib is **plot**, which allows you to plot 2D data. Here is a simple example :

```python
>>> import numpy as np
>>> import matplotlib.pyplot as plt
>>> x = np.arange(0, 3 * np.pi, 0.1)
>>> x
array([ 0. ,  0.1,  0.2,  0.3,  0.4,  0.5,  0.6,  0.7,  0.8,  0.9,  1. ,
        1.1,  1.2,  1.3,  1.4,  1.5,  1.6,  1.7,  1.8,  1.9,  2. ,  2.1,
        2.2,  2.3,  2.4,  2.5,  2.6,  2.7,  2.8,  2.9,  3. ,  3.1,  3.2,
        3.3,  3.4,  3.5,  3.6,  3.7,  3.8,  3.9,  4. ,  4.1,  4.2,  4.3,
        4.4,  4.5,  4.6,  4.7,  4.8,  4.9,  5. ,  5.1,  5.2,  5.3,  5.4,
        5.5,  5.6,  5.7,  5.8,  5.9,  6. ,  6.1,  6.2,  6.3,  6.4,  6.5,
        6.6,  6.7,  6.8,  6.9,  7. ,  7.1,  7.2,  7.3,  7.4,  7.5,  7.6,
        7.7,  7.8,  7.9,  8. ,  8.1,  8.2,  8.3,  8.4,  8.5,  8.6,  8.7,
        8.8,  8.9,  9. ,  9.1,  9.2,  9.3,  9.4])
>>> x.shape
(95,)
>>> x.ndim
1
>>> y = np.sin(x)
>>> y
array([ 0.        ,  0.09983342,  0.19866933,  0.29552021,  0.38941834,
        0.47942554,  0.56464247,  0.64421769,  0.71735609,  0.78332691,
        0.84147098,  0.89120736,  0.93203909,  0.96355819,  0.98544973,
        0.99749499,  0.9995736 ,  0.99166481,  0.97384763,  0.94630009,
        0.90929743,  0.86320937,  0.8084964 ,  0.74570521,  0.67546318,
        0.59847214,  0.51550137,  0.42737988,  0.33498815,  0.23924933,
        0.14112001,  0.04158066, -0.05837414, -0.15774569, -0.2555411 ,
       -0.35078323, -0.44252044, -0.52983614, -0.61185789, -0.68776616,
       -0.7568025 , -0.81827711, -0.87157577, -0.91616594, -0.95160207,
       -0.97753012, -0.993691  , -0.99992326, -0.99616461, -0.98245261,
       -0.95892427, -0.92581468, -0.88345466, -0.83226744, -0.77276449,
       -0.70554033, -0.63126664, -0.55068554, -0.46460218, -0.37387666,
       -0.2794155 , -0.1821625 , -0.0830894 ,  0.0168139 ,  0.1165492 ,
        0.21511999,  0.31154136,  0.40484992,  0.49411335,  0.57843976,
        0.6569866 ,  0.72896904,  0.79366786,  0.85043662,  0.8987081 ,
        0.93799998,  0.96791967,  0.98816823,  0.99854335,  0.99894134,
        0.98935825,  0.96988981,  0.94073056,  0.90217183,  0.85459891,
        0.79848711,  0.7343971 ,  0.66296923,  0.58491719,  0.50102086,
        0.41211849,  0.31909836,  0.22288991,  0.12445442,  0.02477543])
>>> y.shape
(95,)
>>> y.ndim
1
>>> plt.plot(x, y)
[<matplotlib.lines.Line2D object at 0x0523A0D0>]
>>> plt.show()
```

After Running this code, the following plot is produced :

---

![](/img/Image/Languages/Python/2017-04-07-Tutorial_Of_Scipy_And_Matplotlib_Of_Standford/sin(x).png)

the graph of y = sin(x)

---

With just a little of extra work, we can easily plot multiple lines at once, and add a title, legend, and axis labels :

```python 
>>> import numpy as np
>>> import matplotlib.pyplot as plt
>>>
>>> x = np.arange(0, 3 * np.pi, 0.1)
>>> x
array([ 0. ,  0.1,  0.2,  0.3,  0.4,  0.5,  0.6,  0.7,  0.8,  0.9,  1. ,
        1.1,  1.2,  1.3,  1.4,  1.5,  1.6,  1.7,  1.8,  1.9,  2. ,  2.1,
        2.2,  2.3,  2.4,  2.5,  2.6,  2.7,  2.8,  2.9,  3. ,  3.1,  3.2,
        3.3,  3.4,  3.5,  3.6,  3.7,  3.8,  3.9,  4. ,  4.1,  4.2,  4.3,
        4.4,  4.5,  4.6,  4.7,  4.8,  4.9,  5. ,  5.1,  5.2,  5.3,  5.4,
        5.5,  5.6,  5.7,  5.8,  5.9,  6. ,  6.1,  6.2,  6.3,  6.4,  6.5,
        6.6,  6.7,  6.8,  6.9,  7. ,  7.1,  7.2,  7.3,  7.4,  7.5,  7.6,
        7.7,  7.8,  7.9,  8. ,  8.1,  8.2,  8.3,  8.4,  8.5,  8.6,  8.7,
        8.8,  8.9,  9. ,  9.1,  9.2,  9.3,  9.4])
>>> x.shape
(95,)
>>> x.ndim
1
>>> y_sin = np.sin(y)
>>> y_cos = np.sin(x)
>>> y_sin = np.sin(x)
>>> y_sin
array([ 0.        ,  0.09983342,  0.19866933,  0.29552021,  0.38941834,
        0.47942554,  0.56464247,  0.64421769,  0.71735609,  0.78332691,
        0.84147098,  0.89120736,  0.93203909,  0.96355819,  0.98544973,
        0.99749499,  0.9995736 ,  0.99166481,  0.97384763,  0.94630009,
        0.90929743,  0.86320937,  0.8084964 ,  0.74570521,  0.67546318,
        0.59847214,  0.51550137,  0.42737988,  0.33498815,  0.23924933,
        0.14112001,  0.04158066, -0.05837414, -0.15774569, -0.2555411 ,
       -0.35078323, -0.44252044, -0.52983614, -0.61185789, -0.68776616,
       -0.7568025 , -0.81827711, -0.87157577, -0.91616594, -0.95160207,
       -0.97753012, -0.993691  , -0.99992326, -0.99616461, -0.98245261,
       -0.95892427, -0.92581468, -0.88345466, -0.83226744, -0.77276449,
       -0.70554033, -0.63126664, -0.55068554, -0.46460218, -0.37387666,
       -0.2794155 , -0.1821625 , -0.0830894 ,  0.0168139 ,  0.1165492 ,
        0.21511999,  0.31154136,  0.40484992,  0.49411335,  0.57843976,
        0.6569866 ,  0.72896904,  0.79366786,  0.85043662,  0.8987081 ,
        0.93799998,  0.96791967,  0.98816823,  0.99854335,  0.99894134,
        0.98935825,  0.96988981,  0.94073056,  0.90217183,  0.85459891,
        0.79848711,  0.7343971 ,  0.66296923,  0.58491719,  0.50102086,
        0.41211849,  0.31909836,  0.22288991,  0.12445442,  0.02477543])
>>> y_sin.shape
(95,)
>>> y_sin.ndim
1
>>> y_cos = np.cos(x)
>>> y_cos.ndim
1
>>>
>>>
>>> plt.plot(x, y_sin)
[<matplotlib.lines.Line2D object at 0x0538F070>]
>>> plt.plot(x, y_cos)
[<matplotlib.lines.Line2D object at 0x0538F150>]
>>> plt.xlabel('x axis label')
<matplotlib.text.Text object at 0x07001990>
>>> plt.ylabel('y axis label')
<matplotlib.text.Text object at 0x06CB17D0>
>>> plt.title('Sine and Cosine')
<matplotlib.text.Text object at 0x0536CC30>
>>> plt.legend(['Sine', 'Cosine'])
<matplotlib.legend.Legend object at 0x0538FD10>
>>> plt.show()
```

let's see the result of plt.show() :

---

![](/img/Image/Languages/Python/2017-04-07-Tutorial_Of_Scipy_And_Matplotlib_Of_Standford/Sine_and_Cosine.png)

the graph of y_sin and y_cos

---

you can read much more  about the plot function in [the documentation](http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.plot)


### subplot 

you can plot different things in the same figure using the subplot function, Here is an example :

```python 
>>> import numpy as np
>>> import matplotlib.pyplot as plt
>>>
>>>
>>> x = np.arange(0, 3 * np.pi, 0.1)
>>> y_sin = np.sin(x)
>>> y_cos = np.cos(x)
>>>
>>>
>>> plt.subplot(2, 1, 1)
<matplotlib.axes._subplots.AxesSubplot object at 0x0539F2F0>
>>> plt.plot(x, y_sin)
[<matplotlib.lines.Line2D object at 0x05006C30>]
>>> plt.title('Sine')
<matplotlib.text.Text object at 0x04FEA830>
>>>
>>>
>>> plt.subplot(2,1,2)
<matplotlib.axes._subplots.AxesSubplot object at 0x05006D30>
>>> plt.plot(x, y_cos)
[<matplotlib.lines.Line2D object at 0x0503E790>]
>>> plt.title('Cosine')
<matplotlib.text.Text object at 0x05036790>
>>> plt.xlabel('x')
<matplotlib.text.Text object at 0x05016030>
>>> plt.ylabel('y')
<matplotlib.text.Text object at 0x0501CA30>
>>> plt.legend(['Cosine'])
<matplotlib.legend.Legend object at 0x0503E890>
>>> plt.show()
>>>
```

As you can read the above code, after making subplot, each of area is divided. 

---

![](/img/Image/Languages/Python/2017-04-07-Tutorial_Of_Scipy_And_Matplotlib_Of_Standford/subplot.png)

the above is subplot(2,1,1) and the below is subplot(2,1,2)

---

You can read much mor about the **subplot** function in [the documentation](http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.subplot)


### Images 

You can use the imshow function to show image here is an example :

```python 
>>> import numpy as np
>>> from scipy.misc import imread, imresize
>>> import matplotlib.pyplot as plt
>>> img = imread('your path including image\cat.jpg')
>>> img_tinted = img * [1, 0.95, 0.9]
>>> plt.subplot(1,2,1)
<matplotlib.axes._subplots.AxesSubplot object at 0x071A5310>
>>> plt.imshow(img)
<matplotlib.image.AxesImage object at 0x071F1050>
>>> plt.subplot(1,2,2)
<matplotlib.axes._subplots.AxesSubplot object at 0x071E9FD0>
>>> plt.imshow(np.uint8(img_tinted))                  ## plt.imshow(img_tinted)
<matplotlib.image.AxesImage object at 0x05031770>
>>> plt.show()
```

---

![](/img/Image/Languages/Python/2017-04-07-Tutorial_Of_Scipy_And_Matplotlib_Of_Standford/imshow_strange.png)

The only case where you use plt.imshow(img_tinted) instead of plt.imshow(np.uint8(img.tinted)

![](/img/Image/Languages/Python/2017-04-07-Tutorial_Of_Scipy_And_Matplotlib_Of_Standford/imshow.png)

The case where you use correctly plt.imshow(np.unint8(img_tinted)

---

For a while, you have learned about matplotlib and scipy. But this is so easy. 

If you want to know more detail, you need to read [reference of scipy](https://docs.scipy.org/doc/scipy/reference) or [matplotlib api](http://matplotlib.org/api) 

## Reference

 - [Stanford tutorial of python](http://cs231n.github.io/python-numpy-tutorial/#scipy)
 
 - [the official Scipy.org](https://docs.scipy.org/doc/scipy/reference/)
 
  For designs of this page 
  
  - [Stackedit](https://stackedit.io/editor)
  
  - [addition of MathJax](http://gastonsanchez.com/visually-enforced/opinion/2014/02/16/Mathjax-with-jekyll/)
  
  - [The basic Syntax of MathJax](http://www.onemathematicalcat.org/MathJaxDocumentation/MathJaxKorean/TeXSyntax_ko.html#matrix)
  
  If you want to know more in detail. 
  
   - [Higher-dimensional arrays](http://hplgit.github.io/primer.html/doc/pub/plot/._plot-readable007.html)
