---
layout: post
title: What is the argparse module of python 
subtitle: how to use argparse module with an example 
category: Python
tags: [python, tutorial]
permalink: /2017/07/08/Command_Line_Arguments_Of_Python/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---


# [Command Line Arguments In Python](https://docs.python.org/2/howto/argparse.html)

I wanted to use my python program on command-line of Linux. So I could find out the way it is similar and easy to make another usage of shell script on Linux.

For example, When you use linux basic program on shell like wc, split and so on. If you don't know how to use it. 

Basically, users type in as follows :

> man wc   
> wc --help   

wc - word count script

As you can see the above cases, Normally there are two ways. But In my case, I will deal with second case, "wc --help" like this. 

![](/img/Image/Languages/Python/2017-07-08-Command_Line_Arguments_Of_Python/Command_Line_Arguments_of_wc.png)

The reason why I want to deal with second case, Nowadays, I'm making some program to probably reuse, So I decided to make the program is easy to use on command line of Linux

So I figured out the hint from C program. the hint is the variables of argc and argv.

From now on, let's see how to make it with python on my purpose

## Argparse module of python 

**this article got refered from [Argparse Tutorial](https://docs.python.org/2/howto/argparse.html) of the official python site.**

This module is so easy to use it on your purpose. But Basically Users would figure out sys module. i.e. sys.argv of sys module

let's see simple program to sys module 

```python 
import sys
print ("the len of sys.argv :", len(sys.argv))
print ("sys.argv[0] :", sys.argv[0])
print ("sys.argv: ", sys.argv)
```

After the above code, if you execute the above python program on command line, you're getting the result as follows :

```bash
# hyunyoung2 @ hyunyoung2-desktop in ~ [15:33:37] 
$ python3 arguments_of_command_line.py 1 2 3    
the len of sys.argv : 4
sys.argv[0] : arguments_of_command_line.py
sys.argv:  ['arguments_of_command_line.py', '1', '2', '3']
```

As you can see, sys.argv variable recognizes the command line in order. So if you want to make it easy to handle command line on your program,

argv is enough to hadle command line, But if you want to make it useful and beatiful. **use argparse module right away**

### The Basic Of Argparse Module

let's see an simple example of the above module

```python 
import argparse
parser = argparse.ArgumentParser()
parser.parse_args()
```

After that, type in the above python program on command line as follows :

```bash
# hyunyoung2 @ hyunyoung2-desktop in ~ [15:34:18] 
$ python3 arguments_of_command_line.py      

# hyunyoung2 @ hyunyoung2-desktop in ~ [15:47:12] 
$ python3 arguments_of_command_line.py -v
usage: arguments_of_command_line.py [-h]
arguments_of_command_line.py: error: unrecognized arguments: -v

# hyunyoung2 @ hyunyoung2-desktop in ~ [15:47:22] 
$ python3 arguments_of_command_line.py foo
usage: arguments_of_command_line.py [-h]
arguments_of_command_line.py: error: unrecognized arguments: foo

# hyunyoung2 @ hyunyoung2-desktop in ~ [15:47:17] C:2
$ python3 arguments_of_command_line.py -h
usage: arguments_of_command_line.py [-h]

optional arguments:
  -h, --help  show this help message and exit
```

You just entered two lines, parser = argparse.ArgumentParser() and parser.parse_args(), But this module make help message automatically. 

And, if you don't specify positional and optional argument, when you use the arguments on command line, error message appears in the shell.

This is so good and convenient to make it using this module of argparse.

### [Introducing Positional Arguments](https://docs.python.org/2/howto/argparse.html#introducing-positional-arguments)

I exactly don't know whether you know positional and optional arguments or not. So from now on, in turn, I will explain what is the positianl arguments and optional arguments. 

First, let's go through an example of how to make positional arguments with argparse module. 

```python 
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("echo", help="echo the string you use here")
args = parser.parse_args()
print (args.echo)
```

With the above lines, if you type in some arguments on the shell. you will get the result as follows:

```bash
# hyunyoung2 @ hyunyoung2-desktop in ~ [16:45:56] C:1
$ python3 arguments_of_command_line.py
usage: arguments_of_command_line.py [-h] echo
arguments_of_command_line.py: error: the following arguments are required: echo

# hyunyoung2 @ hyunyoung2-desktop in ~ [16:46:30] C:2
$ python3 arguments_of_command_line.py foo
foo

# hyunyoung2 @ hyunyoung2-desktop in ~ [16:49:22] 
$ python3 arguments_of_command_line.py --help
usage: arguments_of_command_line.py [-h] echo

positional arguments:
  echo        echo the string you use here

optional arguments:
  -h, --help  show this help message and exit
```

As you can see output above. Positinal arguments make us specify the positional option typing in command to execute our program on the shell. 

i.e. calling our program now require us to specify an option, in here echo option.

you can specify help message of your arguments easily with help keywrod as follows :

> parser.add_argument("echo", help="echo the string you use here")

If you want to make it more useful, read [the part of introducing positional arguments in argparse tutorial](https://docs.python.org/2/howto/argparse.html) in detail  

###  [Introducing Optional Arguments](https://docs.python.org/2/howto/argparse.html#introducing-optional-arguments)

The optional arguments is depending on user who uses program on commandline. 

i.e that is not necessarily specified on command line. 

Let's go through an example : 

```python 
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("-v", "--verbose", help="increase output verbosity", action="store_true")
args = parser.parse_args()
if args.verbose:
   print ("verbosity turned on")
```

let's experiment with the above code. 

```bash
# hyunyoung2 @ hyunyoung2-desktop in ~ [17:08:59] C:2
$ python3 arguments_of_command_line.py --verbose
verbosity turned on

# hyunyoung2 @ hyunyoung2-desktop in ~ [17:09:22] 
$ python3 arguments_of_command_line.py --verbose 1
usage: arguments_of_command_line.py [-h] [--verbose]
arguments_of_command_line.py: error: unrecognized arguments: 1

# hyunyoung2 @ hyunyoung2-desktop in ~ [17:09:38] 
$ python3 arguments_of_command_line.py --help
usage: arguments_of_command_line.py [-h] [-v]

optional arguments:
  -h, --help     show this help message and exit
  -v, --verbose  increase output verbosity
```

As you can see, the optional arguments, if you don't use action keyword, need some value like this :

> python3 (the above python name) --verbose 1(and so on)

But you don't need to specify some value for the optional argument. that's why you use action keyword. 

And if you type in as follows :

> parser.add_argument("-v", "--verbose", help="increase output verbosity", action="store_true")

\-v means short option 

\-\-verbose means long option

those are two the same in their functionality. 

### [Combining Positional And Optional Argumetns](https://docs.python.org/2/howto/argparse.html#combining-positional-and-optional-arguments)

Finally, let's make an simple example with positional and optional arguments

```python 
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("square", type=int, help="display a square of a given number")
parser.add_argument("-v", "--verbosity", action="count", default=0, help="increase output verbosity")
args = parser.parse_args()
answer = args.square**2
if args.verbosity >= 2:
    print ("the square of {} equals {}".format(args.square, answer))
elif args.verbosity >= 1:
    print ("{}^2 == {}".format(args.square, answer))
else:
    print (answer)
```

```bash
# hyunyoung2 @ hyunyoung2-desktop in ~ [17:30:29] 
$ python3 arguments_of_command_line.py 7 -v     
7^2 == 49

# hyunyoung2 @ hyunyoung2-desktop in ~ [17:40:26] 
$ python3 arguments_of_command_line.py -v 7
7^2 == 49

# hyunyoung2 @ hyunyoung2-desktop in ~ [17:40:30] 
$ python3 arguments_of_command_line.py 7 -vv     
the square of 7 equals 49

# hyunyoung2 @ hyunyoung2-desktop in ~ [17:40:41] 
$ python3 arguments_of_command_line.py 7 -vvv
the square of 7 equals 49

# hyunyoung2 @ hyunyoung2-desktop in ~ [17:40:43] 
$ python3 arguments_of_command_line.py 7     
49

# hyunyoung2 @ hyunyoung2-desktop in ~ [17:40:55] C:2
$ python3 arguments_of_command_line.py --help
usage: arguments_of_command_line.py [-h] [-v] square

positional arguments:
  square           display a square of a given number

optional arguments:
  -h, --help       show this help message and exit
  -v, --verbosity  increase output verbosity
```

As you can see, the order of optional option doesn't matter through as follows :

```bash
# hyunyoung2 @ hyunyoung2-desktop in ~ [17:30:29] 
$ python3 arguments_of_command_line.py 7 -v     
7^2 == 49

# hyunyoung2 @ hyunyoung2-desktop in ~ [17:40:26] 
$ python3 arguments_of_command_line.py -v 7
7^2 == 49
```

Plus, In this example, notice that keywords of default and action="count" are dealt with 

So far, you've gone through the basic usage of argparse module.

If you want to know more advanced mode, read [getting a little more advanced of this tutorial](https://docs.python.org/2/howto/argparse.html#getting-a-little-more-advanced)

and if you want to get more advanced than getting a little more advanced, read how to use [argparse module](https://docs.python.org/2/library/argparse.html#module-argparse) in detail  

here is [documentation](https://docs.python.org/2/library/argparse.html#module-argparse) of argparse module

Furthermore, if you want to get a code of the tutorial of argparse module, here is [my github](https://github.com/hyunyoung2/Natural_Language_Processing_Lab/blob/master/Python/Command_Line_argument/commandline_arguments.py) that you can see about the tutorial code.  

# Reference 

 - [Command-line arguments in Python, Java and C](https://notes.mindprince.in/2013/06/30/command-line-arguments-in-python-java-and-c.html)
 
 - [Argparse Tutorial](https://docs.python.org/2/howto/argparse.html)
 
 - [Argparse module](https://docs.python.org/2/library/argparse.html#module-argparse)

 - [argparse ??? Command line option and argument parsing](https://pymotw.com/2/argparse/)
  
 - [argparse ??? Command line option and argument parsing_1](https://bip.weizmann.ac.il/course/python/PyMOTW/PyMOTW/docs/argparse/index.html)
