---
layout: post
title: Pointing the Unknown Words
subtitle: Title of paper - Pointing the Unknown Words
category: NLP papers - Summarization
tags: [neural network, extractive summarization]
permalink: /2020/08/28/Pointing_the_Unknown_Words/
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

This is a brief summary of paper for me to study and organize it, [Pointing the Unknown Words. Gulcehre et al. ACL 2016](https://www.aclweb.org/anthology/P16-1014/) I read and studied. 
{% include MathJax.html %}




Words are the basic input/output units in most of the NLP systems, and thus the ability to cover a large number of words is a key to building a robust NLP system. 

However, considering that (i) the number of all words in a language including named entities is very large and that (ii) language itself is an evolving system (people create new words), this can be a challenging problem.

First of all, there is usually neural network-based NLP system using softmax output layer where each of the output dimension corresponds to a word in a predefined word-shortlist. 

But it is not efficient, because computing high dimensional softmax is computationally expensive. 

So in practice the shortlist is limited to have only topK most frequent words in the training corpus. All other words are then replaced by a special word, called the unknown word (UNK).

The shortlist approach has two fundamental roblems. 

The first problem, which is known as the rare word problem, is that some of the words in the shortlist occur less frequently in the training set and thus are difficult to learn a good representation, resulting in poor performance. 

Second, it is obvious that we can lose some important information by mapping different words to a single dummy token UNK. Even if we have a very large shortlist including all unique words in the training set, it does not necessarily improve the test performance, because there still exists a chance to see an unknown word at test time. This is known as the unknown word problem. 

In addition, increasing the shortlist size mostly leads to increasing rare words due to Zipf’s Law.

As per this problem, this paper proposed the way to point the unknown word from source text to target text. 

So they used pointer softmax which consists of two types, location softmax and shortlist softmax as follows. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Summarization/2020-08-28-Pointing_the_Unknown_Words/pointer_softmax.PNG)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
The problem of rare and unknown words is an important issue that can potentially effect the performance of many NLP systems, including traditional count-based and deep learning models. They propose a novel way to deal with the rare and unseen words for the neural network models using attention. Their model uses two softmax layers in order to predict the next word in conditional language models: one predicts the location of a word in the source sentence, and the other predicts a word in the shortlist vocabulary. At each timestep, the decision of which softmax layer to use is adaptively made by an MLP which is conditioned on the context. They motivate this work from a psychological evidence that humans naturally have a tendency to point towards objects in the context or the environment when the name of an object is not known. Using their proposed model, they observe improvements on two tasks, neural machine translation on the Europarl English to French parallel corpora and text summarization on the Gigaword dataset.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P16-1014/">The paper: Pointing the Unknown Words. Gulcehre et al. ACL 2016</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Pointing the Unknown Words.  Gulcehre et al. Arxiv 2016](https://arxiv.org/abs/1603.08148)
  - [ACL 2016 version: Pointing the Unknown Words. Gulcehre et al. ACL 2016](https://www.aclweb.org/anthology/P16-1014/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
- For information 
  - [Towards Automatic Text Summarization: Extractive Methods on medium](https://medium.com/sciforce/towards-automatic-text-summarization-extractive-methods-e8439cd54715)
  - [Automatic Text Summarization with Machine Learning — An overview on medium](https://medium.com/luisfredgs/automatic-text-summarization-with-machine-learning-an-overview-68ded5717a25)
  - [Deep Learning Models for Automatic Summarization on toward data science](https://towardsdatascience.com/deep-learning-models-for-automatic-summarization-4c2b89f2a9ea)
    


