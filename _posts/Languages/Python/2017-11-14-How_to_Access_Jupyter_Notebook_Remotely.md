---
layout: post
title: How to Access Jupyter Notebook Remotely
subtitle: If you want to work romotely with jupyter notebook, You have to know this way, 
category: Python
tags: [python, jupyter notebook]
permalink: /2017/11/14/How_to_Access_Jupyter_Notebook_Remotely/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
---

# How to Access Jupyter Notebook Remotely on Webbrowser

First of all, You have to look at what kind of options you use When you run jupyter notebook as server. 

type in as follows :

> $ jupyter notebook --help 

```bash
# hyunyoung2 @ hyunyoung2-desktop in ~ [21:52:14] 
$ jupyter notebook --help
The Jupyter HTML Notebook.

.......
--no-browser
    Don't open the notebook in a browser after startup.
.......
--ip=<Unicode> (NotebookApp.ip)
    Default: 'localhost'
    The IP address the notebook server will listen on.
--port=<Int> (NotebookApp.port)
    Default: 8888
    The port the notebook server will listen on.
.......

Examples
--------

    jupyter notebook                       # start the notebook
    jupyter notebook --certfile=mycert.pem # use SSL/TLS certificate
    jupyter notebook password              # enter a password to protect the server
```

 As you could see above, the left ones is necessity for you to use jupyter notebook remotely. 
 
 
## First, the easiest way to configure only on command line to invoke jupyter notebook remotely. 

After checking output of "jupyter notebook --help", First of all you type in as follows to make password :

> $ jpyter notebook password

![](/img/Image/Languages/Python/2017-11-14-How_to_Access_Jupyter_Notebook_Remotely/Jupyter_notebook_password_and_file.png)

As you could see above, I just made password and then jupyter make some directory(.jupyter) and json file(/juypter_notebook_config.json) under /home/hyunyoung2/

The reason for you to make password is, When you access Jupyter notebook server on web browser, You have to enter the password.

That is the easiest way to access jupyter notebook server on web browser. if you don't make password. you have to use a certain token which  is very long and created randomly whenever you run jupyter notebook. 

So I recommend you to make password first than other thing. 

And then, So Let's run jupyter notebook server. 

> $ jupyter notebook --no-browser --ip="your server IP Address" --port=8888

![](/img/Image/Languages/Python/2017-11-14-How_to_Access_Jupyter_Notebook_Remotely/Jupyter_notebook_password_and_file.png)

After typing the above command, server works well. 

From now on, you can write jupyter notebook on the remote web browser. 

just type Http://"your server IP Address:port number"

Les't say your IP address is **123.456.789.123** and port number is 8888

turn on the web browser, and then type in like this : 

![](/img/Image/Languages/Python/2017-11-14-How_to_Access_Jupyter_Notebook_Remotely/Server_IP_Address_and_Port_number.png)

So you would see the window that make you enter password which you make with "jupyter notebook password" on command line.

![](/img/Image/Languages/Python/2017-11-14-How_to_Access_Jupyter_Notebook_Remotely/Use_Jupyter_Notebook_Remotely_on_webbrowser.png)

After typing password. You could work with jupyter notebook about whatever you want with python.

![](/img/Image/Languages/Python/2017-11-14-How_to_Access_Jupyter_Notebook_Remotely/Finally_Complete.png)


* --no-browser option mean I don't want to invoke jupyter notebook on local web browser. BUT If you want to run on local web browser. omit the option,"--no-browser"

## Second way to statically configure jupyter notebook to run it remotely. 

As you have seen how to run jupyter notebook remotely above. the first way is uncomfortable. That is because everytime you run jupyter notebook, You have to type like this :

> $ jupyter notebook --no-browser --ip="your server IP Address" --port=8888

This is so uncomfortable,So from now on, I will explain how to easily run jupyter notebook server statically.

















![](/img/Image/Languages/Python/2017-11-14-How_to_Access_Jupyter_Notebook_Remotely/Use_Jupyter_Notebook_Remotely_on_webbrowser.png)

After typing password. 

![](/img/Image/Languages/Python/2017-11-14-How_to_Access_Jupyter_Notebook_Remotely/Finally_Complete.png)






