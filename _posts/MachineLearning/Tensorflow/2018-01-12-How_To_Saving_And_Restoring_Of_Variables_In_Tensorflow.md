---
layout: post
title: What is the word embedding in Tensorflow with Tensorboard's Embedding projector
subtitle: Tutorial I wrote in my repository, 01. Word_Embedding.
category: Tensorflow
tags: [tensorflow]
permalink: /2018/01/12/How_To_Saving_And_Restoring_Of_Variables_In_Tensorflow/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

<!-- from https://github.com/hyunyoung2/hyunyoung2_Machine_Learning/blob/master/Tutorial/Tensorflow/01.BasicTensorflow/06.Saving_and_Restoring_of_Variables.ipynb -->

# How to save and restor Tensorflow's Variable

In here, all information of your model in Tensorflow is kept track of on Variable of Tensor. i.e. A Tensorflow variable provides the best way to represent shared, Persistent state manipulated by your program.

with this variable, If you want to save and restore all the variable in Tensorflow, use the **tf.train.Saver** class provides methods for saving and restoring models. 

The **tf.train.Saver** constructor adds **save** and **restore** ops to the graph for all, or a specificed list, of the variables in the graph.

Tensorflow saves variables in binary checkpoint files, that roughly speaking, maps variable names to tensor values. 

## Saving Variables

Create a **Saver** with tf.train.Saver() to manage all variables in the model. For example, the following snippet demonstrates how to call the **tf.train.Saver.save** method to save variables to a checkpoint file:

```python
import os
import tensorflow as tf
# To save checkpoint file
LOG_DIR = os.path.join(os.getcwd(),"log/")

if not os.path.exists(LOG_DIR):
    os.makedirs(LOG_DIR)
    print(LOG_DIR+" is created!\n")
else:
    print("you have already"+LOG_DIR+" !\n")

print("the current working directory:", LOG_DIR, "\n")

# Create some variables. 
v1 = tf.get_variable("v1", shape=[3], initializer = tf.zeros_initializer)
v2 = tf.get_variable("v2", shape=[5], initializer = tf.zeros_initializer)

inc_v1 = v1.assign(v1+1)
dec_v2 = v2.assign(v2-1)

# Add an op to initialize the variables.
global_init_op = tf.global_variables_initializer()

# Add ops to save and restore all the variable.

saver = tf.train.Saver()

# Later, launch the model, initialize the variables, do some work, and save the variables to disk.
with tf.Session() as sess:
    # To draw  a graph of this session on Tensorboard
    writer = tf.summary.FileWriter(LOG_DIR, sess.graph)
    
    sess.run(global_init_op)
    # Do some work with the model
    print("=== Before assigne each variables ===")
    v1_, v2_ = sess.run([v1, v2])
    print("v1:", v1_)
    print("v2:", v2_)
    
    inc_v1.op.run()
    dec_v2.op.run()
    
    print("=== after assigne each variables with inc_v1, dec_v2 ===")
    v1_, v2_ = sess.run([v1, v2])
    print("v1:", v1_)
    print("v2:", v2_)
    
    # Save the variable to disk
    save_path = saver.save(sess, os.path.join(LOG_DIR, "model.ckpt"))
    # To check where I saved checkpoint file
    print("\nModel saved in file: %s" % save_path)
    
    writer.close()
```

## Restoring variables

The **tf.train.Saver** object not only saves variables to checkpoint files, it also restores variables. Note that when you restore variables from a file you do not have to intialize them beforehand. For example, the following snippet demonstrates how to call the **tf.train.Saver.restore** method to restore variables from a checkpoint file. 

```python
import os
import tensorflow as tf
# To save checkpoint file
LOG_DIR = os.path.join(os.getcwd(),"log/")

if not os.path.exists(LOG_DIR):
    os.makedirs(LOG_DIR)
    print(LOG_DIR+" is created!\n")
else:
    print("you have already"+LOG_DIR+" !\n")

print("the current working directory:", LOG_DIR, "\n")

tf.reset_default_graph()

# Create some variables. 
v1 = tf.get_variable("v1", shape=[3])
v2 = tf.get_variable("v2", shape=[5])

# Add ops to save and restore all the variables.
saver = tf.train.Saver()


# Later, launch the model, use the saver to restore variables from disk, and 
# do some work with the model
with tf.Session() as sess:
    # To draw  a graph of this session on Tensorboard
    writer = tf.summary.FileWriter(LOG_DIR)
    writer.add_graph(sess.graph)
    # Do some work with the model
    # Restore variables from disk. 
    # you have to get the same name of each variable in here from model.ckpt
    saver.restore(sess, os.path.join(LOG_DIR, "model.ckpt"))
    print("Model restored.")
    
    # Check the values of the variables.
    print("=== check the value of each variables restored ===")
    print("v1 : %s" % v1.eval())
    print("v2 : %s" % v2.eval())
    writer.close()
```

When you restore variable from the previously saved your model, you can choose a variable you want and vice versa.

Let's see how to choose which variables to save and store.

## Choosing which variables to save and restore

If you do not pass any arguments to **tf.save.Saver()**, the saver deals with all variables in the graph. Each variables is saved under the name created when the variable was created. 

Let's go through two situations you specify the name to restore to **tf.save.Saver**. 

First, the name is not the same between one other, i.e. When you save a variable as the name of "weight", but when you restore it, the name of a variable is "params". 

Second, It is the situation where you want to restore a subset of all the variables you saved in the previous model. i.e. your previous model had five layers of feed-forward neural network, But in new feed-forward neural newtwork, you have six layers but you want to restore five layers from the previous model.

For two case above, it is useful to explicitly specify name of the variables to be restored in your new model.

You can easily specify the names and variables to save or load by passing to the **tf.save.Saver()** constructor in the following either way:

  - A list of variables (which will be stored under their own names).
  
  - A Python Dictionary in which keys are the names to restore and the values are the variable to manage in the current model where you call **tf.save.Saver().restore()**
  
Let's see an example code.

```python
import os
import tensorflow as tf
# To save checkpoint file
LOG_DIR = os.path.join(os.getcwd(),"log/")

if not os.path.exists(LOG_DIR):
    os.makedirs(LOG_DIR)
    print(LOG_DIR+" is created!\n")
else:
    print("you have already"+LOG_DIR+" !\n")

print("the current working directory:", LOG_DIR, "\n")

tf.reset_default_graph()

# Create some variables.
v1 = tf.get_variable("v1", [3], initializer = tf.zeros_initializer)
test = tf.get_variable("v2", [5], initializer = tf.zeros_initializer)

# Add ops to restore "test" name variable from "v2" variable saved previously
saver = tf.train.Saver({"v2": test})

# Use the saver object normally after that.
with tf.Session() as sess:
    # To draw  a graph of this session on Tensorboard
    writer = tf.summary.FileWriter(LOG_DIR)
    writer.add_graph(sess.graph)
    # Initialize v1 since the saver will not.
    v1.initializer.run()
    saver.restore(sess, os.path.join(LOG_DIR, "model.ckpt"))
    
    print("=== check restore variable ===")
    print("v1 : %s" % v1.eval())
    print("test(the value of v2 on previous model saved) : %s" % test.eval())
    writer.close()
```

Be carefule of the followings:

  - You can create as many **tf.save.Saver()** as you want if you need to save adn restore different subsets of the model variables. The same variable can be listed in multiple saver object; its value is only changed when the **tf.save.Saver().restore()** method is run.
  
  - If you restore a subset of the model variables at the start of a session, you have to run an initialize op for the other variables.
  
  - By default, **tf.save.Saver()** uses the value of the **tf.Variable.name** property for indetification of each variable to restore. However, when you create a **Saver** object, you may optionally choose names for the variables in the checkpoint files.
  
If you want to check an executed example code above, visit [06.Saving_and_Restoring](https://github.com/hyunyoung2/hyunyoung2_Machine_Learning/blob/master/Tutorial/Tensorflow/01.BasicTensorflow/06.Saving_and_Restoring_of_Variables.ipynb) of hyunyoung2 git rep  
  
# Reference

  - [Saving and Restoring section of Tensorflow r1.4](https://www.tensorflow.org/programmers_guide/saved_model)
  
  - [tf.reset_default_graph](https://www.tensorflow.org/api_docs/python/tf/reset_default_graph)
