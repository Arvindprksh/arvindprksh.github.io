---
layout: post
title: How to get and use MNIST data in Tensorflow
subtitle: Tutorial I wrote in my repository, Datasetting - MINST.
category: Tensorflow
tags: [tensorflow, tutorial]
permalink: /2018/01/18/How_To_Get_And_Use_MNIST_In_Tensorflow/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

<!-- from https://github.com/hyunyoung2/hyunyoung2_Machine_Learning/blob/master/Tutorial/Tensorflow/02.DataSetting/MNIST/MNIST_Dataset.ipynb -->

# What is the MNIST ?

MNIST is digit images as a simple computer vision dataset. the images of this dataset consist of handwirtten digits like these :

![](https://raw.githubusercontent.com/hyunyoung2/hyunyoung2_Machine_Learning/master/Tutorial/Tensorflow/02.DataSetting/images/MNIST/MNIST.png)

It also includes labels for each image, letting us know which digit it is. For example, the labels for the above images ar 5, 0, 4, and 1. Basically, this dataset is comprised of digit  and the correponding label.

### The MNIST Data

This MNIST data is hosted on [Yann LeCun's websit](http://yann.lecun.com/exdb/mnist). If you want to download and read MNIST data, these two lines is enough in Tensorflow. 
    
```python
from tensorflow.examples.tutorials.mnist import input_data
mnist = input_data.read_data_sets("MNIST_data/", one_hot=True)
# one_hot means MNIST's label is the representaion of one-hot vector. (if one_hot is true)
# if ont_hot is false, MNIST' label is just digit between 0 and 9 like these :
# if MNIST's label is 3, [0, 0, 0, 1, 0, 0, 0, 0, 0, 0]
```
As I mentioned above, MNIST have two part, images and their correspoding labels. for example, **mnist.train.images** for traing images, and **mnist.train.labels** for their correspoding labels. 

The pairs of images and labels split into something like the following.

The MNIST data is split into three parts:

- 55,000 data points of training data(minst.train)  
- 10,000 points of test data(mnist.test)
- 5000 points of validation data(mnist.validation)

The above thing is basic composition set up of dataset for machine learning. i.e. The Dataset for Machine Learning is comprised of three parts like **train set, test set, validation set**.

- train set : to train machine learning algorithms. 
- test set : to verify your machine learning algorithm what if it works in real world
- validation : to adjust hyper parameter in your machine learning algorithm.

Each of images of MNIST is 28\*28 pixels. If we interpret the each of images as a array, the size of a array is 28\*28=784. it looks as follows. 
  
![](https://raw.githubusercontent.com/hyunyoung2/hyunyoung2_Machine_Learning/master/Tutorial/Tensorflow/02.DataSetting/images/MNIST/MNIST-Matrix.png)

After making 28\*28 pixels into a array(784), we just interpert each of image as a vector in vector space. i.e The MNIST images are just a bunch of points in a 784-dimensional vector space. 
  
The below is how to download MNIST Dataset, When you want to implement tensorflow with MNIST. 

If you want to check an executed example code above, visit [Datasetting-MNIST](https://github.com/hyunyoung2/hyunyoung2_Machine_Learning/blob/master/Tutorial/Tensorflow/02.DataSetting/MNIST/MNIST_Dataset.ipynb) of hyunyoung2 git rep

# Reference 

   - [MNIST's official site](http://yann.lecun.com/exdb/mnist/)  
   
   - [MNIST of tensorflow](https://www.tensorflow.org/get_started/mnist/beginners)  
   
   - [Github of tensorflow](https://github.com/tensorflow)  
