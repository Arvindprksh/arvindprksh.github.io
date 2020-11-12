---
layout: post
title: Compositional Sequence Labeling Models for Error Detection in Learner Writing
subtitle: Title of paper - Compositional Sequence Labeling Models for Error Detection in Learner Writing
category: NLP papers - Error Dectection
tags: [error dectection]
permalink: /2020/07/01/Compositional_Sequence_Labeling_Models_for_Error_Detection_in_Learner_Writing/
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

This is a brief summary of paper for me to study and organize it, [Compositional Sequence Labeling Models for Error Detection in Learner Writing.  Rei and Yannakoudakis. ACL 2016](https://www.aclweb.org/anthology/P16-1112/) I read and studied. 
{% include MathJax.html %}

This paper popose a method to detect error in learner writing by tackling it as sequence labeling task. 

Empirically, they experimented the method with compoistion architectures which are convolution neural network, recurrent netword, and Long-short term memory as follows:

In paritcular, for LSTM, they used peephole LSTM.

![Rei and Yannakoudakis. ACL 2016](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-07-01-Compositional_Sequence_Labeling_Models_for_Error_Detection_in_Learner_Writing/error_dectection.PNG)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
In this paper, they present the first experiments using neural network models for the task of error detection in learner writing. We perform a systematic comparison of alternative compositional architectures and propose a framework for error detection based on bidirectional LSTMs. Experiments on the CoNLL-14 shared task dataset show the model is able to outperform other participants on detecting errors in learner writing. Finally, the model is integrated with a publicly deployed self-assessment system, leading to performance comparable to human annotators.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P16-1112/">The paper: Compositional Sequence Labeling Models for Error Detection in Learner Writing.  Rei and Yannakoudakis. ACL 2016</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: Compositional Sequence Labeling Models for Error Detection in Learner Writing. Rei and Yannakoudakis. arXiv 2016](https://arxiv.org/abs/1607.06153)
  - [ACL Version: Compositional Sequence Labeling Models for Error Detection in Learner Writing.  Rei and Yannakoudakis. ACL 2016](https://www.aclweb.org/anthology/P16-1112/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


