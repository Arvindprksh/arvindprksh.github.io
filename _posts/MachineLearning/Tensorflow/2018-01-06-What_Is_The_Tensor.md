---
layout: post
title: What it the tensor in Tensorflow?
subtitle: Tutorial I wrote in my repository, 01.Tensor.
category: Tensorflow
tags: [tensorflow]
permalink: /2018/01/06/What_Is_The_Tensor/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

<!-- from https://github.com/hyunyoung2/hyunyoung2_Machine_Learning/blob/master/Tutorial/Tensorflow/01.BasicTensorflow/01.Tensor.ipynb-->

# What is the tensor?

When you do programming of tensorflow, _Tensor is everything_. I mean the programming of Tensorflow is building a graph that freely transport tensors. Tensor in Tensorflow is a **generalization of vectos and matrices**. it potentially contains higher dimensions. Internally, Tensorflow representas tensors as n-dimension arrays of base datatype(**string, int32, float32 and so on**). 

A **tf.Tensor** has two properties : 

   - a data type(float32, int32 or string and so on): each element in the Tensor has the same datatype. 
   
   - a shape: The number of dimension tensor has and the size of each dimension
       - shape can be partially or fully known.
       
There are some types of tensor :

   - tf.Variable,  tf.Constant, tf.Placeholder, tf.SparseTensor.
    
In the **key point**, with exceptoin of **tf.Variable**, **The value of a tensor is immutable**, which means that in the context of a single execution tensors only have a single value.

## Rank vs Shape 

   - rank: tensor object's number of dimensions.
   
```python
# Rank 0 (scalar)
animal = tf.Variable("Elephant", tf.string)
integer = tf.Variable(451, tf.int32)
# Rank 1 (1-dimension, vector)
floating_array  = tf.Variable([3.14159, 2.71828], tf.float32)
# Rank 2 (2-dimension, matrix)
# Normally, A rank 2 tensor object consists of as least one row and at least one column.
matrix = tf.Variable([[7],[11]], tf.int32)
# To check what version of rank each variables is?
rank0 = tf.rank(animal)
rank1 = tf.rank(floating_array)
rank2 = tf.rank(matrix)
```

   - shape: tensor object's the number of elements in each dimension. 

```python
# Every element in a tensor is one 
rank_three_tensor = tf.ones([3, 4, 5])
# To check the shape of a tensor
tf.shape(rank_three_tensor)
# To reshape of a tensor(rank 2)
matrix = tf.reshape(rank_three_tensor, [6, 10])
# To Check what kind of shape matrix has
tf.shape(matrix)
tf.shape(matrix)[0]
tf.shape(matrix)[1]
```

There are three notation used in Tensorflow:

   - rank, shape, dimencsion number

|  Rank  |      Shape      | dimension number |    Example    |
| :----: | :------------- | ---------------- | :------------- |
| 0 | [] | 0-D | A 0-D tensor, A scalar. |
| 1 | [D0] | 1-D | A 1-D tensor with shape[3]. |
| 2 | [D0, D1] | 2-D | A 2-D tensor with shape[3,2]|
| n | [D0, D0, ... , Dn-1] | n-D | A n-D tensor with shape[D0, D1,..., Dn-1] |

If you don't specify datatye of python object, when you create a **tf.tensor**, Tensorflow automatically choose datatype that can represent your data. 

   - Python's Integers --> tf.int32
   
   
   - Python's Floating point numbers ---> tf.float32
   

If you want to check an executed example code above, visit [01.tensor of hyunyoung2 git repository](https://github.com/hyunyoung2/hyunyoung2_Machine_Learning/blob/master/Tutorial/Tensorflow/01.BasicTensorflow/01.Tensor.ipynb)   
      
# Reference

   - [Guides r0.12](https://www.tensorflow.org/versions/r0.12/how_tos/variables/)
   
   - [Intialization function of tensorflow r0.12](https://www.tensorflow.org/versions/r0.12/api_docs/python/constant_op/)
      
   - [Tensors section of Programmer's guide of Tensorflow](https://www.tensorflow.org/programmers_guide/tensors)
   
   - [Variables section of Programmer's guide of Tensorflow](https://www.tensorflow.org/programmers_guide/variables)
   
   - [Tensor Ranks, Shapes, and Types](https://www.tensorflow.org/versions/r0.12/resources/dims_types)
