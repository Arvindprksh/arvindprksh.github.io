---
layout: post
title: Semi-supervised Multitask Learning for Sequence Labeling
subtitle: Title of paper - Semi-supervised Multitask Learning for Sequence Labeling
category: NLP papers - Tagging
tags: [tagging]
permalink: /2020/06/23/Semi-supervised_Multitask_Learning_for_Sequence_Labeling/
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

This is a brief summary of paper for me to study and organize it, [Semi-supervised Multitask Learning for Sequence Labeling. Marek Rei. ACL 2017](https://www.aclweb.org/anthology/P17-1194/) I read and studied. 
{% include MathJax.html %}

This paper proposed a method using auxiliary objection for sequence labeling task. 

They chose the language modeling as secondary objective loss for sequence labelding as follow:

![Marek Rei. ACL 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-06-23-Semi-supervised_Multitask_Learning_for_Sequence_Labeling/secondary_objective_model.PNG)


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They propose a sequence labeling framework with a secondary training objective, learning to predict surrounding words for every word in the dataset. This language modeling objective incentivises the system to learn general-purpose patterns of semantic and syntactic composition, which are also useful for improving accuracy on different sequence labeling tasks. The architecture was evaluated on a range of datasets, covering the tasks of error detection in learner texts, named entity recognition, chunking and POS-tagging. The novel language modeling objective provided consistent performance improvements on every benchmark, without requiring any additional annotated or unannotated data.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P17-1194/">The paper: Semi-supervised Multitask Learning for Sequence Labeling. Marek Rei. ACL 2017</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Semi-supervised Multitask Learning for Sequence Labelingg. Marek Rei. arXiv 2017](https://arxiv.org/abs/1704.07156)
  - [ACL 2017 version: Semi-supervised Multitask Learning for Sequence Labeling. Marek Rei. ACL 2017](https://www.aclweb.org/anthology/P17-1194/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


