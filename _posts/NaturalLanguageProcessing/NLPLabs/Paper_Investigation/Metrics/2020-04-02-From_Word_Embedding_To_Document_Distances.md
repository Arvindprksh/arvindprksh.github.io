---
layout: post
title: From Word Embeddings To Document Distances
subtitle: Title of paper - From Word Embeddings To Document Distances
category: NLP papers - Metrics
tags: [metrics, distance]
permalink: /2020/04/02/From_Word_Embedding_To_Document_Distances/
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

This is a brief summary of paper for me to study and organize it, [From word embeddings to document distances. Kusner et al. 2015 ICML](https://dl.acm.org/doi/10.5555/3045118.3045221) I read and studied. 
{% include MathJax.html %}

WMD use word embeddings to calculate the distance so that it can calculate even though there is no common word. The assumption is that similar words should have similar vectors.

![Captured from Kusner et al. publication](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Metrics/2020-04-02-From_Word_Embedding_To_Document_Distances/Dist1.PNG)

First of all, lower case and removing stopwords is an essential step to reduce complexity and preventing misleading.

> Sentence 1: obama speaks media illinois  
> Sentence 2: president greets press chicago  

Retrieve vectors from any pre-trained word embeddings models. It can be GloVe, word2vec, fasttext or custom vectors. After that it using normalized bag-of-words (nBOW) to represent the weight or importance. It assumes that higher frequency implies that it is more important.

![Captured from Kusner et al. publication](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Metrics/2020-04-02-From_Word_Embedding_To_Document_Distances/Dist2.PNG)

Strengths of WMD:
 
  - Hyperparameter-free
  - Straight-forward to understand and use, highly interpretable
  - leads to unprecedented low k-nearest neighbor document classification error rates


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They present the Word Mover’s Distance (WMD), a novel distance function between text documents. Their work is based on recent results in word embeddings that learn semantically meaningful representations for words from local cooccurrences in sentences. The WMD distance
measures the dissimilarity between two text documents as the minimum amount of distance that the embedded words of one document need to
“travel” to reach the embedded words of another document. 
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://dl.acm.org/doi/10.5555/3045118.304522">The paper: From word embeddings to document distances. Kusner et al. 2015 ICML</a>
</div>

# Reference 

- Paper 
  - [ICML 2015 version: From word embeddings to document distances. Kusner et al. 2015 ICML](https://dl.acm.org/doi/10.5555/3045118.3045221)
  
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
- References
  - [Word Embedding to Document distances at slideshare](https://www.slideshare.net/GaneshBorle/word-embedding-to-document-distances)
  - [From Word Embeddings To Document Distances pdf](https://stat.snu.ac.kr/idea/seminar/20180426/RNN_tex.pdf)
  - [Earth mover’s distance on towards data science](https://towardsdatascience.com/earth-movers-distance-68fff0363ef2)
  - [Paper: The Earth Mover's Distance as a Metric for Image Retrieval. Rubner et al. 2000 in International journal of computer vision](http://robotics.stanford.edu/~rubner/papers/rubnerIjcv00.pdf)
  - [The Earth Mover's Distance as a Metric for Image Retrieval. Rubner et al. 2000](https://www.cs.cmu.edu/~efros/courses/LBMV07/Papers/rubner-jcviu-00.pdf)
  - [The Earth Mover's Distance](http://homepages.inf.ed.ac.uk/rbf/CVonline/LOCAL_COPIES/RUBNER/emd.htm)
  - [Finding similar documents with Word2Vec and WMD](https://markroxor.github.io/gensim/static/notebooks/WMD_tutorial.html)
  - [Navigating themes in restaurant reviews with Word Mover’s Distance](http://tech.opentable.com/2015/08/11/navigating-themes-in-restaurant-reviews-with-word-movers-distance/)
  - [A Word is Worth a Thousand Vectors](https://multithreaded.stitchfix.com/blog/2015/03/11/word-is-worth-a-thousand-vectors/)
  - [Word Distance between Word Embeddings on towards data science](https://towardsdatascience.com/word-distance-between-word-embeddings-cc3e9cf1d632)
  - [Word Mover’s Distance as a Linear Programming Problem on Medium](https://medium.com/@stephenhky/word-movers-distance-as-a-linear-programming-problem-6b0c2658592e)



























