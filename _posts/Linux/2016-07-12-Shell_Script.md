---
layout: post
title: Shell Script
subtitle: Let's Study Shell Script
category: Linux
tags: [linux, shell, command]
permalink: /2016/07/12/Shell_Script/
---


  I refer to [this site(linuxcommand)](http://linuxcommand.org/wss0010.php) for understanding how I make shell script
  
  I made this cotents based on bash 
  
# Shell script

## Writing  a script 
  
  A shell script is a file that contains ASCII text. To Create a shell script, you can use a text editor.
  
  Now get started, first type in your first script as follows :
  
```shell
  # !/bin/bash
  # My first script
  
  echo "Hello word!"
```
  
  The first line of the script is important. This is a special clue given to the shell indicating that program is used to interpret the script. In this case, it is /bin/bash. Other scripting languages such as perl, python can also use this mechanism.
  
  Thd second line is a comment. Everything that appears after a "#" symbol is ingnored by bash. As your scripts become bigger and more complicated, Comments become vital. They are used by programmes to exmplain what is going on so that others can figure it out. the last line is the **[echo](http://linuxcommand.org/man_pages/echo1.html)** command. This command simply prints what it is given on the display
  
## Setting permissions 

  The next thing we have to do is give the shell permission to execute your script. this is done with the **[chmod](http://linuxcommand.org/man_pages/chmod1.html)** command as follows :

```shell
$ chmod 755 my_script
```  

  The "755" will give you read, write and excute permission. Everybody else will get only read and excute permission. if you 
  want your script to be private. (i.e, only you can read and execute), use "700" instead.
  
## Putting it in your path

  At this point, your script will run : Try this:
  
```shell
./my_script
```

  You Should See "Hello world!" displayed, If you do not, see what directory you really saved your script in, go there and try again.
  
  When you type in the name of a command, the system does not search the entire computer to find the program is located. that would take a long time. You have noticed that you do not usually have to specify a complete path name to the program you want to run, the shell just seems to know. 
  
  yeah, you'r right. The shell does konw. here is how the shell know about that : the shell mainains a list of directories where executable files are kept, and just searches the directories in that list. if if does not find the program after searching each directory in the list, it will issue the famous __command not found__ error message.
  
  This list of directories is called your path. You can  view the list of directories with the following command :

```shell
echo $PATH
```

  This will return a colon separated list of directories that will be searched if a specific path name is not given when a command is attempted. In our first attempt to execute your new script, You specified path("./") to the file. 
  
  Commands, commands everywhere
  
  Commands can be several different things. Some Commands are built into the shell itself. so to speak, The shell automatically understands a few commands on its own. for example. the commmand **cd** and **pwd** are in this group. Commands implemnted in the shell itself are called __shell built-in__ to see a list of the commands bulit into bash, type in **help** command.
  
  The second type of commands is the executable programs. Most commands are in this group. Executable programs are all the files in the directories included in your path.
  
  **In my case, that I studied, just to do my job past, I just skipped part mking script of HTML.**
  
  just I recommend you to try the tutorail of [the shell sripts(linuxcommand)](http://linuxcommand.org/wss0030.php)
  
 
## Assigning a command's result to a variable
  
  You can also assign the results of a command to a variable :
  
  right_now = $(data + "%x %r %z")
  
  You can even nest the variables (place on inside another), like this :
  
  right_now = $(data + "%x %r %z")
  time_stamp = "Updated on $right_now by $USER"
  
## before flow control, just shell script sample 

  this sample is made by refering to [this site(linuxcommand)](http://linuxcommand.org/wss0080.php) 

```shell
  # !/bin/bash
  # test_page 
  
  ### constants

  TITLE="My System information"
  RIGHT_NOW=$(date + " %x %r %Z")
  TIME_STAMP="Updated on $RIGHT_NOW by $USER"

  ### FUNCTIONS

  function system_info
  {
        #Temporary function stub
        echo "function system_info"
  }

  function show_uptime
  {
        #Temporary function stub
        echo "function show_uptime"
  }

  function drive_space
  {
        #Temporary function stub
        echo "function drive_sapce"
  }

  function home_space
  {
        #Temporary function stub
        echo "ssunction home_space"
  }

  ##### main

  cat <<- __EOF__
  \<HTML>
  \<HEAD>
        \<TITLE>
        $title
        \</TITLE>
  \</HEAD>

  \<BODY>
        \<H1>$title  $HOSTNAME \<H1>
        \<P>TIM_STAMP\</P>
        $(system_info)
          $(show_uptime)
        $(drive_space)
        $(home_space)
  \</BODY>
  \</HTML>
  __EOF__
```

## Flow control

 Now get started about flow control.

 I will look at how to add intelligence to our scripts. So far, the above sripts has only consisted of  a seqeunce of commands that starts at the first line and continues line by line until it reaches the end. Most programs do more than this. 
 They make decision and perform different actions depending on conditions :
 
 The shell provides several commands that we can use to control the flow of execution in our program.
 
 the overall explanation is in [this site(linuxcommand)](http://linuxcommand.org/wss0090.php).
 
 Use echo commands to verify your assumption.  -> this means just if you use the C language, use printf to verify your assumptions.
 

## Wathcing your script run

  It is possible to have bash show you what it is doing when you run your script. To do this, add a "**-x**" to the first line of your script. like this :
  
```shell  
  # !/bin/bash -x
```

  Now, when you run your script, bash will display each line (with subsistitution performed) as it executes it. This Technique is called tracing. here is what it looks like :
  
```shell  
  $./trouble.bash  
  + nubmer = 1
  + '[' 1 = 1 ']'
  + echo 'Number equals 1'
  Number equals 1
```

 also, Alternately, you can use the set command within your script to turn tracing on and off. Use **set -x** to turn tracing on and **set +x** to turn tracing off. For example :
 
```shell
  # !/bin/bash
 
  number=1
  
  set -x
  if [$number = "1"]; then
      echo "Number eaual 1"
  else 
      echo "Number does not equal 1"
  if
  set +x
```

## Read

  To get input from keyboard, you use the read command, The read command takes input from the keyboard adn assigns it to variable. Here is an example :
  
```shell
  # !/bin/bash
  
  echo -n "Enter some text > "
  read text
  echo "You etered : %text"
```
  
  As you can sse, we displased a prompt on line 3. Note that "-n" given to the command causes it to keep the curso on the same line; i.e., it does not output a carriage return at the end of the prompt.
  
  Next, We invoke the read command with "text" as its argument. what this does wait for the user to type something followed by a carriage return( the Enter key). and then assingn whatever was typed to the avriable text.
  
  here is an example of result 
  
```shell
  $ read_demo.bash
  Enter some text > **this is some text**
  you entered: this is some text
```
  
  if you don't give the **read** command the name of a variable to assign its input, it will use the environment variable REPLAY
  
  the **read** command also takes some command line options. The two most interesting ones are are -t and -s. the -t option followed by a number of seconds provides an automatic timeout for the read command. this means that the **read** command will give up after the specified number of seconds if no response has been received from the user. This option could be used in the case of a script that must continue (perhaps resorting to a default response) even if the user does not answer the prompts
  
  
## Arithmetic 

  let's say you want to use the command line as a primitive calculator. you can do it like this :

```shell
  $ echo $((2+2))
```

  as you can see, when you surround an arithmeic expression with the double parenthese,the shell will perform arithmetic evaluation. 
  
  Notice that whitespace is not very important :

```shell
  $ echo $((2+2))     
  4     
  $ echo $(( 2+2 ))    
  4  
  $ echo $((   2+2   ))   
  4  
```

  The shell can perform a variety of common (and not so common) arithmetic operations. here is an example :
  
```shell
  # !/bin/bash
  
  first_num = 0
  second_num =0
  
  echo -n "Enter the first number --> "
  read first_num
  echo -n "Enter the firs number --> "
  read second_num
  
  echo "first number + second number = $((first_num + second_num))"
  echo "first number - second number = $((first_num - second_num))"
  echo "first number * second number = $((first_num * second_num))"
  echo "first number / second number = $((first_num / second_num))"
  echo "first number % second number = $((first_num % second_num))"
  echo "first number raised to the"
  echo "power of the second number =  $((first_num ** second_num))"
```
 
 ## Positional parameter 
 
  this is similar to argv and argc of C language. So, in order to  hadle options on the command line, we use charateristic in the shell called **posional parameters**. Positional Parameters are a series of special variable ($0 througt $9) that contain the contents of the command line.
  
  Let's imagine the following command line :

```shell
  $ some_program word1 word2 word3 
```

  If some_program were a bash shell script, we could read each item on the command line because the positional parameters contanin the following :
  
  * $0 would contain "some_program"
  * $1 would contain "word1"
  * $2 would contain "word2"
  * $3 would contain "word3"

  If you try out this, here is a script

```shell
  # !/bin/bash
    
  echo "positional Parameters"
  echo '$0 = ' $0
  echo '$1 = ' $1
  echo '$2 = ' $2
  echo '$3 = ' $3
```

 
 finally, If you want to know more than the above contents, just click **[linux shell tutorial](http://linuxcommand.org/wss0130.php)**
 
 > thanks for your reading
 

<!--
I want the baby to know my voice. 
 
 all the time -> 줄곧, 매번, 항상 the key's been in my pocket all the time  
 always  -> 습관적 인 거  항상 줄곧 내내
 
 all time ->  여기서 time은 시간 즉 모든 시간, 시간을 통틀어서 
 what is your favorite actor all time (역대로)
 
 I want you to know my name 
 I just wnated to let you know that , about , 
 

 how was your 
 how was your blind date
 how was your filght
 how was your 
 how was your interview
 how was your day-off
 how was your day at work 
 how was your business trip 
 how was your first meeting with her 
 how was your meeting at headquarter
 how was your performance at previous work
 how was your performance in your previous job
 -->
