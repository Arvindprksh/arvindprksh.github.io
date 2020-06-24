---
layout: post
title: Neural Architectures for Named Entity Recognition
subtitle: Title of paper - Neural Architectures for Named Entity Recognition
category: NLP papers - Tagging
tags: [tagging]
permalink: /2020/06/24/Neural_Architectures_for_Named_Entity_Recognition/
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

This is a brief summary of paper for me to study and organize it, [Neural Architectures for Named Entity Recognition. Lample et al. NAACL 2016](https://www.aclweb.org/anthology/N16-1030/) I read and studied. 
{% include MathJax.html %}

They propose two method for Named Entity recognition (NER) task. 

The one is bidirectinal LSTM with conditional random field.

![Lample et al. NAACL 2016](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-06-24-Neural_Architectures_for_Named_Entity_Recognition/BiLSTM_CRF.PNG)

The other is stack LSTMs for chuncking method, inspired by transition-based parsing

![Lample et al. NAACL 2016](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-06-24-Neural_Architectures_for_Named_Entity_Recognition/transition_based.PNG)

In their methods, they used character embeddding to use e orthographic or morphological information.

![Lample et al. NAACL 2016](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-06-24-Neural_Architectures_for_Named_Entity_Recognition/character_embedding.PNG)

>>They found that the Stack-LSTM model is more dependent on character-based representations to achieve competitive performance. they hypothesize that the LSTM-CRF model requires less orthographic information since it gets more contextual information out of the bidirectional LSTMs. However, the Stack-LSTM model consumes the words one by one and it just relies on the word representations when it chunks words.  



<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
State-of-the-art named entity recognition systems rely heavily on hand-crafted features and domain-specific knowledge in order to learn effectively from the small, supervised training corpora that are available. In this paper, they introduce two new neural architectures—one based on bidirectional LSTMs and conditional random fields, and the other that constructs and labels segments using a transition-based approach inspired by shift-reduce parsers. Their models rely on two sources of information about words: character-based word representations learned from the supervised corpus and unsupervised word representations learned from unannotated corpora. Their models obtain state-of-the-art performance in NER in four languages without resorting to any language-specific knowledge or resources such as gazetteers.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/N16-1030/">The paper: Neural Architectures for Named Entity Recognition. Lample et al. NAACL 2016</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Neural Architectures for Named Entity Recognition. Lample et al. arXiv 2016](https://arxiv.org/abs/1603.01360)
  - [NAACL 2016 version: Neural Architectures for Named Entity Recognition. Lample et al. NAACL 2016](https://www.aclweb.org/anthology/N16-1030/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


