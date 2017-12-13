---
layout: post
title: Python API with Flask Framework
subtitle: How to make API with flask framework
category: Python
tags: [python, flask]
permalink: /2017/12/13/Some_Example_For_APl_With_Flask_Framework/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

I am going to try to arrange something that I've studied to make OpenAPI. 

This article is refereced from some blogs, in particular, [this blog](https://prateekvjoshi.com/2016/03/08/how-to-create-a-web-server-in-python-using-flask/)

So from now on, I will orgarnize how to make api with flask framework from what I read.

This article is for me to remember and arrange what I study 

# [What is the API?](https://en.wikipedia.org/wiki/Application_programming_interface)

 API is short for "Application programming interface." It is the same to call library when you are programming. 
 
 Let's say you want to make function to copy the string from one to another place. If you are c programmer user, 
 
 You are going to call **strcpy** or **strncpy** function. That is to say, API move calling function to application to do a particular functionality.
 
 i.e. calling library is totally the same from saying "the programmer are using API" 
 
 just depend on environment where you develope program like web, operating systems, and a certain framework.
 
 If you want to know detail. go to [the wikipedia](https://en.wikipedia.org/wiki/Application_programming_interface) 
 
# OpenAPI

  Ahaed of introduction of OpenAPI with flask, I going to explain what kind of openAPI there are. 
  
  What I have known is totally three types of openAPI, SOAP(simple object access protocol) APIs, RESTful APIs, and graphQL.
  
  First is very simple basic concept for OpenAPI. That is SOAP(simple object access protocol). 
  
  That is a messaging protocol that allows programs that run on disparate operating systems(such as Windows and Linux) to communicate using Hypertext Transfer Protocol(HTTP) and its Extensible Markup Language(XML)
  
  Second is a popular one of thos kind of openAPIs, That is RESTful APIs. 
  
  RESTful API is to use basic methods of HTTP protocol, like POST, GET, PUT, DELETE and so on. 
  
  The basic methods is used to present API. 
  
  Final one is GraphQL nowadays preferred. That is based on query. 
  
# [Open API with flask](https://prateekvjoshi.com/2016/03/08/how-to-create-a-web-server-in-python-using-flask/)

  let's make simple api with flask framework. 
  
  the following is based on python3
  
  First, install flask. 
  
  > $ sudo pip3 install flask 
  
 Second, create a file with code containing flask example source code like this  
 
{% highlight python linenos %}
from flask import Flask
app = Flask(__name__)

@app.route('/')
def display():
    return "Looks like it works!"

if __name__=='__main__':
    app.run()
{% endhighlight %}
 
 After writing like above one, execute it 
 
 > python3 sampleflask.py
 
 you will get it like this :
 
 ![](/img/Image/Languages/Python/2017-11-18-How_To_Make_API_With_Flask/Sample_code_of_flask.png)
 
 and then if you access localhost:5000, you will get like the above image.
 
 If you want to change port number and star debug mode, change several lines of code above
 
{% highlight python linenos %}
from flask import Flask
app = Flask(__name__)

@app.route('/')
def display():
    return "Looks like it works!"

if __name__=='__main__':
    app.run(debug=True, port=3134)
{% endhighlight %}
 
 type like this again : 
 
 > python3 sampleflask.py
 
 on localhost:3134 you will get the result on webbrowser like this:
 
 ![](/img/Image/Languages/Python/2017-11-18-How_To_Make_API_With_Flask/Sample_flask.png)
 
## how to use URL with flask

 if you want to make flask application accessible extenally, 
 
 Type in run function like this : 
 
 > app.run(host="0.0.0.0", debug=True, port=3134)
 
 I mean you must not omit **host="0.0.0.0"**. That means you allow application to be accessible from outside.

 let'see an example 
 
{% highlight python lineos %}
from flask import Flask
app = Flask(__name__)

@app.route('/testURL')
def testURL():
    return "Your test is successful"

@app.route('/sample')
def sample():
   return "You got sample"

if __name__=='__main__':
    app.run(host="0.0.0.0", debug=True, port=3134)                                                        
{% endhighlight %}

 As you can see the annotation of @app.route('/sample'),
 
 The annotation make each fucntion perform on different path specified in URL bar. 

![](/img/Image/Languages/Python/2017-11-18-How_To_Make_API_With_Flask/sample_of_flask_final.png)

 Also keep in mide, if you don't know decorator like @app.route('/'), one thing is important in this example. 
 
 "/sample" must be the same from function name below @app.route("/sample")

# Reference 
 
 - [How To Create A web Server In python Using Flask](https://prateekvjoshi.com/2016/03/08/how-to-create-a-web-server-in-python-using-flask/)

 - [Application programming interface of wikipedia](https://en.wikipedia.org/wiki/Application_programming_interface)

 - [api creation of fullstackpython](https://www.fullstackpython.com/api-creation.html)
  
 - [Build a basic restful api in python](https://www.codementor.io/sagaragarwal94/building-a-basic-restful-api-in-python-58k02xsiq)
  
 - [What is the graphQL](https://medium.freecodecamp.org/so-whats-this-graphql-thing-i-keep-hearing-about-baf4d36c20cf)
 
 - [slideshare of lilnkedin about graphQL](https://www.slideshare.net/deview/112rest-graph-ql-relay)
