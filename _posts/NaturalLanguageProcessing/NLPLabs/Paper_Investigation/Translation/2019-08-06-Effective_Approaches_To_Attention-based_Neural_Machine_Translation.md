---
layout: post
title: Effective Approaches to Attention-based Neural Machine Translation
subtitle: Title of paper - Effective Approaches to Attention-based Neural Machine Translation
category: NLP papers - Translation
tags: [neural_network, translation]
permalink: /2019/08/06/Effective_Approaches_To_Attention-based_Neural_Machine_Translation/
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

This is a brief summary of paper for me to study it, [Effective Approaches to Attention-based Neural Machine Translation, Luong et al. (2016)](https://arxiv.org/abs/1508.04025) 

The reason that I am writing this post is for me to organize about studying what the Attention is in deep learning.

{% include MathJax.html %}

Machine Translation task is one of natural language understanding and has been hard to improve the performance. 

However, after using neural network on Machine Translation task. The performance of MT start outperforming the conventional phrase-based translation.

So the authors used additive attention to improve the performance of NMT. 

The reason they used additive attention is it is difficult to include all information of a source sentence into a fixed-length vector as a context vector.

In order to resolve the problem using a fixed-length vector, they used soft-alignment jointly learning alignment and translation.

From a probabilistice perspective, translation is eqaul to find a target sentence **y** that maximizes the conditional probability of **y** given a source sentence **x**.

$$ \hat{y} = \underset{y}{\mathrm{argmax}} P(y|x) $$

In the equation above,

 - x is a source sentence
 - y is a target sentence
 - P(y\|x) is the conditional probabliity of y given x. 

![Luong et al.(2016)](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2019-08-06-Effective_Approaches_To_Attention-based_Neural_Machine_Translation/Neural_Machine_Translation.png)


They suggested two attention machanisms. one is the global attention mechanism and the other is the local attention mechanism which is new attention mechanism. 

local attention mechanism considers the trade-off between soft and hard vesrion attention model proposed by Xu et al. (2015)

![Global attention model by Luong et al.(2016)](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2019-08-06-Effective_Approaches_To_Attention-based_Neural_Machine_Translation/Global_Attention_model.png) ![Local attentio model by Luong et al.(2016)](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2019-08-06-Effective_Approaches_To_Attention-based_Neural_Machine_Translation/Local_attention_model.png)

They proposed three formulas which caculate aligment scores with a **content-based** funtion. 

$$a_t(s) = align(h_t, \bar{h}\_s) = \frac{exp(score(h_t,h_t, \bar{h}\_s))}{exp(\sum{s'}score(h_t,h_t, \bar{h}\_s')}$$
$$score(h_t,h_t, \bar{h}\_s)= \begin{Bmatrix}
    h^T_s \bar{h}\_s dot \\
    h^T_s W_a\bar{h}\_s general \\
    V^T_a tanh(W_a\[h^T_s;\bar{h}\_s\]  concat\\
    \end{Bmatrix}$$

Another one is a **location-based** funtion

$$a_t = softmax(W_ah_t) location$$

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
This paper explained Attention mechanism on translation task, from English to German. They proposed two types of attention mechanism called local and global. The global attension is other variants of (Bahdanau et al. 2015), and the local attention is new attention mechanism using a subset of source states each time. 
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1508.04025">The paper: Effective Approaches to Attention-based Neural Machine Translation</a>
</div>

# Reference 

- Paper 
  - [ArXiv version: Effective Approaches to Attention-based Neural Machine Translation](https://arxiv.org/abs/1508.04025)
  - [ACL version: Effective Approaches to Attention-based Neural Machine Translation](https://aclweb.org/anthology/D15-1166)
  
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
- How to use MathJax
  - [Stackexchange1](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)
  - [Stackexchange2](https://tex.stackexchange.com/questions/5223/command-for-argmin-or-argmax)
  
- For your information
  - [Show, Attend and Tell: Neural Image Caption Generation with Visual Attention, Xu et al.(2015)](https://arxiv.org/abs/1502.03044)
  - [Attention? Attention! on Lil'Log blog](https://lilianweng.github.io/lil-log/2018/06/24/attention-attention.html)
  - [Self-Attention Mechanisms in Natural Language Prcessing on Alibabacloud](https://www.alibabacloud.com/blog/self-attention-mechanisms-in-natural-language-processing_593968)
  - [Deep Learning for NLP Best Practices on ruder blog](http://ruder.io/deep-learning-nlp-best-practices/index.html#fn2)
  - [Soft & Hard Attention on Jonathan Hui Blog](https://jhui.github.io/2017/03/15/Soft-and-hard-attention/)
  - [Attention Mechanism on Heuritech](https://blog.heuritech.com/2016/01/20/attention-mechanism/)
  - [A Brief Overview of Attention Mechanism on Medium](https://medium.com/syncedreview/a-brief-overview-of-attention-mechanism-13c578ba9129)
  - [Attention and Memory in Deep Learning and NLP on WILDML](http://www.wildml.com/2016/01/attention-and-memory-in-deep-learning-and-nlp/)
  - [Attention Mechanism in Neural Network on Hackernoon](https://hackernoon.com/attention-mechanism-in-neural-network-30aaf5e39512)
  
  
  - Kor ver
    - [Neural Turing machine no norman](https://norman3.github.io/papers/docs/neural_turing_machine.html)
  
  - Slide 
    - [Attention is all you need on whikwon slideshare](https://www.slideshare.net/WhiKwon/attention-mechanism)
    - [Attention Mechanisms with Tensorflow on KeonKim slideshare](https://www.slideshare.net/KeonKim/attention-mechanisms-with-tensorflow)



