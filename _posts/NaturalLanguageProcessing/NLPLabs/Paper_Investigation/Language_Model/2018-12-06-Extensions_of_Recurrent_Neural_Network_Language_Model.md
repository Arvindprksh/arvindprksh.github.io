---
layout: post
title: Extensions of recurrent neural network Language model
subtitle: Title of paper - Extensions of recurrent neural network language model
category: NLP papers
tags: [neural_network, language_model]
permalink: /2018/12/06-Extensions_of_Recurrent_Neural_Network_Language_Model
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

<!-- \\( X_{i}=\sum_{k}X_{ik} \\) -->

{% include MathJax.html %}

This article is just brief summary of the paper, [Extensions of Recurrent Neural Network Language model](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=5947611).

This is for me to studying artificial neural network with NLP field. 

This paper is extension edition of Their original paper, [Recurrent neural Network based language model](https://www.fit.vutbr.cz/research/groups/speech/publi/2010/mikolov_interspeech2010_IS100722.pdf).

In this paper, they argued their extension led to more than the 15 times speed up with BPTT(backpropagation through time), factorization of output layer, and compression layer. 

They said their model can be smaller, faster and mor accurate than the basic one, their original RNN-LM because of the threee factors above.

They also said recurrent neural network can perform **clustering of similar histories**. i.e. This allows for instance efficient representation of patterns with variable length. 

Their simple recurrent neural network is like :

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Language_Model/2018-12-06-Extensions_of_Recurrent_Neural_Network_Language_Model/simple_reccurent_neural_network.png)

As you can check their original model, recurrent neural network, they here also used sigmoid as activation function in hidden layer and softmax function in output layer as probability distribution function.

They said the BPTT(Backporopagation through time) is extension of the backpropagation algorithm for recurrent networks and with truncated BPTT, the error is propagated through recurrent connections back in time for a pecific number of time steps.

So they were saying the network learned to remember information for several time steps in the hidden layer when it is learned by the BPTT.

The following figure is the result of BPTT depeding on the number of BPTT steps.

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Language_Model/2018-12-06-Extensions_of_Recurrent_Neural_Network_Language_Model/BPTT_effect.png)

They were also saying the compuational bottlneck is because of the size of vocabularies.

Let's see the time complexity they said in their paper. 

The time complexity of on training step is propotional  to 

- \\( O = (1+H)*H*t + H*V  and in this equation, usually H << V,so the computaional bottleneck exists between hiiden and output layer. \\)

   - H : the size of the hidden layer
   - V : the size of the vocabulary
   - t : the amount of steps they backpropagate the error back in time. 

As you can see the above equation. because normally computational bottleneck happened between hidden and output layer.

So they introduced factorization of the output layer and compression layer between hidden and output layer.

Factorization of output layer based on the assumption that all words belong to classes.

They mapped all word to exactly one class. Thus they could estimate the probability distribution over the classes using RNN and then calculate the probability of a particular words form the desired class like this:

- \\( P(w_{i} \| history) = P(C_{i} \| S_{t})P(W_{i} \| C_{i}, S_{t}) \\)

  - \\( S_{t} \\) : history in context of neural networks that is hidden layer.

The compression layer not only reduces computational complexity, but also reduces the total parameters, which results in the more compact models.

And if the compression layer is between input and hidden layer. it is refered to as a **projection layer**.




<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
This paper introduce literally extensions of recurrent neural network language model, saying BPTT(backpropagation through time), factorizaion of the output layer and compression layer for computational complexity.
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://ieeexplore.ieee.org/abstract/document/5947611">The paper: Extensions of recurrent neural network language model</a>
</div>

# Reference 

- Paper 
  - [Extensions of Recurrent Neural Network Language model](https://ieeexplore.ieee.org/abstract/document/5947611)
 
  - [A Neural Probabilistic Language Model](http://www.jmlr.org/papers/volume3/bengio03a/bengio03a.pdf)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
 
- For your information
  [Distributed representation on O'REILLY](https://mail.google.com/mail/u/0/#inbox/FMfcgxmZTlnNZMxzKqvPTzSHRMVSJZDs)
  [Hierarchical Softmax as output activation function in Neural Network on becominghuman.ai](https://becominghuman.ai/hierarchical-softmax-as-output-activation-function-in-neural-network-1d19089c4f49)





























