---
layout: post
title: how to install TensorFlow
subtitle: installing tensorflow on ubuntu 16.04 LTS
category: machine_learning
tags: [machine_learning, tensorflow]
permalink: /2017/06/27/How_To_Install_Tensorflow/ 
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

**referenced from Installing Tensorflow in officail site of tensorflow**

In my computer, I will follow Installing Tensorflow on Ubuntu

Because my environment is Ubuntu16.04 LTS, I also decided to install tensorflow as native pip. 

after following this whole processing, probably you can install tensorflow anywhere. 

Les't play!

First of all, you need to install pip or pip3. 

basically, the pip or pip3 package manager is usually installed on Ubuntu.

if you didn't install them. 

type in like this :

> sudo apt-get install python-pip python-dev  # for Python 2.7    
> sudo apt-get install python3-pip python3-dev # for Python 3.n      

if you run into the following result, 

```bash
hyunyoung2@hyunyoung2-desktop:~$ sudo apt-get install python-pip
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package python-pip
```

you need to update package list

> sudo apt-get update

```bash
hyunyoung2@hyunyoung2-desktop:~$ sudo apt-get update
Get:1 http://us.archive.ubuntu.com/ubuntu xenial InRelease [247 kB]
Get:2 http://security.ubuntu.com/ubuntu xenial-security InRelease [102 kB]
Get:3 http://us.archive.ubuntu.com/ubuntu xenial-updates InRelease [102 kB]       
......
```

plus, if you upgrade your software version to the latest version. it is much better. 

> sudo apt-get -y upgrade   

```bash 
hyunyoung2@hyunyoung2-desktop:~$ sudo apt-get -y upgrade
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Calculating upgrade... Done
The following package was automatically installed and is no longer required:
  snap-confine
Use 'sudo apt autoremove' to remove it.
The following packages have been kept back:
  gnome-software gnome-software-common libmirclient9 linux-generic-hwe-16.04
  linux-headers-generic-hwe-16.04 linux-image-generic-hwe-16.04 python3-software-properties
  software-properties-common software-properties-gtk ubu
.....
```

# pip 

From now on, I am explaining to you under installing the above update or upgrade.

> sudo apt-get install python-pip python-dev     # for python 2.7     
> sudo apt-get install python3-pip python3-dev   # for python 3.n    

**Keep in mind that as of now(2017.06.27) the officail site of tensorflow strongly recommend version 8.1 or higher of pip or pip3.**


if you already installed one of the above them. you got the following screen

- python-pip python-dev

```bash 
hyunyoung2@hyunyoung2-desktop:~$ sudo apt-get install python-pip python-dev
[sudo] password for hyunyoung2: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
python-dev is already the newest version (2.7.11-1).
python-dev set to manually installed.
python-pip is already the newest version (8.1.1-2ubuntu0.4).
The following package was automatically installed and is no longer required:
  snap-confine
Use 'sudo apt autoremove' to remove it.
0 upgraded, 0 newly installed, 0 to remove and 10 not upgraded.
```

- python3-pip python3-dev

```bash
hyunyoung2@hyunyoung2-desktop:~$ sudo apt-get install python3-pip python3-dev
Reading package lists... Done
Building dependency tree       
Reading state information... Done
python3-dev is already the newest version (3.5.1-3).
python3-dev set to manually installed.
python3-pip is already the newest version (8.1.1-2ubuntu0.4).
The following package was automatically installed and is no longer required:
  snap-confine
Use 'sudo apt autoremove' to remove it.
0 upgraded, 0 newly installed, 0 to remove and 10 not upgraded.
```

Finally,it's time to install tensorflow under installing prerequisite software like pip or pip3 and so on 

In order to install tensorflow, choose one of the following commands. 

> pip install tensorflow      # Python 2.7; CPU support (no GPU support)    
> pip3 install tensorflow     # Python 3.n; CPU support (no GPU support)     
> pip install tensorflow-gpu  # Python 2.7; GPU support    
> pip3 install tensorflow-gpu # Python 3.n; GPU support    

In my case, I decided to install tensorflow-gpu, because I bought the graphic care in order to run tensorflow on graphic card

- pip install tensorflow-gpu

```bash
hyunyoung2@hyunyoung2-desktop:~$ pip install tensorflow-gpu
Collecting tensorflow-gpu
  Downloading tensorflow_gpu-1.2.0-cp27-cp27mu-manylinux1_x86_64.whl (89.2MB)
    100% |████████████████████████████████| 89.2MB 20kB/s 
    ........
Successfully built markdown html5lib
Installing collected packages: six, funcsigs, pbr, mock, numpy, markdown, html5lib, bleach, wheel, setuptools, protobuf, backports.weakref, werkzeug, tensorflow-gpu
Successfully installed backports.weakref bleach funcsigs html5lib-0.999 markdown mock numpy-1.11.0 pbr protobuf setuptools-20.7.0 six-1.10.0 tensorflow-gpu werkzeug wheel-0.29.0
You are using pip version 8.1.1, however version 9.0.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
```

- pip3 install tensorflow-gpu

```bash
hyunyoung2@hyunyoung2-desktop:~$ pip3 install tensorflow-gpu
Collecting tensorflow-gpu
  Downloading tensorflow_gpu-1.2.0-cp35-cp35m-manylinux1_x86_64.whl (89.2MB)
    100% |████████████████████████████████| 89.2MB 23kB/s 
    ........
Successfully built html5lib markdown
Installing collected packages: six, setuptools, protobuf, html5lib, wheel, bleach, numpy, backports.weakref, werkzeug, markdown, tensorflow-gpu
Successfully installed backports.weakref bleach html5lib-0.999 markdown numpy-1.11.0 protobuf setuptools-20.7.0 six-1.10.0 tensorflow-gpu werkzeug wheel-0.29.0
You are using pip version 8.1.1, however version 9.0.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
```

#  Implementation of TensorFlow

Now, if you are done until the above processing, let's check if tensorflow works well. 

> python -c "import tensorflow as tf; print (tf.\_\_version\_\_)" # for Python 2.7      
> python3 -c "import tensorflow as tf; print (tf.\_\_version\_\_)" # for Python 3.0       

as of now, tensorflow doesn't work. I think I didn't install some files related to GPU

So after prompt the above command, you got the following : 

- python -c "import tensorflow as tf; print (tf.\_\_version\_\_)" # for Python 2.7   

```bash
hyunyoung2@hyunyoung2-desktop:~$ python -c "import tensorflow as tf; print (tf.__version__)"
Traceback (most recent call last):
  File "<string>", line 1, in <module>
........
ImportError: libcusolver.so.8.0: cannot open shared object file: No such file or directory


Failed to load the native TensorFlow runtime.

See https://www.tensorflow.org/install/install_sources#common_installation_problems

for some common reasons and solutions.  Include the entire stack trace
above this error message when asking for help.
```

- python3 -c "import tensorflow as tf; print (tf.\_\_version\_\_)" # for Python 3.0

```bash
hyunyoung2@hyunyoung2-desktop:~$ python3 -c "import tensorflow as tf; print (tf.__version__)"
Traceback (most recent call last):
  File "/home/hyunyoung2/.local/lib/python3.5/site-packages/tensorflow/python/pywrap_tensorflow.py", line 41, in <module>
    from tensorflow.python.pywrap_tensorflow_internal import *
  File "/home/hyunyoung2/.local/lib/python3.5/site-packages/tensorflow/python/pywrap_tensorflow_internal.py", line 28, in <module>
    _pywrap_tensorflow_internal = swig_import_helper()
  File "/home/hyunyoung2/.local/lib/python3.5/site-packages/tensorflow/python/pywrap_tensorflow_internal.py", line 24, in swig_import_helper
    _mod = imp.load_module('_pywrap_tensorflow_internal', fp, pathname, description)
  File "/usr/lib/python3.5/imp.py", line 242, in load_module
    return load_dynamic(name, filename, file)
  File "/usr/lib/python3.5/imp.py", line 342, in load_dynamic
    return _load(spec)
ImportError: libcusolver.so.8.0: cannot open shared object file: No such file or directory

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "<string>", line 1, in <module>
..........
ImportError: libcusolver.so.8.0: cannot open shared object file: No such file or directory


Failed to load the native TensorFlow runtime.

See https://www.tensorflow.org/install/install_sources#common_installation_problems

for some common reasons and solutions.  Include the entire stack trace
above this error message when asking for help.
```

if you look into error message, you can verify what error is, where you could resolution about the avoe error(ImportError: libcusolver.so.8.0: cannot open shared object file: No such file or directory

as you saw a line which is "See https://www.tensorflow.org/install/install_sources#common_installation_problems"

If you access [the above link](https://www.tensorflow.org/install/install_sources#common_installation_problems), you got the following :

![](/img/Image/MachineLearning/Tensorflow/2017-06-27-How_To_Install_Tensorflow/ImportError.png)

As you saw, in [the above URL](https://www.tensorflow.org/install/install_sources#common_installation_problems) of officail site of tensorflow, you got Stack Overflow link which provide the resoultion that you'r running into


# GPU support of NVIDIA 

But, the resolution that tensorflow's offering didn't work in my case, 

Because I didn't install NVIDIA requirements to run TnesorFlow with GPU support. 

for GPU support,  you need :

1. you need CUDA® Toolkit 8.0 for this, you need to read [NVIDIA's documentation](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/#axzz4VZnqTJ2A)

2. you need to check if The NVIDIA drivers associated with CUDA Toolkit 8.0. 

3. you need cuDNN v5.1, for details, read [VIDIA's documentation](https://developer.nvidia.com/cudnn)  BUT you are different from version number of v5.1, depending on your system

4. you need to check your GPU card. you nee to read [VIDIA's documentation](https://developer.nvidia.com/cuda-gpus) for checking GPU with CUDA computer Capability 3.0 or higher.

5. The libcupti-dev library, in order to install this Library, 

run the following command in bash :

> sudo apt-get install libcupti-dev


## Checking prerequsite for install CUDA® Toolkit 8.0 

Before install CUDA® Toolkit 8.0, let's do pre-installation Actions. 

- Verify the system has a CUDA-capable GPU

 lspci \| grep -i nvidia

```bash 
hyunyoung2@hyunyoung2-desktop:~$ lspci | grep -i nvidia
01:00.0 VGA compatible controller: NVIDIA Corporation .........
01:00.1 Audio device: NVIDIA Corporation ........
```

you can see system requirements to use GUDA on you system, see [NVIDIA's documenataion](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/#system-requirements)

![](/img/Image/MachineLearning/Tensorflow/2017-06-27-How_To_Install_Tensorflow/System_requirement.png)

- verify the system is running a supported version of Linux

> uname -m && cat /etc/*release

```bash 
hyunyoung2@hyunyoung2-desktop:~$ uname -m && cat /etc/*release
x86_64
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=16.04
.........
```

- verify the system has gcc installed 

> gcc \-\-version

```bash 
hyunyoung2@hyunyoung2-desktop:~$ gcc --version
gcc (Ubuntu 5.4.0-6ubuntu1~16.04.4) 5.4.0 20160609
Copyright (C) 2015 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

- verify the system has the correct kernel headers and development packages installed. 

The following command will find out the version of kernel your system is running : 

> uname -r

```bash 
hyunyoung2@hyunyoung2-desktop:~$ uname -r
4.8.0-36-generic
```
the above is the version of the kernel headers and development packages that must be installed prior to installing the CUDA Drivers.

Let's install kernel headers and development package with the above command,

if you know about another system like CentOS and so on, click [NVIDIA's documentation](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/#verify-kernel-packages)

BUT in my case of Ubuntu

> sudo apt-get install linux-headers-$(uname -r)

```bash 
hyunyoung2@hyunyoung2-desktop:~$ sudo apt-get install linux-headers-$(uname -r)
Reading package lists... Done
Building dependency tree       
Reading state information... Done
linux-headers-4.8.0-36-generic is already the newest version (4.8.0-36.36~16.04.1).
linux-headers-4.8.0-36-generic set to manually installed.
The following package was automatically installed and is no longer required:
  snap-confine
Use 'sudo apt autoremove' to remove it.
0 upgraded, 0 newly installed, 0 to remove and 10 not upgraded.
```

## installing CUDA® Toolkit 8.0 

I've installed CUDA Toolkit with runfile before, if you want to know about this in detail, click [NVIDIA's doucmentation](docs.nvidia.com/cuda/cuda-installation-guide-linux/#runfile-overview)
 
you can download CUDA Toolkit on [here, cuda-download.](https://developer.nvidia.com/cuda-downloads)
 
Just choose platform you are using and download the NVIDIA CUDA Tookit that contains the CUDA driver and tools. 

The following is my choice of CUDA Toolkit

![](/img/Image/MachineLearning/Tensorflow/2017-06-27-How_To_Install_Tensorflow/download_toolkit.png)


you need  Download Verification with MD5 Checksum 

> md5sum \<file\>

```bash
hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [8:31:51] 
$ md5sum cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb 
d735c7fed8be0e72fa853f65042d5438  cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb
```


From now on, I will explaining Package Manager installation. if you want to know about another package manager installation, click [HERE](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/#package-manager-installation)

this way is much easier than [runfile](docs.nvidia.com/cuda/cuda-installation-guide-linux/#runfile-overview) 

procedure of installation : 

First, Perform [the pre-installation actions](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#pre-installation-actions) of NVIDIA's documentation

Sencond, install repositary meta-data

> sudo dpkg -i cuda-repo-\<distro\>\_\<version\>\_\<architecture\>.deb

Third, Update the Apt repository cache

>  sudo apt-get update

Forth, install CUDA

>  sudo apt-get install cuda

![](/img/Image/MachineLearning/Tensorflow/2017-06-27-How_To_Install_Tensorflow/way_to_install.png)


> sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb

```bash 
# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [8:26:08] C:100
$ sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb
Selecting previously unselected package cuda-repo-ubuntu1604-8-0-local-ga2.
(Reading database ... 197423 files and directories currently installed.)
Preparing to unpack cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb ...
Unpacking cuda-repo-ubuntu1604-8-0-local-ga2 (8.0.61-1) ...
Setting up cuda-repo-ubuntu1604-8-0-local-ga2 (8.0.61-1) ...
OK
```

> sudo apt-get update

```bash 
# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [8:27:37] C:1
$ sudo apt-get update
Get:1 file:/var/cuda-repo-8-0-local-ga2  InRelease
Ign:1 file:/var/cuda-repo-8-0-local-ga2  InRelease
Get:2 file:/var/cuda-repo-8-0-local-ga2  Release [574 B]
Get:2 file:/var/cuda-repo-8-0-local-ga2  Release [574 B]
Get:3 file:/var/cuda-repo-8-0-local-ga2  Release.gpg [819 B]                                        
Get:3 file:/var/cuda-repo-8-0-local-ga2  Release.gpg [819 B]                         
........
Fetched 1,353 kB in 10s (129 kB/s)                                                                  
Reading package lists... Done
```

> sudo apt-get install cuda

```bash
# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [8:28:08] 
$ sudo apt-get install cuda
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following package was automatically installed and is no longer required:
  snap-confine
Use 'sudo apt autoremove' to remove it.
The following additional packages will be installed:
  bbswitch-dkms ca-certificates-java cuda-8-0 cuda-command-line-tools-8-0 cuda-core-8-0
........
Processing triggers for initramfs-tools (0.122ubuntu8.8) ...
update-initramfs: Generating /boot/initrd.img-4.8.0-36-generic
Processing triggers for dbus (1.10.6-1ubuntu3.3) ...
Processing triggers for ureadahead (0.100.0-19) ...
```

after the above processing, Perform [Post-installation Actions](#Post-installation Actions)  below

**if you want to install CUDA Toolkit with runfile, you need to know how to execute text mode of linux.**

about the above thing, refer to [this askubuntu](https://askubuntu.com/questions/799184/how-can-i-install-cuda-on-ubuntu-16-04)

## [Post-installation Actions](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#post-installation-actions)

if you want to read NVIDIA's documentation about post-installation actions, click [HERE](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#post-installation-actions)

Post_installation Actions have two ways : 

 - Mandatory Action : Environment Setup.
 
 - Recommended Actions : verify the installation.
 
### Mandatory Action 

Some actions must be taken after the installation before the CUDA Toolkit and Driver can be used. 

- Environment Setup

The PATH variable needs to include > /usr/local/cuda-8.0/bin

In order to add this path to the PATH variable : 

> export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}
 
![](/img/Image/MachineLearning/Tensorflow/2017-06-27-How_To_Install_Tensorflow/zsh_export.png)


In my case, I use [oh my zsh](http://ohmyz.sh/), So I want to configure PATH on olny zsh. 

On environment set up of oh my zsh

```bash
# hyunyoung2 @ hyunyoung2-desktop in ~ [9:37:06] 
$ vim .zshrc

# add the line below in .zshrc file
# exprot cuda 
export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}


# To load the new PATH variable, log out from oh my zsh 
# hyunyoung2 @ hyunyoung2-desktop in ~ [9:39:03] C:127
$ exit
hyunyoung2@hyunyoung2-desktop:~/Downloads$ zsh

# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [9:39:58] 
$ 
```

Before configur PATH variable, you can't use **nvcc --version** like the following

```bash 
hyunyoung2@hyunyoung2-desktop:~/Downloads$ nvcc --version
The program 'nvcc' is currently not installed. You can install it by typing:
sudo apt install nvidia-cuda-toolkit
```

After configure PATH variable on .zshrc file, Now you can verify installation of CUDA 

> nvcc \-\-version 

```bash
# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [9:44:51] C:127
$ nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2016 NVIDIA Corporation
Built on Tue_Jan_10_13:22:03_CST_2017
Cuda compilation tools, release 8.0, V8.0.61
```

So whether or not tensorflow-gpu works well, 

> python -c "import tensorflow as tf; print(tf.\_\_version\_\_)"   # Ptyhon 2.7   
> python3 -c "import tensorflow as tf; print(tf.\_\_version\_\_)"  # Python 3.n    

- python -c "import tensorflow as tf; print(tf.\_\_version\_\_)"   # Ptyhon 2.7  

```bash
# hyunyoung2 @ hyunyoung2-desktop in /usr/local/cuda/bin [9:53:42] C:1
$ python -c "import tensorflow as tf; print(tf.__version__)" 
.........
ImportError: libcudnn.so.5: cannot open shared object file: No such file or directory
........
```

 - python3 -c "import tensorflow as tf; print(tf.\_\_version\_\_)" # Python 3.n  
 
```bash
# hyunyoung2 @ hyunyoung2-desktop in /usr/local/cuda/bin [9:53:58] C:1
$ python3 -c "import tensorflow as tf; print(tf.__version__)"
Traceback (most recent call last):
.........
ImportError: libcudnn.so.5: cannot open shared object file: No such file or directory

During handling of the above exception, another exception occurred:
.........
ImportError: libcudnn.so.5: cannot open shared object file: No such file or directory
.......
```

So from now on, You need to install libcudnn,  read [NVIDIA's documentation](https://developer.nvidia.com/cudnn)

When you install libcudnn, specifically look at the version of cuddn you need.

my case is the version number of 5, before download, you need to register NVIDIA Developer.

if you download and uncompress thie file, cudnn-8.0-linux-x64-v5.0-ga.tgz
 
> tar -xvzf ./cudnn-8.0-linux-x64-v5.0-ga.tgz 

```bash
# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [10:06:11] 
$ tar -xvzf ./cudnn-8.0-linux-x64-v5.0-ga.tgz 
cuda/include/cudnn.h
cuda/lib64/libcudnn.so
cuda/lib64/libcudnn.so.5
cuda/lib64/libcudnn.so.5.0.5
cuda/lib64/libcudnn_static.a
```

you need to move the whole files above into the **lib64** and **include** directoies

```bash
# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [10:08:32] C:1
$ ls
cuda  cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb  cudnn-8.0-linux-x64-v5.0-ga.tgz

# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [10:08:41] 
$ cd cuda

# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads/cuda [10:08:44] 
$ ls      
include  lib64

# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads/cuda [10:12:19] 
$ sudo cp lib64/* /usr/local/cuda/lib64/
[sudo] password for hyunyoung2: 

# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads/cuda [10:12:51] 
$ sudo cp include/* /usr/local/cuda/include/
```

Check if the files moved. 

```bash 
# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads/cuda [10:13:05] 
$ ls include 
cudnn.h

# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads/cuda [10:13:19] 
$ ls lib64                                  
libcudnn.so  libcudnn.so.5  libcudnn.so.5.0.5  libcudnn_static.a

# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads/cuda [10:13:31] 
$ ls /usr/local/cuda/lib64 
..........
libcudnn.so           libcusparse.so.8.0.61  libnppim.so.8.0.61    libnvrtc-builtins.so.8.0
libcudnn.so.5         libcusparse_static.a   libnppi.so            libnvrtc-builtins.so.8.0.61
libcudnn.so.5.0.5     libnppc.so             libnppi.so.8.0        libnvrtc.so
libcudnn_static.a     libnppc.so.8.0         libnppi.so.8.0.61     libnvrtc.so.8.0
..........

# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads/cuda [10:13:45] 
$ ls /usr/local/cuda/include 
.......
cudnn.h                    math_functions_dbl_ptx3.hpp               sm_32_intrinsics.hpp
.......
```

Now check if tensorflow-gpu works well, BUt it doesn't work

Also you need to chang **LD_LIBRARY_PATH** like this :

> export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64\    
>                         ${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

![](/img/Image/MachineLearning/Tensorflow/2017-06-27-How_To_Install_Tensorflow/zsh_export1.png)

```bash 
# hyunyoung2 @ hyunyoung2-desktop in ~ [9:37:06] 
$ vim .zshrc

# exprot cuda 
export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64\
                         ${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```

after the above configuration, tensorflow works well

```bash 
# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [10:23:37] 
$ python -c "import tensorflow as tf; print(tf.__version__)"
1.2.0

# hyunyoung2 @ hyunyoung2-desktop in ~/Downloads [10:23:39] 
$ python3 -c "import tensorflow as tf; print(tf.__version__)"
1.2.0
```

Finally, let's check if nvidia driver works well

## Verify the installation

> nvidia-smi

```bash 
# hyunyoung2 @ hyunyoung2-desktop in /proc/driver/nvidia [11:10:40] 
$ nvidia-smi      
Tue Jun 27 11:12:25 2017       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 375.66                 Driver Version: 375.66                    |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 1080    Off  | 0000:01:00.0      On |                  N/A |
|  0%   40C    P8    11W / 230W |    447MiB /  8105MiB |      1%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID  Type  Process name                               Usage      |
|=============================================================================|
|    0      1070    G   /usr/lib/xorg/Xorg                             290MiB |
|    0      1759    G   compiz                                         155MiB |
+-----------------------------------------------------------------------------+
```

In order to verify the version, type

> cat /proc/driver/nvidia/version

```bash
# hyunyoung2 @ hyunyoung2-desktop in /proc/driver/nvidia [11:13:55] C:1
$ cat /proc/driver/nvidia/version
NVRM version: NVIDIA UNIX x86_64 Kernel Module  375.66  Mon May  1 15:29:16 PDT 2017
GCC version:  gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.4) 
```

more specifically, in order to verify, run sampli source of NVIDIA. 

> cd /usr/local/cuda/bin

```bash
# hyunyoung2 @ hyunyoung2-desktop in /usr/local/cuda/bin [11:17:47] 
$ ls
bin2c        cudafe++                     cuda-memcheck        nsight        nvlink   ptxas
computeprof  cuda-gdb                     cuobjdump            nvcc          nvprof
crt          cuda-gdbserver               fatbinary            nvcc.profile  nvprune
cudafe       cuda-install-samples-8.0.sh  gpu-library-advisor  nvdisasm      nvvp
```

run cuda-install-sample-8.0.sh like this :

> cuda-install-samples-8.0.sh \<dir\>

\<dir\> means where you want install example sources of NVIDIA 

in my case, I installed the source files into **~/sample** directory

>  sudo ./cuda-install-samples-8.0.sh ~/sample/ 

```bash
# hyunyoung2 @ hyunyoung2-desktop in /usr/local/cuda/bin [11:17:48] 
$ sudo ./cuda-install-samples-8.0.sh ~/sample/ 
Copying samples to /home/hyunyoung2/sample/NVIDIA_CUDA-8.0_Samples now...
Finished copying samples.

# hyunyoung2 @ hyunyoung2-desktop in ~/sample [11:21:57] 
$ ls
NVIDIA_CUDA-8.0_Samples
```

move into NVIDIA_CUDA-8.0_Samples, complie any source file

in my case, I chose deviceQuery directory like this :

```bash

# hyunyoung2 @ hyunyoung2-desktop in ~/sample/NVIDIA_CUDA-8.0_Samples/1_Utilities/deviceQuery [11:24:45] 
$ ls
deviceQuery.cpp  Makefile  NsightEclipse.xml  readme.txt


# hyunyoung2 @ hyunyoung2-desktop in ~/sample/NVIDIA_CUDA-8.0_Samples/1_Utilities/deviceQuery [11:24:48] C:2
$ sudo make
/usr/local/cuda-8.0/bin/nvcc -ccbin g++ -I../../common/inc  -m64    -gencode arch=compute_20,code=sm_20 -gencode 
.........
cp deviceQuery ../../bin/x86_64/linux/release


# hyunyoung2 @ hyunyoung2-desktop in ~/sample/NVIDIA_CUDA-8.0_Samples/1_Utilities/deviceQuery [11:24:51] 
$ ls
deviceQuery  deviceQuery.cpp  deviceQuery.o  Makefile  NsightEclipse.xml  readme.txt

# hyunyoung2 @ hyunyoung2-desktop in ~/sample/NVIDIA_CUDA-8.0_Samples/1_Utilities/deviceQuery [11:25:34] 
$ ./deviceQuery
./deviceQuery Starting...

 CUDA Device Query (Runtime API) version (CUDART static linking)

Detected 1 CUDA Capable device(s)

Device 0: "GeForce GTX 1080"
  CUDA Driver Version / Runtime Version          8.0 / 8.0
  CUDA Capability Major/Minor version number:    6.1
  Total amount of global memory:                 8106 MBytes (8499691520 bytes)
  (20) Multiprocessors, (128) CUDA Cores/MP:     2560 CUDA Cores
  GPU Max Clock rate:                            1823 MHz (1.82 GHz)
  Memory Clock rate:                             5005 Mhz
  Memory Bus Width:                              256-bit
  L2 Cache Size:                                 2097152 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(131072), 2D=(131072, 65536), 3D=(16384, 16384, 16384)
  Maximum Layered 1D Texture Size, (num) layers  1D=(32768), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(32768, 32768), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total number of registers available per block: 65536
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  2048
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 2 copy engine(s)
  Run time limit on kernels:                     Yes
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Disabled
  Device supports Unified Addressing (UVA):      Yes
  Device PCI Domain ID / Bus ID / location ID:   0 / 1 / 0
  Compute Mode:
     < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 8.0, CUDA Runtime Version = 8.0, NumDevs = 1, Device0 = GeForce GTX 1080
Result = PASS
```


when you complete until completion of the whole processing above correctly. 

your CUDA driver works well. from now on, have a fun with TensorFlow or CUDA. 



# Reference 
 
  - [Installing TensorFlow](https://www.tensorflow.org/install/)
  
  - [Installing with native pip](https://www.tensorflow.org/install/install_linux#InstallingNativePip)
  
  - [common installation problems with Tensorflow](https://www.tensorflow.org/install/install_sources#common_installation_problems)
  
  - [In order to run TensorFlow with GPU support](https://www.tensorflow.org/install/install_linux#top_of_page)
  
  - [Installing CUDA with runfile](https://askubuntu.com/questions/799184/how-can-i-install-cuda-on-ubuntu-16-04)
  
  - [how to insatll pip](http://idroot.net/linux/install-pip-ubuntu-16-04/)
  
  - [How to insatll cudnn](http://www.pyimagesearch.com/2016/07/04/how-to-install-cuda-toolkit-and-cudnn-for-deep-learning/)
  
  - [how to change path of file for cudnn](https://askubuntu.com/questions/767269/how-can-i-install-cudnn-on-ubuntu-16-04)
  
  

