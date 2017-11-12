---
layout: post
title: What is the jupyter notebook of python
subtitle: I will let you know how to install jupyter and use it.
category: Python
tags: [language, python]
permalink: /2017/05/15/Jupyter_Notebook/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
---

I saw [a certain site](http://pinkwink.kr/815) explaining how to draw the vectors with matplotlib of python. 

while I was reading the [above site](http://pinkwink.kr/815), I felt interested in the jupyter. Fortunately, I found [Jupyter notebook](http://jupyter.org/) that is web application for python interpreter. 

So In here, I will explain a little about jupyter. You can also find out an example of jupyter notebook in [this site](https://github.com/wesm/pydata-book)


## How to install jupyter 

On window 10 :

"pip install ipython[all]" OR "pip install ipython"

> pip install ipython[all] : everything related to ipython is installed. 

![](/img/Image/Languages/Python/2017-05-15-Jupyter_Notebook/ipython_on_windows.JPG)

OR 

The following is what I recommend to you about installation of jupyter notebook : 

"pip install jupyter"

![](/img/Image/Languages/Python/2017-05-15-Jupyter_Notebook/jupyter_on_windows.JPG)


I recommed you for installing juypter that the above is how you can install jupyter. 


**if you want to execute jupyter**


"jupyter notebook"


if you enter the above command in cmd window. 

in cmd window :

![](/img/Image/Languages/Python/2017-05-15-Jupyter_Notebook/execution_of_jupyter_notebook.JPG)

you will get this wab page. 

![](/img/Image/Languages/Python/2017-05-15-Jupyter_Notebook/jupter_test.JPG)


lastly, You can do programming in jupyter and also see graph and result at once. 

![](/img/Image/Languages/Python/2017-05-15-Jupyter_Notebook/jupter_test.JPG)

Also you can share the jupyter file, extension of ipynb.

That way is so easy. 

![](/img/Image/Languages/Python/2017-05-15-Jupyter_Notebook/nbviewer_of_jupyter.JPG)

In the above searching window, If you enter the address where your ipynb is placed. you would get the result of executing jupyter as follows.

![](/img/Image/Languages/Python/2017-05-15-Jupyter_Notebook/result_of_nbviewer_of_jupyter.JPG)

If you want to see the above jupyter nbviewer, click [here](https://nbviewer.jupyter.org/github/hyunyoung2/hyunyoung2.github.io/blob/master/img/Image/Languages/Python/2017-05-15-Jupyter_Notebook/Jupyter%20test%20with%20matplotlib.ipynb).

After finding this jupyter, I will use this tool for python coding. 

So If you want to know the brief information about how to use ipython notebokk (more recently known as jupyter notebook).

Just click [this site, ipython tutorial of Stanford 231 n.](http://cs231n.github.io/ipython-tutorial/) 


**But, The easiest way to install juypter is use of Anaconda.** 

Let's go to [jupyter.org](http://jupyter.org) to look for the way to install Anaconda.

## On  linux with Anancoda

 Just Download Anaconda in [Ananconda download page](https://www.anaconda.com/download/#linux)
 
 ![](/img/Image/Languages/Python/2017-05-15-Jupyter_Notebook/Anaconda_Download.png)
 
 if you download it, go to Downloads directory 
 
 > $ cd Download 
 
 > $ chmod 755 Anaconda3-5.0.1-Linux-x86_64.sh
 
```bash
# hyunyoung2 @ hyunyoung2-desktop in ~ [22:34:00] 
$ cd Downloads 

# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [22:34:03] 
$ ls
Anaconda3-5.0.1-Linux-x86_64.sh
```

  after the above 
 
 > $ ./.Anaconda3-5.0.1-Linux-x86_64.sh

```bash
after the above 
 
# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [22:27:43] C:1
$ ./Anaconda3-5.0.1-Linux-x86_64.sh 

Welcome to Anaconda3 5.0.1

In order to continue the installation process, please review the license
agreement.
.......
cryptography
    A Python library which exposes cryptographic recipes and primitives.


Do you accept the license terms? [yes|no]
[no] >>> yes

Anaconda3 will now be installed into this location:
/home/hyunyoung2/anaconda3

  - Press ENTER to confirm the location
  - Press CTRL-C to abort the installation
  - Or specify a different location below

[/home/hyunyoung2/anaconda3] >>> 
PREFIX=/home/hyunyoung2/anaconda3
installing: python-3.6.3-hc9025b9_1 ...
.......
installation finished.
Do you wish the installer to prepend the Anaconda3 install location
to PATH in your /home/hyunyoung2/.bashrc ? [yes|no]
[no] >>> yes

Appending source /home/hyunyoung2/anaconda3/bin/activate to /home/hyunyoung2/.bashrc
A backup will be made to: /home/hyunyoung2/.bashrc-anaconda3.bak


For this change to become active, you have to open a new terminal.

Thank you for installing Anaconda3!
```

 After finishing installation. 
 
 > $ vim .bashrc

 you see the change of anaconda installation on the last line in .bashrc file. 

 the chage is as follows :
 
```shell
# added by Anaconda3 installer
export PATH="/home/hyunyoung2/anaconda3/bin:$PATH"
```

  From now on, you can run jupyter notebook, run the following command at the terminal
  
  > $ jupyter notebook

  
  **BUT**, in your zsh, you can't run jupyter notebook. 
  
  So like the chage of .bashrc file, you have to change .zshrc file.
  
  Just Add it at the last line of .zshrc like the following :
  
```
# User configuration

# export MANPATH="/usr/local/man:$MANPATH"

# added by hyunyoung2 for Anaconda3
export PATH="/home/hyunyoung2/anaconda3/bin:$PATH"
```
  
  From now on, You can also run jupyter notebook 
  
  after change of .zshrc, type like this to run jupyter notebook on zsh
  
  > $ jupyter notebook
  
## On linux without Anancoda

  [The official site](http://jupyter.org/install.html) of jupyter notebook tells you how to install without Ananconda. 
  
  the way to install jupyter notebook : 
  
  use python package manager,**pip**
  
  if you have Python3 installed(which jupyter notebook's official site recommend) :
  
```
python3 -m pip install --upgrade pip
python3 -m pip install jupyter
```
  
  if you have Python2 installed :
  
```
python -m pip install --upgrade pip
python -m pip install jupyter
```

  Congratulations! you have installed Juypter notebook!. To run notebook 
  
  type like the following : 
  
  > jupyter notebook

# Reference 

  - [Official sit of jupyter](http://jupyter.org/)
  
  - [Official site of installation](http://jupyter.org/install.html)

  - [Korean site of explaining ipython](http://pinkwink.kr/711)
  
  - [Korean site of explaing Nbextensions](http://pinkwink.kr/928)
  
  for more useful way to use jupyter. 
  
  - [jupyter_contrib_nbextension's github](https://github.com/ipython-contrib/jupyter_contrib_nbextensions)
  
