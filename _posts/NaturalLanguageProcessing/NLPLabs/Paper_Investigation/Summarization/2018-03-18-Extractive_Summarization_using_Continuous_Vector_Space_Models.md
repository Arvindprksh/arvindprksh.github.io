---
layout: post
title: Extractive Summarization using Continuous Vector Space Models for Text summarization
subtitle: Title of paper - Extractive Summarization using Continuous Vector Space Models
category: NLP papers - Summarization
tags: [nlp, word2vec, word_embedding, text_summarization, phrase_embedding]
permalink: /2018/03/18/Extractive_Summarization_using_Continuous_Vector_Space_Models/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

This paper,[Extractive Summarization using Continuous Vector Space Models(Mikael Kågebäck et al.(2014))](http://www.aclweb.org/anthology/W14-1504), is related to how to summarize document in the way to well extract sentence from input sentences using continuous vector representaion.

But I think this paper helps me understand the architecture base on neural newwork language modeling.  

For example, Feed-forwar neural network, Auto-Encoder, and recursive neural network. 

The architectur above is as follows: 

The basic and famous way : skip gram - target word(central of context) is used as input to predict words of window size surrounding it. 


![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Summarization/2018-03-18-Extractive_Summarization_using_Continuous_Vector_Space_Models/Skip_gram.png)

Feed-forward neural network : the direction of dataflow is one way forwards.

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Summarization/2018-03-18-Extractive_Summarization_using_Continuous_Vector_Space_Models/FFNN.png)


Auto-encoder : based on central of Coding Later, input and output is symmetrically the same. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Summarization/2018-03-18-Extractive_Summarization_using_Continuous_Vector_Space_Models/Auto_Encoder.png)

Recursive Neural Network : after parsing a sentence to binary search tree, this is evaluated on Neural Network.

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Summarization/2018-03-18-Extractive_Summarization_using_Continuous_Vector_Space_Models/RecursiveNN.png)

Recursive Auto Encoder : combination of Auto-encoder and Recursive Neural Network

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Summarization/2018-03-18-Extractive_Summarization_using_Continuous_Vector_Space_Models/Unfolding_Recursive_Auto_encoder.png)

Also, this paper explain how to make sentence vector or phrase vector. 

This ideas is so fundanmental way. But with regard to word embedding and phrase embedding, this paper simply explained to me. 

i.e. This paper is about explaining extract some sentence to similar summarization of document using word embedding and phrase embedding.


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
This paper explained how to well extract some sentences to summarize a set of multi-document using word embedding and phrase embedding.
Also basic explanation about word embedding is easy to understand to me. I mean explaining basic concept of FFNN, RvNN, and AE makes me easily understand them.  
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="http://www.aclweb.org/anthology/W14-1504">The paper: Extractive Summarization using Continuous Vector Space Models</a>
</div>

# Reference 

- Paper 
  - [Extractive Summarization using Continuous Vector Space Models](http://www.aclweb.org/anthology/W14-1504)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
 
