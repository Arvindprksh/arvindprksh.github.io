---
layout: post
title: What it the sharing variable in Tensorflow?
subtitle: Tutorial I wrote in my repository, 02. Variable.
category: Tensorflow
tags: [tensorflow]
permalink: /2018/01/09/What_Is_The_Sharing_Variable_In_Tensorflow/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

<!-- from https://github.com/hyunyoung2/hyunyoung2_Machine_Learning/blob/master/Tutorial/Tensorflow/01.BasicTensorflow/03.Sharing_Variable.ipynb -->

# What it the sharing variable?

When you do programming of Tensorflow, you have no choice but to use variables, That's becuse it is mutable in a Tensorflow. calculating gradient, It is nedded to adjust gradient descent. 

Sometimes, if you want to reuse a variable, your choice is **tf.get_variable()**.

the **tf.get_variable()** prevents you from wasting a memory space than using **tf.Variable()**.

Let's see simple an example.

Imagine you create a simple function for add with two tf.Variable(), your code in the Tensorflow looks like:

```python
# function to  Add two variables 
# tf.Tensor is implicitly named like <OP_NAME>:<i>
# <OP_NAME>: the name of operation produce the tensor.
# <i>:  integer representing the index of the tensor among the operation's outputs.
def add_function():
    x = tf.Variable(3, name="x_scalar")
    y = tf.Variable(2, name="y_scalar")
    addition = tf.add(x,  y, name="add_function")
    print("=== checking Variables ===")
    print("x:", x, "\ny:", y, "\n")
    return addition

# To check whether or noe result1 and result2 is different
# First Call creates one set of 2 variables.
result1 = add_function()
# Second Call creates another set of 2 variables.
result2 = add_function()
```
here you already have 2 different variables in add_function(), whenever calling the add_function(), it creates each set of 2 variable in add_function().    


The result of calling **add_function()** twice looks like :

```shell
# === result1 = add_function() ===
x: <tf.Variable 'x_scalar:0' shape=() dtype=int32_ref> 
y: <tf.Variable 'y_scalar:0' shape=() dtype=int32_ref> 

# === result2 = add_function() ===
x: <tf.Variable 'x_scalar_1:0' shape=() dtype=int32_ref> 
y: <tf.Variable 'y_scalar_1:0' shape=() dtype=int32_ref> 

# === the result1 and result2 ===
result1: Tensor("add_function:0", shape=(), dtype=int32) 
result2: Tensor("add_function_1:0", shape=(), dtype=int32) 
```

As you can see above, the name of each variables are different. 

If you want to share variables within **add_function()**, Basic ways to share variables is to create them in a seperate piece of code and pass them into the functions that use it.

If you use dictionary, it looks like:

```python 
# The way to share two variables declared in one place 
variables_dict = {"x_scalar": tf.Variable(3, name="x_scalar"), 
                 "y_scalar": tf.Variable(2, name="y_scalar")}

# tf.Tensor is implicitly named like <OP_NAME>:<i>
# <OP_NAME>: the name of operation produce the tensor.
# <i>:  integer representing the index of the tensor among the operation's outputs.
def add_function(x, y):
    addition = tf.add(x,  y, name="add_function")
    print("=== checking Variables ===")
    print("x:", x, "\ny:", y, "\n")
    return addition

# To check whether or noe result1 and result2 is the same
# First Call creates one set of 2 variables.
result1 = add_function(variables_dict["x_scalar"], variables_dict["y_scalar"])
# Second Call also creates the same set of 2 variables.
result2 = add_function(variables_dict["x_scalar"], variables_dict["y_scalar"])
print("=== checking Variables ===")
print("result1:", result1, "\nresult2:", result2, "\n")

# To initialize all variables in this default graph.
global_init_op = tf.global_variables_initializer()

with tf.Session() as sess:
    sess.run(global_init_op)
    print("=== checking Variables in a Session ===")
    print("result1:", result1, "\nresult2:", result2, "\n")
    result1_, result2_ = sess.run([result1, result2])
    print("=== the value each tensor has ===")
    print("result1:", result1_, "\nresult2:", result2_)
    print("[result1, result2]:", sess.run([result1, result2]))
```

The resulting tensors look like:

```shell
=== checking Variables ===
x: <tf.Variable 'x_scalar_2:0' shape=() dtype=int32_ref> 
y: <tf.Variable 'y_scalar_2:0' shape=() dtype=int32_ref> 

=== checking Variables ===
x: <tf.Variable 'x_scalar_2:0' shape=() dtype=int32_ref> 
y: <tf.Variable 'y_scalar_2:0' shape=() dtype=int32_ref> 

=== checking Variables ===
result1: Tensor("add_function_2:0", shape=(), dtype=int32) 
result2: Tensor("add_function_3:0", shape=(), dtype=int32) 
```

Both x varaible and y variable are the same. However result1 and result2 is different in operation named.

Another way to share variables like the above case is to use **classes**. i.e. static class variable can be used to share variable in different instance from the class or it makes **variables_dict** a class to only include varaibles.

When you use class, one is to create a model using class. the other is to create class to only include variables. i.e. the classes take care of managing the variables they need.

For a lighter solution than using class. use _Variable Scope_ mechanism with **tf.get_variable()**

# Understanding tf.get_variable() 

From now on, let's understanding **tf.get_variable()**. This API has a role of creating new variable or resue the existing variable using **variable scope name + variable name**.

let's understand how **tf.getvariable()** works.

The way to call **tf.get_variable()** is : 

> v = tf.get_variable(name, shape, dtype, initializer)

```python
## How tf.getvarialbe works
# First Call create a tensor named "x_scalar"
x = tf.get_variable("x_scalar", [])
# Tensorflow aslo knows creating a tensor name "x_sclar" in a Second Call
# But, at this time, error happen like this:
# That's why reuse option is False 
y = tf.get_variable("x_scalar", []) # error message -> Variable x_scalar already exists, disallowed ...
```

As you can notice in a sample code, By defualt, whenever you call **tf.get_variable()**, it try to create new one named as specified in name argument.    

The **tf.get_varaible()** does one of The following things depending on the scope it is called in.

  - Case 1: The scope is set to create new variable as evidenced by **tf.get_variable_scope() == False**. 
  
  - Case 2: The scope is set to reuse the already existing variable as evidenced by **tf.get_variable_scope() == True**.
  
the cases, of course, both depend on the scope it is called in. 

First of all, let's walk through the frist case, **tf.get_variable_scope() == False**.

If you declare like this:

```python
# By default, resue optiong is set to False
test = tf.get_variable("test_vector", [2]) # Variable scope "variable name" -> test_vector
print("=== variable scope ===") # test.op.name: test_vector 
print("test.name:", test.name) # test.name: test_vector:0
print("test.op.name:", test.op.name, "\n") # test.op.name: test_vector 
assert test.name == "test_vector:0"

# with context statement
with tf.variable_scope("test"):
    v = tf.get_variable("v_vector", [2]) # Variable scope "scope/variable name" -> test/v_vector
print("=== variable scope ===") # === variable scope ===
print("v.name:", v.name) # v.name: test/v_vector:0
print("v.op.name:", v.op.name) # v.op.name: test/v_vector
assert v.name == "test/v_vector:0"
```

Ahead of creating variable named the current variable scope name + the provided name to **tf.get_variable()**

How tf.get_variable() works is to check whether or not a variable does not exist yet with the full name equal to the current variable scope name + the provided name. If not, **tf.get_variable()** create a new variable. however, If it exists **tf.get_variable()** will raise a **ValueError**.

Second, Let's walk through the second case, **tf.get_variable_scope() == True**.

```python 
# with context statement
with tf.variable_scope("test"):
    var = tf.get_variable("var_vector", [2]) # Variable scope -> test/var_vector
with tf.variable_scope("test", reuse=True):
    var1 = tf.get_variable("var_vector", [2])
print("=== variable scope ===")
print("var.name:", var.name, "| var1.name:", var1.name)
print("var.op.name:", var.op.name, "| var1.op.name:", var1.op.name)
assert var.name == "test/var_vector:0"
assert var1.name == "test/var_vector:0"
assert var1 is var
```

In this case, **tf.get_variable()** will search for a already exsting variable with full name equal to the current variable scope name + the provided name. If not exists, **tf.get_variable()** raise a **ValueError**. If the variable is found, it will be return. Here, **var1** that **tf.get_variable("var_vector", [2])** returns is the same from **var**

## Another way to set reuse of tf.get_variable()

Let's go through basic of tf.variable_scope():

```python
# with context statement
with tf.variable_scope("test"):
    with tf.variable_scope("simple"):
        obj = tf.get_variable("obj_vector", [2]) # Variable scope -> test/simple/obj_vector
print("=== variable scope ===")
print("obj.name:", obj.name)
print("obj.op.name:", obj.op.name)
assert obj.name == "test/simple/obj_vector:0"
```

As you see above, Nesting variable scope appends their names like directory structure.

When you set the reuse flag up, you can do the same thing by calling **tf.get_variable_scope().resue_variables()**. That is because calling **tf.get_variable_scope().resue_variables()** can retrieve the current variable scope.

```python 
# with context statement
with tf.variable_scope("test"):
    t = tf.get_variable("t_vector", [2]) # Variable scope  -> test/t_vector
    # instead of with tf.variable_scope("test", reuse=True):
    tf.get_variable_scope().reuse_variables()
    t1 = tf.get_variable("t_vector", [2])
print("=== variable scope ===")
print("t.name:", t.name, "| t1.name:", t1.name)
print("t.op.name:", t.op.name, "| t1.op.name:", t1.op.name)
assert t.name == "test/t_vector:0"
assert t1.name == "test/t_vector:0"
assert t1 is t
```

OR

```python
# with context statement
with tf.variable_scope("test") as scope:
    t = tf.get_variable("t_vector1", [2]) # Variable scope  -> test/t_vector
    # instead of with tf.variable_scope("test", reuse=True):
    scope.reuse_variables()
    t1 = tf.get_variable("t_vector1", [2])
print("=== variable scope ===")
print("t.name:", t.name, "| t1.name:", t1.name)
print("t.op.name:", t.op.name, "| t1.op.name:", t1.op.name)
assert t.name == "test/t_vector1:0"
assert t1.name == "test/t_vector1:0"
assert t1 is t
```

Finally, Let's reuse **tf.get_variable()**.

```python
# function to  Add two variables 
# tf.Tensor is implicitly named like <OP_NAME>:<i>
# <OP_NAME>: the name of operation produce the tensor.
# <i>:  integer representing the index of the tensor among the operation's outputs.
def add_function():
    x = tf.get_variable("x_scalar1", [2])
    y = tf.get_variable("y_scalar1", [2])
    addition = tf.add(x,  y, name="add_function1")
    print("=== checking Variables ===")
    print("x:", x, "\ny:", y)
    print("x.name:", x.name, "\ny.name:", y.name)
    print("x.op.name:", x.op.name, "\ny.op.name:", y.op.name, "\n")
    return addition
    
# To check whether or noe result1 and result2 is different
# First Call creates one set of 2 variables.
result1 = add_function()
tf.get_variable_scope().reuse_variables()
# Second Call creates the same set of 2 variables from result1.
result2 = add_function()
print("=== checking Variables ===")
print("result1:", result1, "\nresult2:", result2)
print("result1.name:", result1.name, "\nresult2.name:", result2.name)
print("result1.op.name:", result1.op.name, "\nresult2.op.name:", result2.op.name, "\n")

global_init_op = tf.global_variables_initializer()
with tf.Session() as sess:
    sess.run(global_init_op)
    for _ in range(3):
        result1_ = sess.run(result1)
        print("=== checking Variables in a session ===")
        print(_, "result1_:", result1_)
```

# the additional property of tf.get_variable()

As you have read this article. Note that you cannot set the reuse option flag to **False** explicitly. 

  - you can go back and forth, i.e. you can enter a resuing variable scope and then exit it to go to a non-reusig variable scope one. So the reuse parameter is inherited into all sub scope. also the scope of variable can inherit initializer.
  
  - Capturing Variable scope not depending on the exact name of scope. 
  
  - tf.get_variable shares the name of scope with other op(operations)
  
# the additional property of tf.get_variable()

As you have read this article. Note that you cannot set the reuse option flag to **False** explicitly. 

  - you can go back and forth, i.e. you can enter a resuing variable scope and then exit it to go to a non-reusig variable scope one. So the reuse parameter is inherited into all sub scope. also the scope of variable can inherit initializer.
  
  - Capturing Variable scope not depending on the exact name of scope. 
  
  - tf.get_variable shares the name of scope with other op(operations)
  
 Frist, Let's walk through the flag of reuse inherited.

```python
# Let's walke through the inheritance of resue flag
with tf.variable_scope("root1"):
    print("=== checking reuse and scope of variables ===")
    print("first scope name:", tf.get_variable_scope().name)
    print("first scope reuse:", tf.get_variable_scope().reuse, "\n")
    # At start, the scope is not reusing.
    assert tf.get_variable_scope().reuse == False
    with tf.variable_scope("foo2"):
        print("=== checking reuse and scope of variables ===")
        print("second scope name:", tf.get_variable_scope().name)
        print("scond scope reuse:", tf.get_variable_scope().reuse, "\n")
        # Opened a sub-scope, still not reusing.
        assert tf.get_variable_scope().reuse == False
    with tf.variable_scope("foo1", reuse=True):
        print("=== checking reuse and scope of variables ===")
        print("third scope name:", tf.get_variable_scope().name)
        print("third scope reuse:", tf.get_variable_scope().reuse, "\n")
        # Explicitly opened a reusing scope.
        assert tf.get_variable_scope().reuse == True
        with tf.variable_scope("bar1"):
            print("=== checking reuse and scope of variables ===")
            print("fourth scope name:", tf.get_variable_scope().name)
            print("fourth scope reuse:", tf.get_variable_scope().reuse, "\n")
            # Now sub-scope inherits the reuse flag.
            assert tf.get_variable_scope().reuse == True
    print("=== checking reuse and scope of variables ===")
    print("fifth scope name:", tf.get_variable_scope().name)
    print("fifth scope reuse:", tf.get_variable_scope().reuse)
    # Exited the reusing scope, back to a non-reusing one.
    assert tf.get_variable_scope().reuse == False
```

As you can see python code above, the reuse of "root1/foo1/" i set to **True**, since that scope, the reuse of nesting scope is implicitly set to **True**, evev though you specify the  flag of reuse to **True**. Keep in mind of it!

Let's Walk through capturing scope with a with block :

```python 
# Let's walk through capturing scope ot initialze a variable scope based on another one.
with tf.variable_scope("foo") as foo_scope:
    v = tf.get_variable("v", [1])
    print("=== checking reuse and scope of variables ===")
    print("the first scope:", tf.get_variable_scope().name)
    print("the reuse flag of the first scope:", tf.get_variable_scope().reuse)
    print("v.name:", v.name, "|", "v.op.name:", v.op.name, "\n")
with tf.variable_scope(foo_scope):
    w = tf.get_variable("w", [1])
    print("=== checking reuse and scope of variables ===")
    print("the second scope:", tf.get_variable_scope().name)
    print("the reuse flag of the first scope:", tf.get_variable_scope().reuse)
    print("w.name:", w.name, "|", "w.op.name:", w.op.name, "\n")
# you don't have to use the exact string for a variable scope. 
# capturing a variable scope helps you make a mistake like this.
with tf.variable_scope(foo_scope, reuse=True):
    print("=== checking reuse and scope of variables ===")
    print("the third scope:", tf.get_variable_scope().name)
    print("the reuse flag of the first scope:", tf.get_variable_scope().reuse)
    v1 = tf.get_variable("v", [1])
    w1 = tf.get_variable("w", [1])
    print("v1.name:", v.name, "|", "v1.op.name:", v.op.name)
    print("w1.name:", v.name, "|", "w1.op.name:", v.op.name)
    
print("the scope of foo_scope:", foo_scope.name)
assert v1 is v
assert w1 is w
```

as you can see above, a with block can capture **tf.variable_scope()**. and then the variable scope is maintained out of the orginal with block.

So If you use this property well, transferring several variable scopes is very easy an convenient.

```python 
with tf.variable_scope("foo_test") as foo_scope:
    print(foo_scope)
    print("=== checking reuse and scope of variables ===")
    print("the first scope:", tf.get_variable_scope().name)
    print("the reuse flag of the first scope:", tf.get_variable_scope().reuse, "\n")
    assert foo_scope.name == "foo_test"
with tf.variable_scope("bar_test"):
    print("=== checking reuse and scope of variables ===")
    print("the first scope:", tf.get_variable_scope().name)
    print("the reuse flag of the first scope:", tf.get_variable_scope().reuse, "\n")
    with tf.variable_scope("baz_test") as other_scope:
        print("=== checking reuse and scope of variables ===")
        print("the first scope:", tf.get_variable_scope().name)
        print("the reuse flag of the first scope:", tf.get_variable_scope().reuse, "\n")
        assert other_scope.name == "bar_test/baz_test"
        with tf.variable_scope(foo_scope) as foo_scope2:
            print(foo_scope)
            print("=== checking reuse and scope of variables ===")
            print("the first scope:", tf.get_variable_scope().name)
            print("the reuse flag of the first scope:", tf.get_variable_scope().reuse, "\n")
            assert foo_scope2.name == "foo_test"  # Not changed.
```

As you can check, in the case of **foo_scope2**, the scope of variable come back to  the scope of **foo_scope**. as above, you can move the scope freely if you use capturing the scope of variable. 

Let's simply walk through inheriting initializer.

```python
# Let's walk through inheriting initializer.
with tf.variable_scope("initiializer", initializer=tf.constant_initializer(0.4)):
    v = tf.get_variable("v", [1])
    w = tf.get_variable("w", [1], initializer=tf.constant_initializer(0.3))
    with tf.variable_scope("initiializer_inherited"):
        v1 = tf.get_variable("v", [1])
    with tf.variable_scope("solely_initiializer", initializer=tf.constant_initializer(0.2)):
        v2 = tf.get_variable("v", [1])
    
global_init_op = tf.global_variables_initializer()
with tf.Session() as sess:
    sess.run(global_init_op)
    v_, w_, v1_, v2_ =sess.run([v, w, v1, v2])
    print("=== check what kind of initialize is used ===")
    print("v_(0.4):", v_) 
    print("w_(0.3):", w_)
    print("v1_(0.4):", v1_)
    print("v2_(0.2):", v2_, "\n")        
```

As you can notice above, the scope of "initializer_inherited" is the same from the initializer of the scope of "initializer".

To sum up, variable scope can carry a default initializer. sub-scope inherit it, and it is passed into each **tf.get_variable()** call. However If you specify another initialzier explicitly, it can be overridden.

Let's go through how much using variable scope appects the name of ops. 

If you run the lines of code below, you can assure that ops created inside a variable scope share that name of variable scope. That is, When you do with **tf.variable_scope("name")**, This implicitly opens opens a **tf.name_scope**. 

```python 
# how much using variable scope affect 
with tf.variable_scope("variable_name"):
    x = 1.0 + tf.get_variable("v", [1])
    print("=== check op name and variable name ===")
    print("x.name:", x.name)
    print("x.op.name:", x.op.name, "\n")
assert x.op.name == "variable_name/add"

# Second experiment with tf.name_scope 
with tf.variable_scope("op_name"):
    with tf.name_scope("name_scope"): # it only influence the name of ops
        v = tf.get_variable("v", [1])
        x = 1.0 + v
        print("=== check op name and variable name ===")
        print("x.name:", x.name, "|", "v.name:", v.name)
        print("x.op.name:", x.op.name, "|", "v.op.name:", v.op.name)
assert v.name == "op_name/v:0"
assert x.op.name == "op_name/name_scope/add"
```

Here you realize that the kind of scope is two, variable scope and op scope. 

**tf.name_scope()** is related to ops. 

**tf.varialbe_scope()** is related to variable. 

# Summary


In Tensorflow, reuse of variable is associated with **tf.get_variable()**. 

two case of using **tf.get_variable()** is:

  - Under reuse, a check will perform to ensure whether or not the variable with full name already exist. if not, ValueError happen. if it exist. **tf.get_variable()** will return a variable with the same full name. 
  
  - Under no resue, a check will perfor to ensure whether the variable with full name already exist or not. At this time. the act of **tf.get_variable()** is opposed to reuse that set to **True**.
  
  If you want to check an executed example code above, visit [03.sharing variable](https://github.com/hyunyoung2/hyunyoung2_Machine_Learning/blob/master/Tutorial/Tensorflow/01.BasicTensorflow/03.Sharing_Variable.ipynb) of hyunyoung2 git repository
  
 # Reference 

  - [Variable sharing section of Tensorflow Programmer's guide_r1.4](https://www.tensorflow.org/programmers_guide/variables#sharing_variables)
  
  - [Sharing section of howto of Guides r0.12](https://www.tensorflow.org/versions/r0.12/how_tos/variable_scope/) 
  
  - [tf.add() API r1.4](https://www.tensorflow.org/api_docs/python/tf/add)
