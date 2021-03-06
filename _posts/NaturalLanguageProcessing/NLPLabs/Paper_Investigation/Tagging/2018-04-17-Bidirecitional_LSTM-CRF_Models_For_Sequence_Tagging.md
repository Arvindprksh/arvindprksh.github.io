---
layout: post
title: Bidirectional LSTM-CRF Models for Seqeunce Tagging
subtitle: Title of paper - Bidirectional LSTM-CRF Models for Seqeunce Tagging
category: NLP papers - Tagging
tags: [nlp, tagging]
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

This paper,[Bidirectional LSTM-CRF Models for Sequence Tagging (Huang et al., arXiv 2015)](https://arxiv.org/abs/1508.01991v1), refered to how to use BiLSTM+CRF for seqeunce tagging in NLT task. 

Normally, If you run into Sequence tagging problem, you would think of RNN. 

It is because the key point is seqeunce in the problem.

So This paper implemented LSTM network, BiLSTM network, LSTM-CRF Network, BiLSTM-CRF network. 

First, A LSTM network deals with information from left to right : 

![Huang et al., arXiv 2015](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2018-04-17-Bidirecitional_LSTM-CRF_Models_For_Sequence_Tagging/A_LSTM_Network.png)

as you can already know and understand RNN structure, the utilize the infromation of previous information and current input. 

So LSTM utilize the past information at the time, But BiLSTM is different as follows:

Second, Bidirectional LSTM network is like this :

![Huang et al., arXiv 2015](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2018-04-17-Bidirecitional_LSTM-CRF_Models_For_Sequence_Tagging/Bidirectional_LSTM.png)

BiLSTM have two type of LSTM, one is forward LSTM and the other is backward LSTM. 

operation of the two LSTM is the same, the direction of information flow is different. 

Let's see how to take advantage of BiLSTM to extract information. 

there two ways to extract information. one is only final state, the other is sequence output at the time. 


firstly, use final state(output) that it summarize the infromation of forward and backward respectively :

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2018-04-17-Bidirecitional_LSTM-CRF_Models_For_Sequence_Tagging/word_representation.png)

OR

Seconde, methods to use contextual represetation of forward and backward respectively. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2018-04-17-Bidirecitional_LSTM-CRF_Models_For_Sequence_Tagging/Contextual_word_representation.png)


as you could know, for sequence labeling problem, we need to use contextual represenation. 

## conditional random field

Conditional random field(CRF) is useful graphical model on probability. 

It consider sentence level tag sequence information. 

![Huang et al., arXiv 2015](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2018-04-17-Bidirecitional_LSTM-CRF_Models_For_Sequence_Tagging/CRF_network.png)

Let's see the combination of LSTM and CRF 

First, LSTM with a CRF layer 

![Huang et al., arXiv 2015](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2018-04-17-Bidirecitional_LSTM-CRF_Models_For_Sequence_Tagging/LSTM_CRF.JPG)

Second, Bi-direcational LSTM with A CRF Layer

![Huang et al., arXiv 2015](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2018-04-17-Bidirecitional_LSTM-CRF_Models_For_Sequence_Tagging/Bidirectional_LSTM_CRF.JPG)

As you can know, in this paper, LSTM is variant like Peephole LSTM. 

They use cell state as input for input, output, forget gate.

In particular, the weight matrix from cell to gate vectors are diagonal.

additionaly, they used BIO2 annotation standard for Chunking and NER tasks.

also they use the connection trick of features like this: 

![Huang et al., arXiv 2015](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2018-04-17-Bidirecitional_LSTM-CRF_Models_For_Sequence_Tagging/feature_connection.JPG)


They estimated the robustness of models with respect to engineered features(spelling and context features).

So they trained their models with word features only(spelling and context features removed).

they argued that 

- CRF model heavily rely on engineered features to obtain good performance. 

- on the other hand, LSTM, BiLSTM, and BiLSTM-CRF models are more robust and they are less affected by the  removal of engineering features.



<div class="alert alert-success" role="alert"><i class="fa fa-check-square-o"></i> <b>Tip: </b>
If you use this model for sequence tagging, be careful of the following about how to extract features :<br/>
There used the spelling features and context features <br/>
 <br/>
- spelling features :  <br/>
  ??? whether start with a capital letter  <br/>
  ??? whether has all capital letters  <br/>
  ??? whether has all lower case letters  <br/>
  ??? whether has non initial capital letters  <br/>
  ??? whether mix with letters and digits  <br/>
  ??? whether has punctuation  <br/>
  ??? letter prefixes and suffixes (with window size of 2 to 5)  <br/>
  ??? whether has apostrophe end (???s)  <br/>
  ??? letters only, for example, I. B. M. to IBM  <br/>
  ??? non-letters only, for example, A. T. &T. to ..&  <br/>
  ??? word  pattern  feature,   with  capital  letters, lower case letters, and digits mapped to ???A???, ???a??? and ???0??? respectively, for example, D56y-3 to A00a-0   <br/>
  ??? word pattern summarization feature,  similar to word pattern feature but with consecutive identical characters removed. For example, D56y-3 to A0a-0   <br/>
  <br/>
- context features : uni-gram, bi-gram or tri-gram  <br/>
</div>


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
In this paper, they proposed a variety of Long Short-Term Memory based models for sequence tagging. These models include LSTM networks, bidirectional LSTM(BI-LSTM) networks, LSTM with a Conditional Random Field(CRF) layer(LSTM-CRF) and bidirectional LSTM with a CRF layer (BI-LSTM-CRM) model.
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1508.01991v1">The paper: Bidirectional LSTM-CRF Models for Sequence Tagging (Huang et al., arXiv 2015)</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: Bidirectional LSTM-CRF Models for Sequence Tagging (Huang et al., arXiv 2015)](https://arxiv.org/abs/1508.01991v1)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
- blogs related to information of Linear-chain CRF
  - [Guillaume Genthial blog's Sequence Tagging with Tensorflow ](https://guillaumegenthial.github.io/sequence-tagging-with-tensorflow.html)
  - [WILDML's RNN](http://www.wildml.com/2016/08/rnns-in-tensorflow-a-practical-guide-and-undocumented-features/)
  - [aymericdamien's RNN](https://github.com/aymericdamien/TensorFlow-Examples/blob/master/examples/3_NeuralNetworks/bidirectional_rnn.py)
  - [Implementing a linear-chain Conditional Random Field (CRF) in PyTorch on towardsdatascience](https://towardsdatascience.com/implementing-a-linear-chain-conditional-random-field-crf-in-pytorch-16b0b9c4b4ea) 
  - [HMM, MEMM, and CRF: A Comparative Analysis of Statistical Modeling Methods on llibabacloud](https://www.alibabacloud.com/blog/hmm-memm-and-crf-a-comparative-analysis-of-statistical-modeling-methods_592049?spm=a2c41.11544581.0.0)
  - [Maximum Entropy Markov Models and Logistic Regression on David S. Batista blog](http://www.davidsbatista.net/blog/2017/11/12/Maximum_Entropy_Markov_Model/)
  - [Introduction to Conditional Random Fields on Edwin Chen blog](https://blog.echen.me/2012/01/03/introduction-to-conditional-random-fields/)
  - [Conditional Random Field Tutorial in PyTorch on Towards Data Science](https://towardsdatascience.com/conditional-random-field-tutorial-in-pytorch-ca0d04499463)
