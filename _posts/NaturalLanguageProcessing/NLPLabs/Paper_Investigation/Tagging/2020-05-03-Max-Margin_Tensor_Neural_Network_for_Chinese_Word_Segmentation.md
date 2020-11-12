---
layout: post
title: Max-Margin Tensor Neural Network for Chinese Word Segmentation
subtitle: Title of paper - Max-Margin Tensor Neural Network for Chinese Word Segmentation
category: NLP papers - Tagging
tags: [tagging]
permalink: /2020/05/03/Max-Margin_Tensor_Neural_Network_for_Chinese_Word_Segmentation/
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

This is a brief summary of paper for me to study and arrange for [Max-Margin Tensor Neural Network for Chinese Word Segmentation. Pei et al. ACL 2014](https://www.aclweb.org/anthology/P14-1028/) I read and studied. 
{% include MathJax.html %}

This paper is a research ralted to chinese word segmentation task. 

They said that the existing study of chinese word segmeantationa used manual feature engineerings, however the neural network model alleviate the burden of manual feature engineering. 

The following is an example of feature engineering they explained.

![Pei et al. 2014 ACL](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-05-03-Max-Margin_Tensor_Neural_Network_for_Chinese_Word_Segmentation/feature_engineering.PNG)

so they propose an model to utilize neural network with tensor. 

The reason that they use tensor as alternative of non-linear transformation

That is because non-linear transformation poorly models the complex interaction wihch is between tags and characters(e.g. context and target character).

Frist of all, before diving into their model let's see conventional model for chines word segmenation. 

The conventional model is as follows:

![Pei et al. 2014 ACL](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-05-03-Max-Margin_Tensor_Neural_Network_for_Chinese_Word_Segmentation/conventional_model.PNG)

The model is simple, they use an window for context character embedding and then compute hidden layer with concatenation of the center and context character embedding. 

Finally it evaluates score for each tag types. 

They propose Max-margin Tensor Neural Network to model tag-tag, tag-character and character-character interactions in neural network as follows:

![Pei et al. ACL 2014](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-05-03-Max-Margin_Tensor_Neural_Network_for_Chinese_Word_Segmentation/feature_engineering.PNG)


They regarded each slice of the tensor as capturing a specific type of tag-character interaction and character-character interaction. 

The following is bilinear form with tensor on vector a.

![Pei et al. ACL 2014](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-05-03-Max-Margin_Tensor_Neural_Network_for_Chinese_Word_Segmentation/tensor-based_transformation.PNG)


For tensor operation, it is expensive and has the risk of overfitting so they proposed tesor factorization as follows:

![Pei et al. ACL 2014](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-05-03-Max-Margin_Tensor_Neural_Network_for_Chinese_Word_Segmentation/tensor_factorization.PNG)


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Recently, neural network models for natural language processing tasks have been increasingly focused on for their ability to alleviate the burden of manual feature engineering. In this paper, they propose a novel neural network model for Chinese word segmentation called Max-Margin Tensor Neural Network (MMTNN). By exploiting tag embeddings and tensorbased transformation, MMTNN has the ability to model complicated interactions between tags and context characters. Furthermore, a new tensor factorization approach is proposed to speed up the model and avoid overfitting. Their model can achieve a competitive performance with minimal feature engineering. Despite Chinese word segmentation being a specific case, MMTNN can be easily generalized and applied to other sequence labeling tasks. 
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P14-1028/">The paper: Max-Margin Tensor Neural Network for Chinese Word Segmentation. Pei et al. ACL 2014</a>
</div>

# Reference 

- Paper 
  - [ACL Version: Max-Margin Tensor Neural Network for Chinese Word Segmentation. Pei et al. ACL 2014](https://www.aclweb.org/anthology/P14-1028/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    




























