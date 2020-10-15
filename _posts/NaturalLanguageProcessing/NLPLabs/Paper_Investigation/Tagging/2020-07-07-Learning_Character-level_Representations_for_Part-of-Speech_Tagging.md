---
layout: post
title: Learning Character-level Representations for Part-of-Speech Tagging
subtitle: Title of paper - Learning Character-level Representations for Part-of-Speech Tagging
category: NLP papers - POS Tagging
tags: [pos tagging]
permalink: /2020/07/07/Learning_Character-level_Representations_for_Part-of-Speech_Tagging/
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

This is a brief summary of paper for me to study and organize it, [ICML 2014 version: Learning Character-level Representations for Part-of-Speech Tagging. Santos and Zadrozny. ICML 2014](http://proceedings.mlr.press/v32/santos14.html/) I read and studied. 
{% include MathJax.html %}

They used character embedding not pretrained other than word embedding pretrained. 

They concatented character and word embedding, and characters is a intra-word to be used to extract morphological and shape information. 

When constructing a word-level representation from characters, they used CNN network as follows:

![Santos and Zadrozny. ICML 2014](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-07-07-Learning_Character-level_Representations_for_Part-of-Speech_Tagging/cnn_embedding.PNG)

The next layer used the concatenation of word-symbol and word-level representation with sucessive window centralized in a target word. 

Finally, They compute the cost function of strucured inference depending neighboring tags.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Distributed word representations have recently been proven to be an invaluable resource for NLP. These representations are normally learned  using neural networks and capture syntactic and semantic information about words. Information about word morphology and shape is normally ignored when learning word representations. However, for tasks like part-of-speech tagging, intra-word information is extremely useful, specially when dealing with morphologically rich languages. In this paper, they propose a deep neural network that learns character-level representation of words and associate them with usual word representations to perform POS tagging. Using the proposed approach, while avoiding the use of any handcrafted feature,  they produce stateof-the-art POS taggers for two languages: English, with 97.32% accuracy on the Penn Treebank WSJ corpus; and Portuguese, with 97.47% accuracy on the Mac-Morpho corpus, where the latter represents an error reduction of 12.2% on the best previous known result.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="http://proceedings.mlr.press/v32/santos14.html/">The paper: Learning Character-level Representations for Part-of-Speech Tagging. Santos and Zadrozny. ICML 2014</a>
</div>

# Reference 

- Paper 
  - [ICML 2014 version: Learning Character-level Representations for Part-of-Speech Tagging. Santos and Zadrozny. ICML 2014](http://proceedings.mlr.press/v32/santos14.html/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


