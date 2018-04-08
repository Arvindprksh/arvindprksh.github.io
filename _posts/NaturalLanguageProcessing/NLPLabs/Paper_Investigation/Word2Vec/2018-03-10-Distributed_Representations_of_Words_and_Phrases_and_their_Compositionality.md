---
layout: post
title: Distributed Representations of Words and Phrases and their Compositionality for Word2Vec investigation
subtitle: Title of paper - Distributed Representations of Words and Phrases and their Compositionality
category: NLP papers
tags: [nlp, word2vec, word_embedding]
permalink: /2018/03/08/The_Distribuational_Hypothesis/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

I think this paper is the best to understand why the addition of two vectors works well to meaningfully infer the relation between two words.

And also it is good to understand why I have to make phrase from words. let's think of the reason.

"Boston Globe" is a newspaper, and so it is not a natural combination of the meanings of "Boston" and "Globe".

The two reasons above is a good idea when we make word embedding.

The performance to infer meanings of words depends on the loss function.

I recommend you to read this paper. 

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
This paper presents several extensions that improve both the quality of the vectors and the training speed. By subsampling of the frequent words we obtain significangant speedup and also learn more regular word representations. </br>
This paper introduces another loss function called negative sampling. An inherent limitation of word representations is their indifference to word order and their inability to represent idiomatic phrases. for example, The meanings of "Canada" and "Air" cannot be easily combined to obtain "Air Canada"</br>

If you want to download the data set, visit [here](https://code.google.com/archive/p/word2vec/)
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="http://papers.nips.cc/paper/5021-distributed-representations-of-words-and-phrases-and-their-compositionality.pdf">The paper: Distributed Representations of Words and Phrases and their Compositionality</a>
</div>

# Reference 

- Paper 
  - [Distributed Representations of Words and Phrases and their Compositionality](http://papers.nips.cc/paper/5021-distributed-representations-of-words-and-phrases-and-their-compositionality.pdf)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
- Tutorial site of word2vec 
  - [Chris McCormick's skip gram model](http://mccormickml.com/2016/04/19/word2vec-tutorial-the-skip-gram-model/)
  - [Chris McCormick's negative sampling](http://mccormickml.com/2017/01/11/word2vec-tutorial-part-2-negative-sampling/)
