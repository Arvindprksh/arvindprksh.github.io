---
layout: post
title: How transferable are features in deep neural networks?
subtitle: Title of paper - How transferable are features in deep neural networks?
category: NN papers - Analysis
tags: [neural network, analysis]
permalink: /2019/09/24/How_Transferable_are_Features_in_Deep_Neural_Networks/
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

This is a brief summary of paper for me to note it, [How transferable are features in deep neural networks?, Yosinski et al. (2014)](https://papers.nips.cc/paper/5347-how-transferable-are-features-in-deep-neural-networks)

{% include MathJax.html %}


They show the feature transferability with empirical experiment. 

They said first-layer features, they called general, is independent of teh exact cost function and natural dataset. 

However, the last-layer features, they called specific, is greatly dependent on the chosen dataset and task. 

Let's see the figure they demonstrated :


![Yosinski et al. (2014)](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Neural_Network/2019-09-24-How_Transferable_are_Features_in_Deep_Neural_Networks/how_transferable_are_features_in_deep_neural_networks.JPG)



<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Many deep neural networks trained on natural images exhibit a curious phenomenon in common: on the first layer they learn features similar to Gabor filters and color blobs. Such first-layer features appear not to be specific to a particular dataset or task, but general in that they are applicable to many datasets and tasks. Features must eventually transition from general to specific by the last layer of the network, but this transition has not been studied extensively. In this paper they experimentally quantify the generality versus specificity of neurons in each layer of a deep convolutional neural network and report a few surprising results. Transferability is negatively affected by two distinct issues: (1) the specialization of higher layer neurons to their original task at the expense of performance on the target task, which was expected, and (2) optimization difficulties related to splitting networks between co-adapted neurons, which was not expected. In an example network trained on ImageNet, they demonstrated that either of these two issues may dominate, depending on whether features are transferred from the bottom, middle, or top of the network. they also documented that the transferability of features decreases as the distance between the base task and target task increases, but that transferring features even from distant tasks can be better than using random features. A final surprising result is that initializing a network with transferred features from almost any number of layers can produce a boost to generalization that lingers even after fine-tuning to the target dataset.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://papers.nips.cc/paper/5347-how-transferable-are-features-in-deep-neural-networks">The paper: How transferable are features in deep neural networks?, Yosinski et al. (2014)</a>
</div>

# Reference 

- Paper 
  - [ArXiv version: How transferable are features in deep neural networks?, Yosinski et al. (2014)](https://arxiv.org/abs/1411.1792)
  - [NIPS version: How transferable are features in deep neural networks?, Yosinski et al. (2014)](https://papers.nips.cc/paper/5347-how-transferable-are-features-in-deep-neural-networks)
  
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
