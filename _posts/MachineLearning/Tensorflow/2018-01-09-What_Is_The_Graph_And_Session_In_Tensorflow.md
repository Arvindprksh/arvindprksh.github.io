---
layout: post
title: What it the graph and session in Tensorflow?
subtitle: Tutorial I wrote in my repository, 04. Graph_and_Session.
category: Tensorflow
tags: [tensorflow]
permalink: /2018/01/09/What_Is_The_Graph_And_Session_In_Tensorflow/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

<!-- from https://github.com/hyunyoung2/hyunyoung2_Machine_Learning/blob/master/Tutorial/Tensorflow/01.BasicTensorflow/04.Graph_and_Session.ipynb -->

# What is the graph in Tensorflow?

Tensorflow is a graph of computation. it is comprised of **nodes(tf.Operation)** and **edge(tf.Tensor)** as a graph. When you call API of Tensorflow, each function of API is regarded as **a node(tf.operation)** in a graph. and each function return a tensor. i.e. tensor is the return value of each API. So each tensor move between **nodes(tf.Operation)**.

Tensorflow programs are usually structured into a construction phase that assembles a graph, and an execution phase that a session to execute ops in the graph. 

the two phase existing together look like:

<div align="center">
![](https://raw.githubusercontent.com/hyunyoung2/hyunyoung2_Machine_Learning/master/Tutorial/Tensorflow/01.BasicTensorflow/images/04.Graph_and_Session/tensors_flowing.gif)
</div>

on the above figure. each nodes represent **tf.Operation** and each edges represent **tf.Tensor**. Tensorflow API function construct new tf.Operation(node) and tf.Tensor(edge) objects and add them to a tf.Graph, such as a default graph. i.e. Tensorflow provides a default graph that is an implicit argument to all API functions in the same contexts. 

To sum up, 

  - programming is to draw a graph of computation calling API of Tensorflow. At this time. If you don't set another graph up, You basically draw computation into a default graph.
  
  - running Session is to put your graph of computation into physical devices such as CPU, GPU, and you can execute sub-graph or total-graph using method to execute them such as **session.run()** fucntion. 

# What is the Session in Tensorflow?

Session is responsible for matching physical device and provide methods to execute them. i.e. in a session. you will put a graph comprised of **nodes(ops) and tensor**, into device to execute by calling a certain method(**tf.Session().run()**). 

When you call **tf.Session().run(a list of fetch)**, it determines the return values, and may be a **tf.Operation**, a **tf.Tensor**, or a **tensor-like type** such as **tf.Variable**. These fetches determine what subgraph of the overall **tf.Graph** must be executed to produce the result: this is the subgraph that contains all operation named in the fetch list, plus all operations whose outputs are used to compute the value of the fetches. For example, the following code fragment shows how different arguments to **tf.Session().run()** cause different subgraphs to be executed.

```python
# Let's walk throug how to execute a graph to get value of ops.
x = tf.constant([[37.0, -23.0], [1.0, 4.0]])
w = tf.Variable(tf.random_uniform([2, 2]))
y = tf.matmul(x, w)
output = tf.nn.softmax(y)
global_init_op = w.initializer
print("=== checking Variables ===")
print("x:", x, "\nw:", w, "\ny:", y, "\n")

with tf.Session() as sess:
    
    # Run the initializer on `w`.
    sess.run(global_init_op)

    # Evaluate `output`. `sess.run(output)` will return a NumPy array containing
    # the result of the computation.
    print(sess.run(output))
    print("=== checking Variables ===")
    print("x:", x, "\nw:", w, "\ny:", y, "\n")
    
    # Evaluate `y` and `output`. Note that `y` will only be computed once, and its
    # result used both to return `y_val` and as an input to the `tf.nn.softmax()`
    # op. Both `y_val` and `output_val` will be NumPy arrays.
    y_val, output_val = sess.run([y, output])
    
    print("=== result of session run ===")
    print("y_val:\n", y_val)
    print("output_val:\n", output_val,"\n")
    
    for i in range(3):
        print("=== checking Variables:", i ,"===")
        print(i,"- x:", x, "\nw:", w, "\ny:", y, "\n")
```

As you check the code above, in particular, y is computated once for a session. So if y is used several times, just after a computation of y, when it is needed, the evaluated value is reused.

Sometimes, **tf.Session().run()** aslo optionally takes a dicationary of feeds, which is a mapping from **tf.Tensor** objects to values(typically Python scalars, lists or Numpy array) such as typically **tf.placeholder** tensors. the value will be substituted for those tensors in the execution like this:

```python
# Define a placeholder that expects a vector of three floating-point values,
# and a computation that depends on it.
x = tf.placeholder(tf.float32, shape=[3])
y = tf.square(x)

with tf.Session() as sess:
    # Feeding a value changes the result that is returned when you evaluate `y`.
    print(sess.run(y, feed_dict={x: [1.0, 2.0, 3.0]})  # => "[1.0, 4.0, 9.0]"
    print(sess.run(y, feed_dict={x: [0.0, 0.0, 5.0]})  # => "[0.0, 0.0, 25.0]"

    # Raises `tf.errors.InvalidArgumentError`, because you must feed a value for
    # a `tf.placeholder()` when evaluating a tensor that depends on it.
    #sess.run(y) # error will happen

    # Raises `ValueError`, because the shape of `37.0` does not match the shape
    # of placeholder `x`.
    #sess.run(y, {x: 37.0})  # error will happen```
```
## visualizing a graph of Tensorflow using tensorboard

If you want to debug with a graph comprised of node(ops) and tensor on tensorboard. 

call **tf.summary.FileWriter(path you want to store,  graph you want to print)**.

```python
# Define a placeholder that expects a vector of three floating-point values,
# and a computation that depends on it.
x = tf.placeholder(tf.float32, shape=[3])
y = tf.square(x)

with tf.Session() as sess:
    # `sess.graph` provides access to the graph used in a `tf.Session`.
    writer = tf.summary.FileWriter("./log/...", sess.graph)

    # Feeding a value changes the result that is returned when you evaluate `y`.
    print(sess.run(y, feed_dict={x: [1.0, 2.0, 3.0]})  # => "[1.0, 4.0, 9.0]"
    print(sess.run(y, feed_dict={x: [0.0, 0.0, 5.0]})  # => "[0.0, 0.0, 25.0]"

    # Raises `tf.errors.InvalidArgumentError`, because you must feed a value for
    # a `tf.placeholder()` when evaluating a tensor that depends on it.
    #sess.run(y) # error will happen

    # Raises `ValueError`, because the shape of `37.0` does not match the shape
    # of placeholder `x`.
    #sess.run(y, {x: 37.0})  # error will happen
```

And then, launch a directory path of **tf.summary.FileWriter** with tensorboard --logdir=**path of log directory**.

If you want to check an executed example code above, visit [04.Graph and Session](https://github.com/hyunyoung2/hyunyoung2_Machine_Learning/blob/master/Tutorial/Tensorflow/01.BasicTensorflow/04.Graph_and_Session.ipynb) of hyunyoung2 git repository

# Reference

  - [r1.4 graph and session section of programmer's guide of Tensorflow](https://www.tensorflow.org/programmers_guide/graphs)
  
  - [r0.12 Basic usage of Tensorflow](https://www.tensorflow.org/versions/r0.12/get_started/basic_usage)
