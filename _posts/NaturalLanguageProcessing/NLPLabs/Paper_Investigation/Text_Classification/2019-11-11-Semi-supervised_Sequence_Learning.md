---
layout: post
title: Semi-supervised Sequence Learning
subtitle: Title of paper - Semi-supervised Sequence Learning
category: NLP papers - Transfer Learning
tags: [neural network, text classification, word dropout]
permalink: /2019/11/11/Semi-supervised_Sequence_Learning/
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

This is a brief summary of paper for me to study and organize it, [Semi-supervised Sequence Learning, Dai and Le. NIPS 2015](https://papers.nips.cc/paper/5949-semi-supervised-sequence-learning) I read and studied. 
{% include MathJax.html %}

This paper showed the pretrainig with unlabeled data improve the performance of text classification. 

They present two approaches that sequence autoencoder and Language modeling with recurrent nueral network. 

Below is the sequence autoencoder firgure they used: 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Classification/2019-11-11-Semi-supervised_Sequence_Learning/semi-supervised_sequence_learning.PNG)

Interesting experiment to me is that they used CIFAR-10 to classify imaget with LSTM pretraining.

The input to a LSTM is an entire row of pixels and they predict the class of the image after reading the final row. 

In this case, for pretraining based on Language modeling, they tranied LSTM to do next row prediction given the current row.

Another method for sequence auhoencoder autoencode the image by rows.

And the loss function during unsupervised learning is the Eucledean L2 distance between prediction and the target row. 

For details, read section  4.5 Object classification experiments with CIFAR-10 in their paper.

They said 

>>  They demonstrated that a language model or a sequence autoencoder can help stabilize the learning in LSTM recurrent networks.

Also They used **word dropout**

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They present two approaches to use unlabeled data to improve Sequence Learning with recurrent networks. The first approach is to predict what comes next in a sequence, which is a language model in NLP. The second approach is to use a sequence autoencoder, which reads the input sequence into a vector and predicts the input sequence again. These two algorithms can be used as a “pretraining” algorithm for a later supervised sequence learning algorithm. In other words, the parameters obtained from the pretraining step can then be used as a starting point for other supervised training models. In they experiments, we find that long short term memory recurrent networks after pretrained with the two approaches become more stable to train and generalize better.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://papers.nips.cc/paper/5949-semi-supervised-sequence-learning">The paper: Semi-supervised Sequence Learning, Andrew M. Dai and Quoc V. Le.(NIPS 2015)</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: Semi-supervised Sequence Learning, Dai and Le. arXiv 2015](https://arxiv.org/abs/1511.01432)
  - [NIPS Version: Semi-supervised Sequence Learning, Dai and Le. NIPS 2015](https://papers.nips.cc/paper/5949-semi-supervised-sequence-learning)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [NAACL 2019 Highlight on Ruder.io](http://ruder.io/naacl2019/)
  
  - Slide 
    - [Transfer Learning in Natural Language Processing tutorial on NAACL-HLT 2019](https://docs.google.com/presentation/d/1fIhGikFPnb7G5kr58OvYC3GN4io7MznnM0aAgadvJfc/edit#slide=id.g5888218f39_177_4)
































