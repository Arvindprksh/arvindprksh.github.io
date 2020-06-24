---
layout: post
title: Learning Distributed Representations of Sentences from Unlabelled Data
subtitle: Title of paper - Learning Distributed Representations of Sentences from Unlabelled Data
category: NLP papers - Sentence Embedding
tags: [neural network, sentence embedding]
permalink: /2020/06/23/Learning_Distributed_Representations_of_Sentences_from_Unlabelled_Data/
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

This is a brief summary of paper for me to study and arrange it, [Learning Distributed Representations of Sentences from Unlabelled Data. Hill et al. NAACL 2016](https://www.aclweb.org/anthology/N16-1162/) I read and studied. 
{% include MathJax.html %}


They proposed the two approaches to represent a sentence into a fixed-lengtj vector. 

- **Sequential Denoising Autoencoders**:

 In a Denosigin Autoencoder, high-dimensional input data is corrupted according to some noise function, and the model is trained to recover the original data from the corrupted version.

>>The original DAEs were feedforward nets applied to (image) data of fixed size. Here, they adapt the approach to variable-length sentences by means of a noise function N(S|po, px), determined by free parameters po, px ∈ [0, 1]. First, for each word w in S, N deletes w with (independent) probability po.   
>>Then, for each non-overlapping bigram wiwi+1 inS, N swaps wi and wi+1 with probability px.     
>>They then train the same LSTM-based encoder-decoder architecture as NMT, but with the denoising objective to predict (as target) the original source sentence S given a corrupted version N(S|po, px) (as source).  
>>The trained model can then encode novel word sequences into distributed representations.   
>>They call this model the Sequential Denoising Autoencoder (SDAE). Note that, unlike SkipThought, SDAEs can be trained on sets of sentences in arbitrary order.

- **FastSent**:

>>FastSent is a simple additive (log-bilinear) sentence model designed to exploit the same signal, but at much lower computational expense.   
>>Given a BOW representation of some sentence in context, the model simply predicts adjacent sentences (also represented as BOW).  

Also, They experiment a variant (+AE) in which the encoded (source) representation must predict its own words as target in addition to those of adjacent sentences.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Unsupervised methods for learning distributed representations of words are ubiquitous in today’s NLP research, but far less is known about the best ways to learn distributed phrase or sentence representations from unlabelled data. This paper is a systematic comparison of models that learn such representations. They find that the optimal approach depends critically on the intended application. Deeper, more complex models are preferable for representations to be used in supervised systems, but shallow log-bilinear models work best for building representation spaces that can be decoded with simple spatial distance metrics. They also propose two new unsupervised representation-learning objectives designed to optimise the trade-off between training time, domain portability and performance.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/D16-1157/">The paper- CHARAGRAM: Embedding Words and Sentences via Character n-grams. Wieting et al. EMNLP 2016</a>
</div>

# Reference 

- Paper 
  - [arXiv version: Learning Distributed Representations of Sentences from Unlabelled Data. Hill et al. 2016](https://arxiv.org/abs/1602.03483)
  - [NAACL 2016 version: Learning Distributed Representations of Sentences from Unlabelled Data. Hill et al. NAACL 2016](https://www.aclweb.org/anthology/N16-1162/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    






























