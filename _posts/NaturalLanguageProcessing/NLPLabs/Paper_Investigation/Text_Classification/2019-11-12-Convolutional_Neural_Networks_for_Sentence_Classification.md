---
layout: post
title: Convolutional Neural Networks for Sentence Classification
subtitle: Title of paper - Convolutional Neural Networks for Sentence Classification
category: NLP papers - Transfer Learning
tags: [neural network, text classification]
permalink: /2019/11/12/Convolutional_Neural_Networks_for_Sentence_Classification/
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

This is a brief summary of paper for me to study and organize it, [EMNLP 2014 version: Convolutional Neural Networks for Sentence Classification (Kim. 2014)](https://www.aclweb.org/anthology/D14-1181/) I read and studied. 
{% include MathJax.html %}

They propose CNN architecture on top two sets of pre-training **word2vecs**, static and dynamic one.  

Their architecture is the followings: 

![(Kim. 2014)](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Classification/2019-11-12-Convolutional_Neural_Networks_for_Sentence_Classification/convolutional neural networks for Sentence Classification_1.PNG)

For two sets of pre-training word vectors, one of **word2vecs** is kept static throughout training training and another is fine-tuned via backpropagation. 

The following is examples of top 4 neighboring words based on cosine similarity for static channel(left) and fine-tuned vectors in the non-static channel (right) for multichannel model.

![(Kim. 2014)](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Classification/2019-11-12-Convolutional_Neural_Networks_for_Sentence_Classification/convolutional neural networks for Sentence Classification_2.PNG)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They report on a series of experiments with convolutional neural networks (CNN) trained on top of pre-trained word vectors for sentence-level classification tasks. They show that a simple CNN with little hyperparameter tuning and static vectors achieves excellent results on multiple benchmarks. Learning task-specific vectors through fine-tuning offers further gains in performance. They additionally propose a simple modification to the architecture to allow for the use of both task-specific and static vectors.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/D14-1181/">The paper: Convolutional Neural Networks for Sentence Classification (Kim. 2014)</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Convolutional Neural Networks for Sentence Classification (Kim 2014)](https://arxiv.org/abs/1408.5882)
  - [EMNLP 2014 version: Convolutional Neural Networks for Sentence Classification (Kim 2014)](https://www.aclweb.org/anthology/D14-1181/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [NAACL 2019 Highlight on Ruder.io](http://ruder.io/naacl2019/)
  
  - Slide 
    - [Transfer Learning in Natural Language Processing tutorial on NAACL-HLT 2019](https://docs.google.com/presentation/d/1fIhGikFPnb7G5kr58OvYC3GN4io7MznnM0aAgadvJfc/edit#slide=id.g5888218f39_177_4)
































