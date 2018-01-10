---
layout: post
title: Get Started of Tensorflow with basic way
subtitle: Tutorial I wrote in my repository, 05. Getting_Started.
category: Tensorflow
tags: [tensorflow]
permalink: /2018/01/10/Get_Started_Of_TensorFlow_With_TensorBoard/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

<!-- from https://github.com/hyunyoung2/hyunyoung2_Machine_Learning/blob/master/Tutorial/Tensorflow/01.BasicTensorflow/05.Getting_Strated.ipynb -->

# Get started with basic usage of Tensorflow

So far, I arranged all about tensor, variable, Graph and Session one by one. From now on, I will arrange what I explained together as one on this article.

When you do programming of Tensorflow, There are two phases, one is contruction of ops in a default graph. i.e. you have to represent computation of machine learning as a graph. and then the other is execution phase. i.e. if you want to compute whatever subgraph of the total graph, what you want to computes must be launched in a Session.

As you know, a Tensorflow graph is a description of computations. if you launch a session to get the result of whatever subgrap of a graph, the session places the subgraph ops onto Device such as GPU or CPU, and provides method to execute them. the method return tensors produced by ops as **numpy** ndarray objects in Python.

First, Build up Graph and then Launch it in a session!

Here I will construct a simple computationa to put those ops into a graph. I will show I will launch a session to get the return value. 

```python
# Let's walk through this code with Tensorboard. 
# To understand how to use tensorborad and for Tensorflow to work
# This is not to use variable to be assigned.  
import tensorflow as tf

# Create a Constant op that produces a 1x2 matrix.  The op is
# added as a node to the default graph.
#
# The value returned by the constructor represents the output
# of the Constant op.
matrix1 = tf.constant([[3., 3.]], name="matrix1")

# Create another Constant that produces a 2x1 matrix.
matrix2 = tf.constant([[2.],[2.]], name="matrix2")

# Create a Matmul op that takes 'matrix1' and 'matrix2' as inputs.
# The returned value, 'product', represents the result of the matrix
# multiplication.
product = tf.matmul(matrix1, matrix2, name="multiplication")

with tf.Session() as sess:
    # `sess.graph` provides access to the graph used in a `tf.Session`.
    writer = tf.summary.FileWriter("./log/05.Getting_Started/", sess.graph)
    sess.run(global_init_op)
    
    # test to how to use tensorboard at runtime of this model.
    for i in range (2):
        print(sess.run([matrix1, matrix2, product]))    
        
    writer.close()
```

The Default graph now has three nodes: two **tf.constant()** ops and one **tf.matmul()** op. To actually multiply the matrices, and ge the result of the multiplication, launch a graph in a session. without arguments the session constructor launches the default graph.

The Tensorflow implementation translates the graph definition inot executable operatioins distributed across available computing resource, such as the CPU or one of your computer's GPU cards. In general, you do not have to specify CPUs or GPUs explicitly. Tensorflow uses your first GPU, if you have one, for as many operations as possible.

## Interactive Usage

For ease of use in interacitve environments such as IPython, you can instead use the **InteractiveSession** class, ant the **Tensor.eval()** and **Operation.run()** method in the **InteractiveSession**.

```python
# Enter an interactive TensorFlow Session.
import tensorflow as tf
sess = tf.InteractiveSession()

x = tf.Variable([1.0, 2.0])
a = tf.constant([3.0, 3.0])

# Initialize 'x' using the run() method of its initializer op.
x.initializer.run()

# Add an op to subtract 'a' from 'x'.  Run it and print the result
sub = tf.subtract(x, a)
print(sub.eval())
# ==> [-2. -1.]

# Close the Session when we're done.
sess.close()
```

If you want to check an executed example code above, visit [05.Getting_Started](https://github.com/hyunyoung2/hyunyoung2_Machine_Learning/tree/master/Tutorial/Tensorflow/01.BasicTensorflow) of hyunyoung2 git repository

# Summary 

running a session is two ways, one is Interactive Session, the other one is not Interactive Session. i.e. after drawing a graph of computation. it is runing a session with a graph you want to execute. When you make a model with tensorflow, I strongly recommend you to use the latter one.

Finally, I add an example about using gradient descent algorithm. 

```python
# with Tensorboard
# Final example to understad a process of machine learning.
import tensorflow as tf

# Model parameters
W = tf.Variable([.3], dtype=tf.float32)
b = tf.Variable([-.3], dtype=tf.float32)
# Model input and output
x = tf.placeholder(tf.float32)
linear_model = W*x + b
y = tf.placeholder(tf.float32)

# loss
loss = tf.reduce_sum(tf.square(linear_model - y)) # sum of the squares
# optimizer
optimizer = tf.train.GradientDescentOptimizer(0.01)
train = optimizer.minimize(loss)

# training data
x_train = [1, 2, 3, 4]
y_train = [0, -1, -2, -3]

global_init_op = tf.global_variables_initializer()
with tf.Session() as sess:
    # `sess.graph` provides access to the graph used in a `tf.Session`.
    writer = tf.summary.FileWriter("./log/05.Getting_Started/", sess.graph)
    sess.run(global_init_op)
    # training op
    for i in range(1000):
        _, W_, b_ = sess.run([train,W,b], {x: x_train, y: y_train})
        if i % 10 == 0:
            print("=== checking variable ===")
            print("W:", W, "-", W_, "\nb:", b, "-", b_)

    # evaluate training accuracy
    curr_W, curr_b, curr_loss = sess.run([W, b, loss], {x: x_train, y: y_train})
    print("W: %s b: %s loss: %s"%(curr_W, curr_b, curr_loss))
    
    writer.close()
```

# Reference 

  - [Basic usage of Tensorflow r0.12](https://www.tensorflow.org/versions/r0.12/get_started/basic_usage)
  
  - [r1.4 getting started of Tensorflow](https://www.tensorflow.org/get_started/get_started)
