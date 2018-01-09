---
layout: post
title: What it the variable in Tensorflow?
subtitle: Tutorial I wrote in my repository, 02. Variable.
category: Tensorflow
tags: [tensorflow]
permalink: /2018/01/06/What_Is_The_Variable_In_Tensorflow/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

<!-- from https://github.com/hyunyoung2/hyunyoung2_Machine_Learning/blob/master/Tutorial/Tensorflow/01.BasicTensorflow/02.Variable.ipynb -->

#  What is the variable in Tensorflow?

When you create model, you use variable to hold and update parameters. varibale are in-memory buffer containing tensors. The varibles must be explicitly initialized and can be saved to disk during and after training. Later on, You can restore it to exercise and analyze the model(**tf.train.Saver**).

Programming of Tensorflow make a collection of ops producing tensors as **a graph**. Executing a collection of ops is moving a tensor between ops.

Let's how to Create varialbe in Tensorflow.

When you create a Variable, you pass a **Tensor** as its value to the **Variable()** constructor.

```python
# Create two variables.
weights = tf.Variable(tf.random_normal([784, 200], stddev=0.35),
                      name="weights")
biases = tf.Variable(tf.zeros([200]), name="biases")
```

As you can check above, **tf.random_normal(shape)** and **tf.zeros(shape)** produce tensor.

   - Calling **tf.Variable** adds several ops to the computational graph
   
       - A **varialbe** op that holds the variable value. 
       
       - An initializer op that sets the variable to its value. This is actually as **tf.assign** op. 
       
       - The ops for the initial value, such as **zeros** op for **bias** variable in  example above are also added the graph.
       
##  How to Initialize a variable

Variable initializers mus be explicitly run before other ops in your model of tensorflow can be run. 

The way to initialize varialbes : 

   - Add an op that run all the variable initializer and run that op before using the model(Currently, I am dealing with this way). 
 
 
   - Alternatively, You can restore variable values from a checkpoint file(I will not cover this here).

### Use tf.global_variables_initializer()

This op is to run varialble initialziers. Only run that op after you have fully constructed your model and launched it in a session:

```python
# Create two variables.
weights = tf.Variable(tf.random_normal([784, 200], stddev=0.35),name="weights")

biases = tf.Variable(tf.zeros([200]), name="biases")
# a portion your molde operate ...
# Add an op to initialize the variables.
init_op = tf.global_variables_initializer()
# Later, when launching the model
with tf.Session() as sess:
  # Run the init operation.
  sess.run(init_op)
  # ...
  # Use the model
  # ...
```     

### Initialization from another Variable

This way is using the initial value of another varialbe to initialize a variable. 

```python
# Create a variable with a random value.
weights = tf.Variable(tf.random_normal([784, 200], stddev=0.35),name="weights")
# Create another variable with the same value as 'weights'.
w2 = tf.Variable(weights.initialized_value(), name="w2")
# Create another variable with twice the value of 'weights'
w_twice = tf.Variable(weights.initialized_value() * 2.0, name="w_twice")
```


### Summary of initializing variables

As you can know above, **tf.global_variables_initializer()** initialize variables of a colloecntion, **tf.GraphKeys.GLOBAL_VARIBALES**.

```python
sesssion.run(tf.global_variables_initializer())
```

BUT, If you want to initialize variables yourself, use like the follwoing

```python
session.run(weights.initializer)
```

Also, you can inspect which variables have still now been initialized. 

```python
print(session.run(tf.report_uninitialized_variables())
```

# Variable Property

With exception of tf.Variable, another types of tensor is immutable. i.e. during an execution of a model, a single tensor value is the same up to in the end of the executing. But **tf.Variable** can be changed by runing some ops on it. 

The big property of **tf.Variable** is:

   - tf.Variable exists outside of the context of a single **session.run** call. 
   
   
   - Interally, a **tf.Variable** stores a persistent tensor. Specific ops on it allow you to read and modify the value of this tensor. And these modifications are visible across multiple **tf.Session**, So multiple workers can see the same values for a tf.Variable. 
   
   ```python
def variables():
    tf_variable = tf.Variable(tf.random_normal([2,2]), name="tf_variable_test")
    
    return tf_variable

# First create one tf_variable. 
result1 = variables()
# Second, Another variable is created in the second call. 
result2 = variables()
```

As you see above, you have already one variable. But after calling the function of variable twice, This will create two variables. i.e. result1 and result2 indicate different variable.

   - By default, every **tf.Variable** gets placed in the following two collections:
       - **tf.GraphKeys.GLOBAL_VARIABLES**,  
       - **tf.GraphKeys.TRAINABLE_VARIABLES**.
   
BUT, **tf.get_variable** function is the best way to only create a variable once. 

# What is the tf.get_variable function?

In Tensorflow, there are Basically two ways, those is using **tf.Variable** and **tf.get_variable()**.

**tf.get_variable()** function can allows you to reuse a previously created variable of the same name. So this function make it easy to reuse a certain layer in a model.

First of all, Here is how to call **tf.get_variable** function to create a variable.

> tf.get_variable( name ,  shape , intitializer)

the **tf.get_variable** is used to get a already created variable or create a new variable without a exting variable called name that you name when you call **tf.get_variable**.

To create a variable with **tf.get_variable**, enter the name and shape for a variable you want to creat. 

```python
my_variable = tf.get_variable("my_variable",  [2,2])
```

Also you can specify the initializer and datatype for a variable: 

```python
my_specific_variable = tf.get_variable("my_specific_variable", [2,3], dtype=tf.int32, initializer=tf.zeros_initializer)
```

But if not specifying datatype and initialzier, By default, in Tensorflow the datatype is tf.float32 and the initialzier is **tf.glorot_uniform_initializer**.

BUT, If you use a tensor as initializer. you shoud not specify the variable shape, Because the shape of initializer will be used. 

```python
other_variable = tf.get_variable("other_variable", dtype=tf.int32, initializer=tf.constant([23, 42]))
```

If you want to check an executed example code above, visit [02.variable of hyunyoung2 git repository](https://github.com/hyunyoung2/hyunyoung2_Machine_Learning/blob/master/Tutorial/Tensorflow/01.BasicTensorflow/02.Variable.ipynb) 

# Reference

   - [Guides r0.12](https://www.tensorflow.org/versions/r0.12/how_tos/variables/)
   
   - [Intialization function of Tensorflow r0.12](https://www.tensorflow.org/versions/r0.12/api_docs/python/constant_op/)
      
   - [Sharing section of Howto of Tensorflow r0.12](https://www.tensorflow.org/versions/r0.12/how_tos/variable_scope/#how_does_variable_scope_work) 
      
   - [Tensors section of Programmer's guide of Tensorflow](https://www.tensorflow.org/programmers_guide/tensors)
     
   - [Variables section of Programmer's guide of Tensorflow](https://www.tensorflow.org/programmers_guide/variables)
   
   
```
