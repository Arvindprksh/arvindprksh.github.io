---
layout: post
title: Neural Machine Translation By Jointly Learning to align and translate
subtitle: Title of paper - Neural Machine Translation By Jointly Learning to align and translate
category: NLP papers - Translation
tags: [neural network, translation]
permalink: /2019/01/01/Neural_Machine_Translation_by_Jointly_Learning_to_Align_And_Translate/
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

This is a brief summary of paper, [Neural Machine Translation By jointly Learning to align and translate, Bahdanau et al. ICLR 2015](https://arxiv.org/abs/1409.0473) I read and studied. 

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

So the equation above means maximizing the conditional probability of a target sentence **y** given a source sentence **x**. it is parameterized in neural network model. 

From now on, Let's see notion of the model, called RNN Encoder-Decoder, that they was saying for NMT task.

the model of theirs is learned to align and translate simultaneously on **Encoder-Decoder Framework**

In the Encoder-Decoder Framework, An encoder reads the input sentence, a sequence of vectors, \\(x = (x_{1},...,x_{T_{x}})\\).

The common RNN's structure to use it:

$$ h_{t} = f(x_{t}, h_{t-1})  $$

and 

$$ c = q(h_{1},....,h_{T_{x}}) $$

Where \\(h_{t} \in \mathbb{R}^n\\) is a hidden state at time t, and c is a vector generated from the sequence of the hidden states. 

\\(f\\) and \\(q\\) are some non-linear functions. in their paper, \\(f\\) is GRU and \\(q\\) is feedforward neural network to pay attend to hiddens of Encoder.

The decoder to sequentially predict target words defines a probability over the translation **y** by decomposing the joint probability into the ordered conditional : 

$$    P(y_{1},....,y_{n}) = \prod_{t=1}^nP(y_{t} | {y_{1},...,y_{t-1}}, c)   $$

With an RNN each conditional probability is modeled as 

$$  p(y_{t} | {y_{1},...,y_{t-1}}, c) = g(y_{i-1}, s_{t}, c) $$

where \\(g\\) is a non-linear, potentially multi-layered, function that outputs the probability of \\(y_{t}\\), and \\(s_{t}\\) is the hidden state of the RNN.

with the notion above for translation using RNN, the architecture of decoder they say is :

![Bahdanau_et_al_(2015)](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2019-01-01-Neural_Machine_Translation_by_Jointly_Learning_to_Align_And_Translate/Bahdanau_et_al_(2015).png)

The image above is a decoder of their NMT, in the model, they define each conditional probability as :

$$  p(y_{i} | {y_{1},...,y_{i-1}},x) = g(y_{i-1},s_{i},c_{i})   $$

where \\(s_{i}\\) is an RNN hidden state for time \\(i\\) computed by 

$$ s_{i} = f(s_{i-1}, y_{i-1}, c_{i}) $$

Here, the probability is conditioned on a distinct context vector \\(c_{i}\\) for each target word \\(y_{i}\\).

The context vector \\(c_{i}\\) depends on a sequece of hidden states \\((h_{1},...,h_{T_{x}})\\) that an encoder maps an input sentence to.

Each hidden state \\(h_{i}\\) contains information about the whole input sequence with a strong focus on the parts surrounding the \\(i\\)-th word of the input sequence.

Let's see how for them to compute context vector. 

The context vector \\(c_{i}\\) is, then, computed as a weighted sum of these hidden states \\(h_{i}\\) as : 

$$  c_{i} = \sum_{j=1}^{T_{x}} \alpha_{ij}h_{j}   $$

The weight \\(a_{ij}\\) of each hidden state \\(h_{j}\\), which is call attention, is computed by

$$   
 \alpha_{ij} = \frac{exp(e_{ij})}{\sum_{k=1}^{T_{x}} exp(e_{ik})}
$$

where 

$$  e_{ij} = \alpha(s_{i-1}, h_{j})  $$

the \\(e_{ij}\\) is an alignment model which scores how well the inputs around position \\(j\\) and the output at position \\(i\\) match. 

The score is based on the RNN(decoder) hidden state \\(s_{i-1}\\) before emitting \\(y_{i}\\) and the \\(j\\)-th hidden state \\(h_{j}\\) of input sentence.

They parameterized the alignment model \\(\alpha\\) as a feedforward neural network which is jointly trained with all the other components of the proposed system.

Specifically, the alignment model is modeled as 

$$
\alpha(s_{i-1}, h_{j}) = V_{\alpha}^\top tanh(W_{\alpha}s_{i-1} + U_{\alpha}h_{j})
$$

where \\(W_{\alpha} \in \mathbb{R}^{nxn}, U_{\alpha} \in \mathbb{R}^{nx2n}\\) and \\(V_{\alpha} \in \mathbb{R}^n\\) are the weight metrices. 

They regard the approach of taking a weighted sum of all the hidden states as computing an **expected hiddend state**, where the expectation is over possible alignments. 

Let \\(\alpha_{ij}\\) be a proability that the target word \\(y_{i}\\) is aligned to , or translated from.

Then the \\(i\\)-th context vector \\(c_{i}\\) is the expected hidden state over all hidden states with probabilities \\(\alpha_{ij}\\).

The probability \\(\alpha_{ij}\\), or its associated energy \\(e_{ij}\\) reflects the importance of the hidden state \\( h_{j}\\) with respect to the previous hidden state \\(s_{i-1}\\) in deciding the next state \\(s_{i}\\) and generating \\(y_{i}\\).

Intuitively, this implement an mechanism of attention in the decoder. The decoder decides parts of the source sentence to pay attention to.

by doing the mechanism on the decoder, they relieve the burden for the encoder to summarize all information of a source sentence into a fixed-length vector.

With this approach, the information can be spread throughout the sequence of hidden states, which can be selectively retrieved by the decoder accordingly.

<div id="tutorial-section">

  <div id="tutorial-title">Youtube of Deeplearning Ai</div>

  <ul class="nav nav-pills">
    <li class="active"><a data-toggle="tab" href="#refrigerator">Attention Model Intution</a></li>
    <li><a data-toggle="tab" href="#refrigerator_concept">Attention Model</a></li>
  </ul>

  <div class="tab-content">
    <div id="refrigerator" class="tab-pane fade in active">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/SysgYptB198" frameborder="0" allowfullscreen></iframe>
    </div>
    <div id="refrigerator_concept" class="tab-pane fade">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/quoGRI-1l0A" frameborder="0" allowfullscreen></iframe> </div>
  </div>
 
</div>

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
This paper explained how to pay attention on NMT(neural machine translation) task. They said the previous encoder-decoder architecture has a bottleneck in fixed-length context vector. So They extended the existing encoder-decoder architecture by using (soft-)alignment between source and target sentence with a context vector.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1409.0473">The paper: Neural Machine Translation By Jointly Learning to align and translate</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: Neural Machine Translation By Jointly Learning to align and translate. Bahdanau et al. arXiv 2015](https://arxiv.org/abs/1409.0473)
  
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
- How to use MathJax
  - [Stackexchange1](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)
  - [Stackexchange2](https://tex.stackexchange.com/questions/5223/command-for-argmin-or-argmax)
  
- For your information
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
































