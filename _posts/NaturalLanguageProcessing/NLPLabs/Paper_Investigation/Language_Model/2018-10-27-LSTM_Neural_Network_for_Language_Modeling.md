---
layout: post
title: LSTM Neural Network for Language Modeling
subtitle: Title of paper - LSTM Neural Network for Language Modeling
category: NLP papers
tags: [neural_network, nlp]
permalink: /2018/10/27/LSTM_Neural_Network_for_Language_Modeling/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

This page is brief summary of [LSTM Neural Network for Language Modeling](https://www.isca-speech.org/archive/interspeech_2012/i12_0194.html) for my study.

Language model means If you have text which is "A B C X" and already know "A B C", and then from corpus, you can expect whether What kind of word, X appears in the context.

i.e. The task to predict a word(X) with the context("A B C") is the goal of Language model(LM).


In this page, to resovle LM, they used LSTM(long short term memory) neural network. 


The existing model to LM has a problem like this :

 - Statistic model is to use frequencies of n-gram to expect the word when you know the past context. however, When you calculate the probability of n-gram based on words. you could encounter the probability not calculated ahead with corpus. So they explained alternative is [backing-off model](https://en.wikipedia.org/wiki/Katz%27s_back-off_model).
 
    - Backing-off model :
      - n-gram language model that estimates the conditional probability of a word given its history in the n-gram.
      - if there is not n-gram probability, use (n-1) gram probability.
      
 - Neural network model using vanilla RNN, FeedForward Neural Network. 
 
    - FeedFoward Neural network is to exploit a fixed context.
    
    - vanilla RNN which is free on the length of context has shorter dependancy to its history because of vanishing gradient. 
    
 So They used LSTM momory cell which is better version than vanilla RNN about momory capability. 
 
 Below is their LSTM variant from the orignal LSTM which is [F.A. Gers et al](https://ieeexplore.ieee.org/document/818041). 
 
 ![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Language_Model/2018-10-27-LSTM_Neural_Network_for_Language_Modeling/LSTM_memory_cell.png)
 
 also they used one-hot encoding and projection layer.
 
 ![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Language_Model/2018-10-27-LSTM_Neural_Network_for_Language_Modeling/projection_layer.png)
 

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
This paper said the result of using LSTM neural network on language model with corpus(English, French).The existing statistic method mentioned in this paper is backing-off model. the existing neural network method is to use vanilla RNN and Feedforward neural network. the mothods aforementioned have a problem to resolve task of language model.
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.isca-speech.org/archive/interspeech_2012/i12_0194.html">The paper: LSTM_Neural_Network_for_Language_Modeling</a>
</div>

# Reference 

- Paper 
  - [LSTM_Neural_Network_for_Language_Modeling](https://www.isca-speech.org/archive/interspeech_2012/i12_0194.html)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
 
- [wikipedia about backing-off model](https://en.wikipedia.org/wiki/Katz%27s_back-off_model)










