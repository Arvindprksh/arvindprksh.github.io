---
layout: post
title: Multi-prototype Chinese Character Embedding
subtitle: Title of paper - Multi-prototype Chinese Character Embedding
category: NLP papers - Character Embedding
tags: [tagging]
permalink: /2020/05/02/Multi-prototype_Chinese_Character_Embedding/
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

This is a brief summary of paper for me to study and arrange for [Multi-prototype Chinese Character Embedding. Lu, Zhang, and Ji. 2016 LREC](https://www.aclweb.org/anthology/L16-1138/) I read and studied. 
{% include MathJax.html %}

This paper is a research ralted to character embedding 

They designed the model to train character vector based on skip-gram model with word as input. there are a reason for their to suggest multi-prototype character embedidng. 

The reason is that Characters are highly polysemous in forming words.

They make three significant changes to [MSSG](https://www.aclweb.org/anthology/D14-1113/) for the character embedding task.

First, they predict the sense of the current character given the context directly by using a neural model, rather than by finding the cluster center which is closed to average context vector. 

Second, characters are highly order-sensitive in forming words, they add position into the context by combining a character with its position, so each character in each position (relative to the current character position) has a embedding.

This results in a position-sensitive variation of the Skipgram model.

In addition, the number of senses per character is induced from a lexicon rather than automatically.

Their model is as follows:

![Lu, Zhang, and Ji. 2016 LREC](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-05-02-Multi-prototype_Chinese_Character_Embedding/Multi-prototype_embedding.PNG)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Chinese sentences are written as sequences of characters, which are elementary units of syntax and semantics. Characters are highly polysemous in forming words. They present a position-sensitive skip-gram model to learn multi-prototype Chinese character embeddings, and explore the usefulness of such character embeddings to Chinese NLP tasks. Evaluation on character similarity shows that multi-prototype embeddings are significantly better than a single-prototype baseline.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/L16-1138/">The paper:  Multi-prototype Chinese Character Embedding. Lu, Zhang, and Ji. 2016 LREC</a>
</div>

# Reference 

- Paper 
  - [LREC 2016 version: Multi-prototype Chinese Character Embedding. Lu, Zhang, and Ji. 2016 LREC](https://www.aclweb.org/anthology/L16-1138/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    

