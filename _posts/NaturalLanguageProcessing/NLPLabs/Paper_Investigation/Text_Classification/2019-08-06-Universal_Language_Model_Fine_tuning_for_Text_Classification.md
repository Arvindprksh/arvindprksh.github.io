---
layout: post
title: Universal Language Model Fine-tuning for Text Classification
subtitle: Title of paper - Universal Language Model Fine-tuning for Text Classification
category: NLP papers - Transfer Learning
tags: [neural network, text classification]
permalink: /2019/08/06/Universal_Language_Model_Fine_tuning_for_Text_Classification/
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

This is a brief summary of paper for me to study and organize it, [Universal Language Model Fine-tuning for Text Classification, Howard and Ruder.(ACL 2018)](https://arxiv.org/abs/1801.06146) I read and studied. 
{% include MathJax.html %}

They propose how to fine-tune Language model to transfer into another task. 

The fine-tuning of LM has a problem called **catastrophic forgetting**

So They argue, when you fine-tune LM, you apply correct way to do fine-tunning.

They propose two types of fine-tuning, **discriminative fine-tuning** and **slanted triangular learning rates**.

- Discriminative fine-tuning 

> As different layers acpture different types of information(Yosinki et al., 2014), they shoud be fine-tuned to different extents using different learning rates.

- slanted triangular le fine-tuning 

> This is the way to adapt model's parameters to task-specific features to quickly converge to a suitable region of the parameter space in the beginning of training and the refine its parameter.

Also they proposed fine-tuning of classifier. 

The way to fine-tune the classifier is  **gradual unfreezing** which is unfreezing the the model starting from last layer as this contains the least gneenral knowledge. i.e. They first unfreeze the last layer and fine-tune all unfrozen layers for one epoch. They then unfreeze the next lower layer and repeat, until they fine-tune all layers until convergence at the last iteration.

![Howard and Ruder(ACL 2018)](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Classification/2019-08-06-Universal_Language_Model_Fine_tuning_for_Text_Classification/ULMFiT.png)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Inductive transfer learning has greatly impacted computer vision, but existing approaches in NLP still require task-specific modifications and training from scratch. We propose Universal Language Model Fine-tuning (ULMFiT), an effective transfer learning method that can be applied to any task in NLP, and introduce techniques that are key for fine-tuning a language model. Our method significantly outperforms the state-of-the-art on six text classification tasks, reducing the error by 18-24% on the majority of datasets. Furthermore, with only 100 labeled examples, it matches the performance of training from scratch on 100x more data. We open-source our pretrained models and code.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1801.06146">The paper: Universal Language Model Fine-tuning for Text Classification</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Universal Language Model Fine-tuning for Text Classification](https://arxiv.org/abs/1801.06146)
  - [ACL 2018 version: Universal Language Model Fine-tuning for Text Classification](https://aclweb.org/anthology/P18-1031)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [NAACL 2019 Highlight on Ruder.io](http://ruder.io/naacl2019/)
  
  - Slide 
    - [Transfer Learning in Natural Language Processing tutorial on NAACL-HLT 2019](https://docs.google.com/presentation/d/1fIhGikFPnb7G5kr58OvYC3GN4io7MznnM0aAgadvJfc/edit#slide=id.g5888218f39_177_4)
































