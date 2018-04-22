---
layout: post
title: Bidirectional LSTM-CRF Models for Seqeunce Tagging
subtitle: Title of paper - Bidirectional LSTM-CRF Models for Seqeunce Tagging
category: NLP papers
tags: [nlp, word2vec, tagging]
permalink: /2018/04/17/Bidirecitional_LSTM-CRF_Models_For_Sequence_Tagging/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

This paper refered to how to use BiLSTM+CRF for seqeunce tagging in NLT task. 

Normally, If you run into Sequence tagging problem, you would think of RNN. 

It is because the key point is seqeunce in the problem.

So This paper implemented LSTM network, BiLSTM network, and LSTM-CRF Network. 

First, A LSTM network : 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/tagging/2018-04-17-Bidirecitional_LSTM-CRF_Models_For_Sequence_Tagging/A_LSTM_Network.png)

If you already know and understand RNN structure, for Sequence tagging, that is it. 

Second, Bidirectional LSTM network is like this :

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/tagging/2018-04-17-Bidirecitional_LSTM-CRF_Models_For_Sequence_Tagging/Bidirectional_LSTM.png)

But, You have to consider how to use bidirectional LSTM's infomations: 

There are two types information. 

one is to use final hidden layers forward and backward

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/tagging/2018-04-17-Bidirecitional_LSTM-CRF_Models_For_Sequence_Tagging/word_representation.png)

OR

The other is to use contextual represetation. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/tagging/2018-04-17-Bidirecitional_LSTM-CRF_Models_For_Sequence_Tagging/Contextual_word_representation.png)


Finally, LSTM-CRF Network means LSTM plus CRF. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/tagging/2018-04-17-Bidirecitional_LSTM-CRF_Models_For_Sequence_Tagging/Bidirectional_LSTM_CRF.png)


CRF is normally used to tag sequence label in statistics way.

In particular, There are two ways to make use of neighbor tag information in predicting current tags. 

The first is to predict a distribution of tags for each time step and then use beam-like decoding to find optimal tag seqeunces. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/tagging/2018-04-17-Bidirecitional_LSTM-CRF_Models_For_Sequence_Tagging/CRF_network.png)

<div class="alert alert-success" role="alert"><i class="fa fa-check-square-o"></i> <b>Tip: </b>
If you use this model for sequence tagging, be careful of the following about how to extract features :<br/>
There used the spelling features and context features <br/>
 <br/>
- spelling features :  <br/>
  • whether start with a capital letter  <br/>
  • whether has all capital letters  <br/>
  • whether has all lower case letters  <br/>
  • whether has non initial capital letters  <br/>
  • whether mix with letters and digits  <br/>
  • whether has punctuation  <br/>
  • letter prefixes and suffixes (with window size of 2 to 5)  <br/>
  • whether has apostrophe end (’s)  <br/>
  • letters only, for example, I. B. M. to IBM  <br/>
  • non-letters only, for example, A. T. &T. to ..&  <br/>
  • word  pattern  feature,   with  capital  letters, lower case letters, and digits mapped to ‘A’, ‘a’ and ‘0’ respectively, for example, D56y-3 to A00a-0   <br/>
  • word pattern summarization feature,  similar to word pattern feature but with consecutive identical characters removed. For example, D56y-3 to A0a-0   <br/>
  <br/>
- context features : uni-gram, bi-gram or tri-gram  <br/>
</div>


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
In this paper, they proposed a variety of Long Short-Term Memory based models for sequence tagging. These models include LSTM networks, bidirectional LSTM(BI-LSTM) networks, LSTM with a Conditional Random Field(CRF) layer(LSTM-CRF) and bidirectional LSTM with a CRF layer (BI-LSTM-CRM) model.
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1508.01991v1">The paper: Bidirectional LSTM-CRF Models for Sequence Tagging</a>
</div>

# Reference 

- Paper 
  - [Efficient Estimation of Word Representations in Vector Space](https://arxiv.org/abs/1508.01991v1)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
- Example with tensorflow
  - [Guillaume Genthial blog's Sequence Tagging with Tensorflow ](https://guillaumegenthial.github.io/sequence-tagging-with-tensorflow.html)
  - [WILDML's RNN](http://www.wildml.com/2016/08/rnns-in-tensorflow-a-practical-guide-and-undocumented-features/)
  - [aymericdamien's RNN](https://github.com/aymericdamien/TensorFlow-Examples/blob/master/examples/3_NeuralNetworks/bidirectional_rnn.py)
   
  
