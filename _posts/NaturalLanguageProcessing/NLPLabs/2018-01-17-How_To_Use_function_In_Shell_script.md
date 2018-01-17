---
layout: post
title: Function usage of shell script
subtitle: How to write function on shell script
category: Natural Language Processing Labs
tags: [linux, shell script]
permalink: /2018/01/17/How_To_Use_function_In_Shell_script/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

When I needed to do shell programming to get material for Deep learning. I studied shell programming about syntax and so on. 

So here I will organize what have studied shell programming, in particular, about function usage. 

When you use bash as your shell, A bash function cannnot return directly a string like you want it to do.

But you can return a value another way as follows :

 - Echo a string
 
 - Return an exit status, which is a number, not a string.
 
 - Share a Varaible. 
 
Let's how to do each of those options:

### 1. Echo a string

```shell
#!/bin/sh


hello () {
    retrieval="Echo a string"

    echo $retrieval
}

result=$(hello)

echo $result
```

On execution 

```shell
# hyunyoung2 @ hyunyoung2-desktop in ~ [14:14:41] 
$ ./test.sh 
Echo a string
```

As you can see, by calling functiona, the hello function of the code above returns echo value such as a string, "Echo a string".

Also if the variable of **retrieval** is number, it works.


### 2. Return exit status

```shell
#!/bin/sh

hello () {
    retrieval=9
    
    # Yon can also use a string number like "20" instead of number, 9, 
    return $retrieval  
}

# call function 
hello

# exit status of the last command executed
result=$?

echo $result
```

On execute

```shell
# hyunyoung2 @ hyunyoung2-desktop in ~ [14:20:13] 
$ ./test.sh
9
```

In here, if you return a string, you will get error message like:

```shell
# hyunyoung2 @ hyunyoung2-desktop in ~ [14:21:27] 
$ ./test.sh 
./test.sh: 7: return: Illegal number: tests
```

In the case above, I changed the return value into a string, "tests"

### 3. Share variable

This is so easy to understand the process of shaing varialbe.

Just consider that you use global variable. 

```shell
#!/bin/sh

retrieval=9

hello () {

    retrieval=20
}

hello

echo $retrieval
```

On Execution 

```shell
# hyunyoung2 @ hyunyoung2-desktop in ~ [14:24:25] 
$ ./test.sh
20
```

As you can see above, the variable of retrieval is global variable. If you call a function assigning some value to global variable, the value of global variable is changed.

# Reference

 - [Stackoverflow](https://stackoverflow.com/questions/8742783/returning-value-from-called-function-in-a-shell-script)
