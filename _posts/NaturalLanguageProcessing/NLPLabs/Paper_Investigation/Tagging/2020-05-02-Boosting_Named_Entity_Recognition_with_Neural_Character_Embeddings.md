---
layout: post
title: Boosting Named Entity Recognition with Neural Character Embeddings
subtitle: Title of paper - Boosting Named Entity Recognition with Neural Character Embeddings
category: NLP papers - Tagging
tags: [tagging]
permalink: /2020/05/02/Boosting_Named_Entity_Recognition_with_Neural_Character_Embeddings/
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

This is a brief summary of paper for me to study and arrange for [Boosting Named Entity Recognition with Neural Character Embeddings. Santos and Guimarães. 2015 NEWS workshop](https://www.aclweb.org/anthology/W15-3904/) I read and studied. 
{% include MathJax.html %}

This paper is a research ralted to NER tagging and focus on not using the handcrafted fetaures and the output of other NLP tasks such as part-of-speech tagging and text chuncking.

Ther model jointly trained word and character embedding to boost the performance of NER task in Portuguese and Spanish.

representing character embedding in a word, they use covoutional neural network with max operation to generate a fix-size vector. 

And then they have an assumption that in sequential classification tag of word mainly depends on its neghboring words. 

So they joinlty concatenate word and character embedding corresponding to each word in a window which is hyper-parameter as follows:

![Santos and Guimarães. 2015](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-05-02-Boosting_Named_Entity_Recognition_with_Neural_Character_Embeddings/CharWNN.PNG)

They use a tag style called IOB2.

The following is an example they show in their paper:

![Santos and Guimarães. 2015](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-05-02-Boosting_Named_Entity_Recognition_with_Neural_Character_Embeddings/IOB2.PNG)



<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Most state-of-the-art named entity recognition (NER) systems rely on handcrafted features and on the output of other NLP tasks such as part-of-speech (POS) tagging and text chunking. In this work they propose a language-independent NER system that uses automatically learned features only. Their approach is based on the CharWNN deep neural network, which uses word-level and character-level representations (embeddings) to perform sequential classification. 
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/W15-3904/">The paper: Boosting Named Entity Recognition with Neural Character Embeddings. Santos and Guimarães 2015 NEWS workshop</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Boosting Named Entity Recognition with Neural Character Embeddings. Santos and Guimarães. 2015 arXiv](https://arxiv.org/abs/1505.05008)
  - [TACL 2016 version: Boosting Named Entity Recognition with Neural Character Embeddings. Santos and Guimarães. 2015 NEWS workshop](https://www.aclweb.org/anthology/W15-3904/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    




























