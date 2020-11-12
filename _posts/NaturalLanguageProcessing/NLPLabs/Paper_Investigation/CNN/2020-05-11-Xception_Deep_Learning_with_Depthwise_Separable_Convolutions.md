---
layout: post
title: Xception Deep Learning with Depthwise Separable Convolutions
subtitle: Title of paper - Xceptio Deep Learning with Depthwise Separable Convolutions
category: NLP papers - CNN
tags: [cnn]
permalink: /2020/05/11/Xception_Deep_Learning_with_Depthwise_Separable_Convolutions/
css : /css/ForYouTubeByHyun.css
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
  
---

This is a brief summary of paper for me to study and arrange for [Xception: Deep Learning with Depthwise Separable Convolutions, Cholletl., CVPR 2017](https://ieeexplore.ieee.org/document/8099678) I read and studied. 
{% include MathJax.html %}

This paper is a research ralted to answer to the quextion which is how the convolutional network works.

They proposed depth-wise separable convolution neural networks. 

They follow the following hypothesis: that the mapping of cross-channels correlation and spatial correlations in the featur maps of convolutional neural networks can be entirely decoupled. 

It underlies the inception architecture, So they named their method Xception, which stands for "Extreme Inception".

The following figure is their architectur of Xception:

![Francois Cholletl., CVPR 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/CNN/2020-05-11-Xception_Deep_Learning_with_Depthwise_Separable_Convolutions/Xception.PNG)

As you can see image above,  they decoupled mapping of cross-channel correlation and spatial correlation.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They present an interpretation of Inception modules in convolutional neural networks as being an intermediate step in-between regular convolution and the depthwise separable convolution operation (a depthwise convolution followed by a pointwise convolution). In this light, a depthwise separable convolution can be understood as an Inception module with a maximally large number of towers. This observation leads them to propose a novel deep convolutional neural network architecture inspired by Inception, where Inception modules have been replaced with depthwise separable convolutions. They show that this architecture, dubbed Xception. Since the Xception architecture has the same number of parameters as Inception V3, the performance gains are not due to increased capacity but rather to a more efficient use of model parameters.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://ieeexplore.ieee.org/document/8099678">The paper: Xception: Deep Learning with Depthwise Separable Convolutions, Cholletl., CVPR 2017</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: Xception: Deep Learning with Depthwise Separable Convolutions, Chollet., arXiv 2017](https://arxiv.org/abs/1610.02357v3)
  - [CVPR Version: Xception: Deep Learning with Depthwise Separable Convolutions, Cholletl., CVPR 2017](https://ieeexplore.ieee.org/document/8099678)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    




























