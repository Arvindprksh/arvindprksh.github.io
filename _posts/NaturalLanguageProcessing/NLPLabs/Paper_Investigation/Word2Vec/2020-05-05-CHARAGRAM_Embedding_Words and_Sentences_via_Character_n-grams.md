---
layout: post
title: CHARAGRAM- Embedding Words and Sentences via Character n-grams
subtitle: Title of paper - CHARAGRAM- Embedding Words and Sentences via Character n-grams
category: NLP papers - Sentence Embedding
tags: [neural network, sentence embedding]
permalink: /2020/05/05/CHARAGRAM_Embedding_Words and_Sentences_via_Character_n-grams/
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

This is a brief summary of paper for me to study and arrange it, [CHARAGRAM: Embedding Words and Sentences via Character n-grams. Wieting et al. EMNLP 2016](https://www.aclweb.org/anthology/D16-1157/) I read and studied. 
{% include MathJax.html %}

This paper propose character embedding for word, sentence similarity and tagging problem.

character n-gram match exactly for its vector in character n-gram embedding model. 

Also they said the character n-gram captures aspects of word order and word co-occurence in CHARACGRAM-PHRASE.

They use a white-space as a special token which they think it is regarded as signal of the beggining and end of a word in CHARAGRAM-PHRASE.

In other words, they model a character-based textual sequence by \\(x\\) = \\(<x_1, x_2, ... , x_m>\\), which includes space characters between words as well as special start-of_sequence and end-of_sequence characters.

The CHARAGRAM model embeds a character sequence \\(x\\) by adding the vectors of it character n-grams followed by an elemenwise nonlinearity.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They present CHARAGRAM embeddings, a simple approach for learning character-based compositional models to embed textual sequences. A word or sentence is represented using a character n-gram count vector, followed by a single nonlinear transformation to yield a low-dimensional embedding. They use three tasks for evaluation: word similarity, sentence similarity, and part-of-speech tagging. They demonstrate that CHARAGRAM embeddings outperform more complex architectures based on character-level recurrent and convolutional neural networks, achieving new state-of-the-art performance on several similarity tasks.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/D16-1157/">The paper- CHARAGRAM: Embedding Words and Sentences via Character n-grams. Wieting et al. EMNLP 2016</a>
</div>

# Reference 

- Paper 
  - [arXiv version- CHARAGRAM: Embedding Words and Sentences via Character n-grams. Wieting et al. arXiv 2016](https://arxiv.org/abs/1607.02789v1)
  - [EMNLP 2016 version- CHARAGRAM: Embedding Words and Sentences via Character n-grams. Wieting et al. EMNLP 2016](https://www.aclweb.org/anthology/D16-1157/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    






























