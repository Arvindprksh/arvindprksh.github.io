---
layout: post
title: Recurrent neural network based language model
subtitle: Title of paper - Recurrent neural network based language model
category: NLP papers - Language Model
tags: [neural network, language model]
permalink: /2018/12/06/Recurrent_Neural_Network_based_language_model/
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

This article is just brief summary of the paper, [Recurrent neural network based language model, Mikolov et al.(2010)](http://www.fit.vutbr.cz/research/groups/speech/publi/2010/mikolov_interspeech2010_IS100722.pdf).

This is for me to studying artificial neural network with NLP field. 

The task that the paper applied is Language model, just it predict the conditional probability of the next word given the previous words. 

let's say the length of a sequence of words is 3, if we want to predict fourth word. the pobability of next word is conditional probability distribution is like :

- \\(  P(w_{3} \| w_{1}, w_{2}) = P(w_{1})\*P(w_{2}\|w_{1})\*P(w_{3}\|w_{1}, w_{2})  \\)

Their model estimate the conditional probability of the next word given the previous words. 

as you know, their model is useful at sequential data for Recurrent neural network. 

They explained with the reason that Bengio et al(2003) model has the fixed context length their model is efficient to deal with sequential data.

They said that recurrent neural network is a model which could encode temporal information implicitly for contexts with arbitrary langths.

Their model is like :  

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Language_Model/2018-12-06-Recurrent_Neural_Network_based_language_model/Recurrent_neural_network_based_language_model.png)

As you can check, By using recurrent connection of prior context, information can cycle inside these networks for arbitrarily long time. 

I realized the on-line learning they called dynamic model. 

The following is the summary about dynamic model they called in their paper. 

- dynamic model : They said the network should continue training even during testing phase. They refered to such a model as dynamic.

For their dynamic model. they used the fixed learning rate(0.1) for retrainig on testing phase. while in trainig phase all data is provided to the model several times in epochs. their dynamic model gets updated just once as test data is processed on testing phase.

So their dynamic model can automatically adapt to new domains like unkonwn data.

In this case they used the standard backpropagation algorithm.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They introduce a new recurrent neural network based language model(RNN LM) with speech recognition is presented. i.e. they used Recurrent neural network with sigmoid and softmax for Language model.
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="http://www.fit.vutbr.cz/research/pubs/index.php?id=9362">The paper: Recurrent Neural Network based Language model</a>
</div>

# Reference 

- Paper 
  - [Recurrent neural network based language model](http://www.fit.vutbr.cz/research/pubs/index.php?id=9362)
 
  - [A Neural Probabilistic Language Model](http://www.jmlr.org/papers/volume3/bengio03a/bengio03a.pdf)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
 
- For your information
  - [Distributed representation on O'REILLY](https://www.oreilly.com/ideas/how-neural-networks-learn-distributed-representations)
  - [Hierarchical Softmax as output activation function in Neural Network on becominghuman.ai](https://becominghuman.ai/hierarchical-softmax-as-output-activation-function-in-neural-network-1d19089c4f49)
  - [Language model on Wikipedia](https://en.wikipedia.org/wiki/Language_model)
  - [Language model A Survey of the State-of-the-Art Techonology on medium](https://medium.com/syncedreview/language-model-a-survey-of-the-state-of-the-art-technology-64d1a2e5a466)
  - [Stackexchange on log-linear vs log-bilear](https://stats.stackexchange.com/questions/157136/log-linear-vs-log-bilinear)
  - [Neural Language models and word embedding as reference](https://piotrmirowski.files.wordpress.com/2014/06/piotrmirowski_2014_wordembeddings.pdf)
  - [Language Modelling and Text generation using LSTMs-Deep Learning for NLP](https://medium.com/@shivambansal36/language-modelling-text-generation-using-lstms-deep-learning-for-nlp-ed36b224b275)
  - [Build your LSTM language model with Tensorflow on medium](https://medium.com/@MilkKnight/build-your-lstm-language-model-with-tensorflow-3416142c9919)
  - [Language modeling with Deep Learning](https://hub.packtpub.com/language-modeling-with-deep-learning/)
  - [What's an LSTM-LM formulation on Stackexchange](https://datascience.stackexchange.com/questions/13188/whats-an-lstm-lm-formulation)
  - [A Recurrent Latent Variable Model for Sequential Data, Junyoung chung et al.(2016)](https://arxiv.org/pdf/1506.02216.pdf)
























