---
layout: post
title: Enhanced LSTM for Natural Language Inference
subtitle: Title of paper - Enhanced LSTM for Natural Language Inference
category: NLP papers - Natural_Language_Inference
tags: [neural_network, text_classification, NLI]
permalink: /2019/12/09/Enhanced_LSTM_for_Natural_Language_Inference/
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

This is a brief summary of paper for me to study and organize it, [Enhanced LSTM for Natural Language Inference.  Chen et al. 2017 ACL](https://www.aclweb.org/anthology/P17-1152/) I read and studied. 
{% include MathJax.html %}

This paper is a research related to  Natural Language inference task.

Entailment task is to predict whether the two sentences are entailment, contradiction, and neutral.

Their model is called ESIM (Enhanced Sequential Inference Model) as in the left below figure.

![Chen et al. 2017 ACL](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Classification/2019-12-09-Enhanced_LSTM_for_Natural_Language_Inference/ESIM_firgure1.PNG)

In here, they used tree-LSTM as follows:

![Chen et al. 2017 ACL](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Classification/2019-12-09-Enhanced_LSTM_for_Natural_Language_Inference/ESIM_firgure2.PNG)

![Chen et al. 2017 ACL](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Classification/2019-12-09-Enhanced_LSTM_for_Natural_Language_Inference/ESIM_firgure3.PNG)

They domonstrates using syntactic parsing information contribute to their best result with tree-LSTM.

They use bidirectional LSTM to ecode a word itself and its context, and then they extraced the local inference information with attention mechanism. 

Before classifying, in order to enhance local inference information, they compute the difference and the elemnt-wise product for the tuple $<a^{-},a^{~}>$
 as well as for $<b^{-},b^{~}>$, where $a^{-} and b^{-}$ is the output of bidirectional LSTMs on a premise and a hypothesis respectively.

Also they used Bidirectional LSTM to compose local inferences into a fixed-lenght vector:

![Chen et al. 2017 ACL](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Classification/2019-12-09-Enhanced_LSTM_for_Natural_Language_Inference/ESIM_firgure4.PNG)

Also this paper showed the a variety of sentence embedding for Natural languae Inference task, suggesting their model outputperform the previous models: 

![Chen et al. 2017 ACL](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Classification/2019-12-09-Enhanced_LSTM_for_Natural_Language_Inference/ESIM_firgure5.PNG)


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Reasoning and inference are central to human and artificial intelligence. Modeling inference in human language is very challenging. With the availability of large annotated data (i.e. Stanford Natural Language Inference corpus), it has recently become feasible to train neural network based inference models, which have shown to be very effective. In Their paper, Unlike the previous top models that use very complicated network architectures, they first demonstrate that carefully designing sequential inference models based on chain LSTMs can outperform all previous models. Based on this, they further show that by explicitly considering recursive architectures in both local inference modeling and inference composition, they achieve additional improvement. Particularly, incorporating syntactic parsing information contributes to our best result—it further improves the performance even when added to the already very strong model.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P17-1152/">The paper: Enhanced LSTM for Natural Language Inference  Chen et al. 2017 AC</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Enhanced LSTM for Natural Language Inference.  Chen et al. 2017 arXiv](https://arxiv.org/abs/1609.06038)
  - [ACL 2017 version: Enhanced LSTM for Natural Language Inference.  Chen et al. 2017 ACL](https://www.aclweb.org/anthology/P17-1152/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    




























