---
layout: post
title: An efficient framework for learning sentence representations
subtitle: Title of paper - An efficient framework for learning sentence representations
category: NLP papers - Sentence Embedding
tags: [neural network, sentence embedding]
permalink: /2019/12/19/An_efficient_framework_for_learning_sentence_representations/
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

This is a brief summary of paper for me to study and organize it, [An efficient framework for learning sentence representations. Lajanugen Logeswaran and Honglak Lee. ICLR 2018](https://openreview.net/forum?id=rJvJXZb0W) I read and studied. 
{% include MathJax.html %}

They propose simple method to represent a sentence into a fixed-length vectors they call **[Quick Thought Vectors](https://github.com/lajanugen/S2V)**

The method is similar to skip-gram method of word2vec. i.e. they extend the skip-gram to sentence-level. 

Unlike skip-thought vector, the differences is they use only an encoder to represent a sentence into a fixed-length vector using RNN types (here GRU). 

They turn the part of decoder to generate adjacent sentences into discriminative approximation which is whether the context sentence is adjacent to input sentence.

The method is as follows:

![Lajanugen Logeswaran and Honglak Lee. ICLR 2018](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2019-12-19-An_efficient_framework_for_learning_sentence_representations/quick_thought_vectors1.PNG)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
In this work they propose a simple and efficient framework for learning sentence representations from unlabelled data. Drawing inspiration from the distributional hypothesis and recent work on learning sentence representations, they reformulate the problem of predicting the context in which a sentence appears as a classification problem. Given a sentence and its context, a classifier distinguishes context sentences from other contrastive sentences based on their vector representations. This allows them to efficiently learn different types of encoding functions. Their method is calle qucik-thougt vectors.
speedup in training time.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://openreview.net/forum?id=rJvJXZb0W">The paper: An efficient framework for learning sentence representations. Lajanugen Logeswaran and Honglak Lee. ICLR 2018</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: An efficient framework for learning sentence representations. Lajanugen Logeswaran and Honglak Lee. Arxiv 2018](https://arxiv.org/abs/1803.02893)
  - [ICLR 2018 version: An efficient framework for learning sentence representations. Lajanugen Logeswaran and Honglak Lee. ICLR 2018](https://openreview.net/forum?id=rJvJXZb0W)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [Github of An efficient framework for learning sentence representations. Lajanugen Logeswaran and Honglak Lee. ICLR 2018](https://github.com/lajanugen/S2V)
  - [word2vec Explained: deriving Mikolov et al.'s negative-sampling word-embedding method on Goldberg and Levy arXiv 2014](https://arxiv.org/abs/1402.3722)
  - [Word2Vec Tutorial Part 2 - Negative Sampling on Chris McCormick blog](http://mccormickml.com/2017/01/11/word2vec-tutorial-part-2-negative-sampling/)
  - [Optimize Computational Efficiency of Skip-Gram with Negative Sampling on aegis4048 blog](https://aegis4048.github.io/optimize_computational_efficiency_of_skip-gram_with_negative_sampling#fig1)
  - [How does sub-sampling of frequent words work in the context of Word2Vec? on quora](https://www.quora.com/How-does-sub-sampling-of-frequent-words-work-in-the-context-of-Word2Vec)
  - [word2vec: negative sampling (in layman term)? on stackoverflow](https://stackoverflow.com/questions/27860652/word2vec-negative-sampling-in-layman-term)
  - [Learning Word Embedding on Lil'log](https://lilianweng.github.io/lil-log/2017/10/15/learning-word-embedding.html)





























