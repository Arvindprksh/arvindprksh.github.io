---
layout: post
title: How To Use SVMight And SVM Multiclass
subtitle: In order to classify with several or binary class, Utilize SVM light and SVM Multiclass
category: Natural Language Processing Labs
tags: [nlp, machine learning, svm]
permalink: /2017-11-16/How_To_Use_SVMight_And_SVM_Multiclass/
css : /css/ForPDFShareByHyun.css
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

# SVM light

## SVM light's input file format 

The thing below is basic format for input file of svm light you learn model about

```
<line> .=. <target> <feature>:<value> <feature>:<value> ... <feature>:<value> # <info>
<target> .=. +1 | -1 | 0 | <float> 
<feature> .=. <integer> | "qid"
<value> .=. <float>
<info> .=. <string> 
```
According to the format above, if I make simple example like this :

> 1 1:0.43 3:0.12 9284:0.2 # abcdef

- 1 means target class (total +1 \| -1 \| 0)
- a pair of 1:0.42 means 1 is feature number and 0.24 is value of feature. 

If a pair of 1:0.42 is vector, 1 is index of a vector, and 0.42 is value of the index(in here 1) of a vector.

> If want to rank your data, you can use **qid** in your training file and test file

## How To Learn SVM light and Classify 

If you want to learn the model with your input file, type in terminal as follow :

> svm_learn [options] example_file model_file 

- example_file : input file, usually training file when you learn
- model_file : model file you will learn with your input file

If you want to see what the options do. type as follows : 
 
> svm_learn -h

Finally If you want to classify test file with your model 

> svm_classify [options] example_file model_file output_file

 - example_file : input file, usually test file when you classify
 - model_file : model file you learn with training file. 
 - output_file : the result that svm light classify test file 

# SVM Multiclass

## SVM Multiclass's input file format 

the basic form is below when you use SVM multiclass. 

```
<line> .=. <target> <feature>:<value> <feature>:<value> ... <feature>:<value> # <info>
<target> .=. <integer>
<feature> .=. <integer>
<value> .=. <float>
<info> .=. <string> 
```

Let's say you have input file as follows : 

3 1:0.43 3:0.12 9284:0.2 # abcdef

 - 3 means target class, in SVM multicalss, you can make more target classes.
 - 1:0.43 means this pair is totally the same from SVM light, i.e. 1 is index of a vector, 0.43 is the value of the index

## How To Learn SVM multiclass and Classify 

When you learn training file with SVM multiclass, one thing is different. 

That is you have to use a option, -c float as follows :

 > svm_multiclass_learn -c 1.0 example_file model_file
 
Option c means trade-off between training error and margin (default 0.01)

 > svm_multiclass_classify [options] test_example_file model_file output_file

And the basic way to utilize SVM multiclass is usually the same from SVM light except for a option, -c float.  


<iframe src="//www.slideshare.net/slideshow/embed_code/key/B49DbAPye3aNwI" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/HyunYoungLee3/svm-light-and-svm-multiclass-practice-119301354" title="SVM light and SVM Multiclass Practice" target="_blank">SVM light and SVM Multiclass Practice</a> </strong> from <strong><a href="https://www.slideshare.net/HyunYoungLee3" target="_blank">hyunyoung Lee</a></strong> </div>

# Reference 

 - [SVM light](http://svmlight.joachims.org/)
 
 - [SVM multiclass](https://www.cs.cornell.edu/people/tj/svm_light/svm_multiclass.html)
 
 - [SVM light and SVM multiclass](https://www.slideshare.net/HyunYoungLee3/svm-light-and-svm-multiclass-practice-82029582)
