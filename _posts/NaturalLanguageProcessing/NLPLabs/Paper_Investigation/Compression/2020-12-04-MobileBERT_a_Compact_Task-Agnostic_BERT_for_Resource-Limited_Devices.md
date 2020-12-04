---
layout: post
title: MobileBERT- a Compact Task-Agnostic BERT for Resource-Limited Devices
subtitle: Title of paper - MobileBERT- a Compact Task-Agnostic BERT for Resource-Limited Devices
category: NLP papers - Compression
tags: [compression]
permalink: /2020/12/04/MobileBERT_a_Compact_Task-Agnostic_BERT_for_Resource-Limited_Devices/
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

This is a brief summary of paper for me to study and organize it, [Addressing the Rare Word Problem in Neural Machine Translation (MobileBERT: a Compact Task-Agnostic BERT for Resource-Limited Devices (Sun et al., ACL 2020)](https://www.aclweb.org/anthology/2020.acl-main.195/) that I read and studied. 
{% include MathJax.html %}

They proposed task-agnostic BERT for Resouce-Limited Devices by using layerwise knowledge distilattion technique  as follows:

![Sun et al., ACL 2020](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Compression/2020-12-04-MobileBERT_a_Compact_Task-Agnostic_BERT_for_Resource-Limited_Devices/architecture.PNG)

For detailed experiment analysis, you can found in [MobileBERT: a Compact Task-Agnostic BERT for Resource-Limited Devices (Sun et al., ACL 2020)](https://www.aclweb.org/anthology/2020.acl-main.195/)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Natural Language Processing (NLP) has recently achieved great success by using huge pre-trained models with hundreds of millions of parameters. However, these models suffer from heavy model sizes and high latency such that they cannot be deployed to resourcelimited mobile devices. In this paper, they propose MobileBERT for compressing and accelerating the popular BERT model. Like the original BERT, MobileBERT is task-agnostic, that is, it can be generically applied to various downstream NLP tasks via simple fine-tuning. Basically, MobileBERT is a thin version of BERTLARGE, while equipped with bottleneck structures and a carefully designed balance between self-attentions and feed-forward networks. To train MobileBERT, they first train a specially designed teacher model, an invertedbottleneck incorporated BERTLARGE model.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/2020.acl-main.195/">The paper: MobileBERT: a Compact Task-Agnostic BERT for Resource-Limited Devices (Sun et al., ACL 2020)</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: MobileBERT: a Compact Task-Agnostic BERT for Resource-Limited Devices (Sun et al., arXiv 2020)](https://arxiv.org/abs/2004.02984)
  - [ACL Version: MobileBERT: a Compact Task-Agnostic BERT for Resource-Limited Devices (Sun et al., ACL 2020)](https://www.aclweb.org/anthology/2020.acl-main.195/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


