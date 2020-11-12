---
layout: post
title: Deep contextualized word representations. Peters et al. NAACL. 2018.
subtitle: Title of paper - Deep contextualized word representations. Peters et al. NAACL. 2018.
category: NLP papers - Transfer Learning
tags: [neural network, contextual embedding]
permalink: /2019/12/02/Deep_Contextualized_Word_Representations/
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

This is a brief summary of paper for me to study and organize it, [Deep Contextualized Word Representations. Peters et al. NAACL 2018](https://www.aclweb.org/anthology/N18-1202/) I read and studied. 
{% include MathJax.html %}

Their archtecture could be shown as following:

![Transfer Learning Natural Language Processing tutorial](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Contextual_Embedding/2019-12-02-Deep_Contextualized_Word_Representations/ELMo_method.PNG)

Pretrain deep bidirectional LM, extract contextual word vectors as learned linear combination of hidden states

For detail of therir method, If you want to require it, visit the videos below.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
They introduce a new type of deep contextualized word representation that models both (1) complex characteristics of word use (e.g., syntax and semantics), and (2) how these uses vary across linguistic contexts (i.e., to model polysemy). Their word vectors are learned functions of the internal states of a deep bidirectional language model (biLM), which is pretrained on a large text corpus. They show that these representations can be easily added to existing models and significantly improve the state of the art across six challenging NLP problems, including question answering, textual entailment and sentiment analysis. They also present an analysis showing that exposing the deep internals of the pre-trained network is crucial, allowing downstream models to mix different types of semi-supervision signals.
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/N18-1202/">The paper: Deep Contextualized Word Representations Peters et al. NAACL 2018</a>
</div>

<div id="tutorial-section">

  <div id="tutorial-title">ELMo Youtube & language model youtube</div>

  <ul class="nav nav-pills">
    <li class="active"><a data-toggle="tab" href="#ELMo1">ELMo1</a></li>
    <li><a data-toggle="tab" href="#ELMo2">ELMo2</a></li>
    <li><a data-toggle="tab" href="#Language_model">Language model</a></li>
  </ul>

  <div class="tab-content">
    <div id="ELMo1" class="tab-pane fade in active">
      <iframe src="https://player.vimeo.com/video/277672840" width="560" height="315" frameborder="0" allowfullscreen></iframe>
    </div>
    <div id="ELMo2" class="tab-pane fade">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/9JfGxKkmBc0" frameborder="0" allowfullscreen></iframe> 
    </div>
    <div id="Language_model" class="tab-pane fade">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/6N-fev9Zm2s" frameborder="0" allowfullscreen></iframe>
    </div>
  </div>
</div>


# Reference 

- Paper 
  - [arXiv version: Deep Contextualized Word Representations. Peters et al. arXiv 2018](https://arxiv.org/abs/1802.05365)
  - [NAACL 2018 version: Deep Contextualized Word Representations. Peters et al. NAACL 2018](https://www.aclweb.org/anthology/N18-1202/)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
- For your information
  - [NAACL 2019 Highlight on Ruder.io](http://ruder.io/naacl2019/)
  - [ELMo of Allen NLP](https://allennlp.org/elmo)
  - [Deep Contextualized Word Representations Peters et al. NAACL 2018 on Paper with code](https://paperswithcode.com/paper/deep-contextualized-word-representations)
  
  - Slide 
    - [Transfer Learning in Natural Language Processing tutorial on NAACL-HLT 2019](https://docs.google.com/presentation/d/1fIhGikFPnb7G5kr58OvYC3GN4io7MznnM0aAgadvJfc/edit#slide=id.g5888218f39_177_4)
