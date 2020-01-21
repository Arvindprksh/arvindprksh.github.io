---
layout: post
title: Semi-supervised sequence tagging with bidirectional language models
subtitle: Title of paper - Semi-supervised sequence tagging with bidirectional language models
category: NLP papers - Transfer Learning
tags: [neural network, contextual embedding]
permalink: /2019/08/06/Semi-supervised_sequence_tagging_with_bidirectional_language_models/
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

This is a brief summary of paper for me to study and organize it, [Semi-supervised sequence tagging with bidirectional language models. Peters et al. ACL 2017](https://www.aclweb.org/anthology/P17-1161/) I read and studied. 
{% include MathJax.html %}

They used the tokens (i.e. words) sensitive to context surrounding it. 

In order to make the context sensitive representation, they used pre-training LM called **LM embedding** in their paper.

They show how to used a LM embedding component in the following

![Peters et al. ACL 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Contextual_Embedding/2019-12-16-Semi-supervised_sequence_tagging_with_bidirectional_language_models/Semi-supervised_sequence_tagging_1.PNG)

The total overview of their TagLM is as follows: 

![Peters et al. ACL 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Contextual_Embedding/2019-12-16-Semi-supervised_sequence_tagging_with_bidirectional_language_models/Semi-supervised_sequence_tagging_2.PNG)

Though their idea is simple, the resuling performance is superior to the previous moethod at the moment. 

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Pre-trained word embeddings learned from unlabeled text have become a standard component of neural network architectures for NLP tasks. However, in most cases, the recurrent network that operates on word-level representations to produce context sensitive representations is trained on relatively little labeled data. In this paper, they demonstrate a general semi-supervised approach for adding pretrained context embeddings from bidirectional language models to NLP systems and apply it to sequence labeling tasks. They evaluate our model on two standard datasets for named entity recognition (NER) and chunking.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P17-1161/">The paper: Semi-supervised sequence tagging with bidirectional language models. Peters et al. ACL 2017</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Semi-supervised sequence tagging with bidirectional language models. Peters et al. ACL 2017](https://arxiv.org/pdf/1705.00108.pdf)
  - [ACL 2017 version: Semi-supervised sequence tagging with bidirectional language models. Peters et al. ACL 2017](https://www.aclweb.org/anthology/P17-1161/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [NAACL 2019 Highlight on Ruder.io](http://ruder.io/naacl2019/)
  
  - Slide 
    - [Transfer Learning in Natural Language Processing tutorial on NAACL-HLT 2019](https://docs.google.com/presentation/d/1fIhGikFPnb7G5kr58OvYC3GN4io7MznnM0aAgadvJfc/edit#slide=id.g5888218f39_177_4)
































