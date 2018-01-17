---
layout: post
title: Basic Shell Script
subtitle: The basic concept for shell script programming
category: Natural Language Processing Labs
tags: [linux, shell script]
permalink: /2018/01/17/Shell_Script/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

A shell provide you with an interface to unix or linux. Shell gatehrs input from you and executes programs based on that input. 

i.e. shell is an environment in which we can run our commands, programs, and shell scripts. 

# Shell Prompt

The **$** is called **command prompt**. look at How can we run shell command:

```shell
# hyunyoung2 @ hyunyoung2-desktop in ~ [13:04:25] 
$ date 
2018. 01. 17. (수) 13:04:32 KST
```

Keep in mind, there are much types of shell like bourne shell, c shell, z shell and so forth. 

# Shell script

Shell script is a list of commands. which are listed in the order of execution.

When you make shell cript, its extension is **.sh**. 

Before you continue to do shell programming on shell script, First of all, you need to alert the system like linux that a shell script id beding started. 

This is done using **shebang** construct like this:

```shell
#!/bin/sh
```
Basically, **#** means comment. But if you write like the above thing. This tells the system(Linux or UNIX) that the commands that follows are to be executed by the Bourne shell.

It's called a **shebang** becuase the **!** is called **bang** and **#*** is called **hash**.

Basic shell script is: 

```shell
#!/bin/sh

pwd

date
```

The result of the input is: 

```shell 
# hyunyoung2 @ hyunyoung2-desktop in ~ [13:19:16] C:126
$ chmod +x test.sh 

# hyunyoung2 @ hyunyoung2-desktop in ~ [13:19:27] 
$ ./test.sh
/home/hyunyoung2
2018. 01. 17. (수) 13:19:30 KST
```

As you can check from the resulting output of shell cript above, After making shell script, you have to change the shell script to be executable like this.

> $ chmod +x the-shell-script

## Variable

you can also use variable concept like other programming language like this:

```shell
# hyunyoung2 @ hyunyoung2-desktop in ~ [13:04:32] 
$ NAME="test"

# hyunyoung2 @ hyunyoung2-desktop in ~ [13:05:20] 
$ NUMBER_TEST=20

# hyunyoung2 @ hyunyoung2-desktop in ~ [13:05:33] 
$ echo $NAME $NUMBER_TEST
test 20
```

When you intialize a variable, use asignment sign like **NAME="test"**. 

After assigning a variable, if you want to refer to it, use a symbol like **$the-name-of-variable**.

Shell also have Special Variable. in particular, we will say an example of Special Variable like this:

> $? - The exit status of the last command executed. 

This variable is useful when you execute program or command, it let you know what kind of termination happened.

When you call shell script or a function in shell script, the argument is $1, $2, .... $9 are position parameter, with  $0 pointing to the actual command, program, shell script.

## Decision statements

  - if..fi statement 
  
  - if..elif..fi statement
  
  - if..elif..esle..fi statement
  
  - the case...esca statement
  
Let's say, 
 
```shell 
#!/bin/sh

a=10
b=20

if [ $a == $b ]
then
   echo "a is equal to b"
elif [ $a -gt $b ]
then
   echo "a is greater than b"
elif [ $a -lt $b ]
then
   echo "a is less than b"
else
   echo "None of the condition met"
fi
```

on execution 

```shell
 $ a is less than b
```

In the case,

```shell 
#!/bin/sh

FRUIT="kiwi"

case "$FRUIT" in
   "apple") echo "Apple pie is quite tasty." 
   ;;
   "banana") echo "I like banana nut bread." 
   ;;
   "kiwi") echo "New Zealand is famous for kiwi." 
   ;;
esac
```
on execution 

```shell
 $ New Zealand is famous for kiwi.
```

## Loops of shell

Shell has four types of loops like **while**, **for**, **until**, **select**. BUT, here I will walk through two of while and for. 

While loop statement:

```shell
#!/bin/sh

a=0

while [ $a -lt 10 ]
do
   echo $a
   a=`expr $a + 1`
done
```

For loop statement

```shell
#!/bin/sh

for var in 0 1 2 3 4 5 6 7 8 9
do
   echo $var
done
```

output of both while loop and for loop : 

```shell
0
1
2
3
4
5
6
7
8
9
```

As you can know, the concept of for and while loop is the same from C/C++ and other languages. 

## Function 

The concept of function is also the same from C/C++ and other languages. 

Let's see how to use it syntactically.

```shell
#!/bin/sh

# Define your function here
Hello () {
   echo "Hello World"
}

# Invoke your function
Hello
```
on execution, 

```shell
$./test.sh
Hello World
```

As you can see, the declaration of function looks like:

> function_name () {  
 list of commands   
}

Also you return a value like this: 

```shell
#!/bin/sh

# Define your function here
Hello () {
   echo "Hello World $1 $2"
}

# Invoke your function
Hello Zara Ali
```

On execution:
```shell
$./test.sh
Hello World Zara Ali
```

##  command substitution

Command substitution is the mechanism by which the shell performs a given set of commands and then substitutes their output in the place of the commands. 

**Syntax**

Ths command subsitution is performed when a command is given as: 

> \`command\`

**When performing the command substitution make sure that you use the backquote, not the single qoute character**.

**Example**

```shell
#!/bin/sh

DATE=`date`
echo "Date is $DATE"

USERS=`who | wc -l`
echo "Logged in user are $USERS"

UP=`date ; uptime`
echo "Uptime is $UP"
```

on execution:

```shell
Date is Wed Jan 17 04:53:06 UTC 2018
Logged in user are 0
Uptime is Wed Jan 17 04:53:06 UTC 2018
 04:53:06 up 29 days, 23:12,  0 users,  load average: 74.24, 73.94, 73.71
```

# Reference 

 - [Tutorials point of shell programming](https://www.tutorialspoint.com/unix/unix-what-is-shell.htm)
