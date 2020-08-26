---
layout: post
title: Neural Summarization by Extracting Sentences and Words
subtitle: Title of paper - Neural Summarization by Extracting Sentences and Words
category: NLP papers - Summarization
tags: [neural network, extractive summarization]
permalink: /2020/08/26/Neural_Summarization_by_Extracting_Sentences_and_Words/
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

This is a brief summary of paper for me to study and organize it, [Neural Summarization by Extracting Sentences and Words. Cheng and Lapata. ACL 2016](https://www.aclweb.org/anthology/P16-1046/) I read and studied. 
{% include MathJax.html %}

This paper proposed an extractive summarization method based on neuaral networks.

The extractive unit is two types, one is the sentence and the other is word.

For sentence, extractive summarization method select sentences in a document as summary. 

Normally, research of it was consider sequence labeling task to choose sentences in a document 

Let's see an example data 

![Cheng and Lapata. ACL 2016](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Summarization/2020-08-26-Neural_Summarization_by_Extracting_Sentences_and_Words/example_data.PNG)

First of all, sentence extractor is as following:

![Cheng and Lapata. ACL 2016](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Summarization/2020-08-26-Neural_Summarization_by_Extracting_Sentences_and_Words/Sentence_extractor.PNG)

Finally, Word extractor,which is the extracted unit change from sentence to word , is as following:

![Cheng and Lapata. ACL 2016](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Summarization/2020-08-26-Neural_Summarization_by_Extracting_Sentences_and_Words/Word_extractor.PNG)

on evaluation, they used ROUGE-1,2 as means of assessing informativeness and the longest common subsequences(ROUGE-L) as a means of assessing fluency.


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Traditional approaches to extractive summarization rely heavily on humanengineered features. In this work they propose a data-driven approach based on neural networks and continuous sentence features. They develop a general framework for single-document summarization composed of a hierarchical document encoder and an attention-based extractor. This architecture allows them to develop different classes of summarization models which can extract sentences or words. 
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P16-1046/">The paper: Neural Summarization by Extracting Sentences and Words. Cheng and Lapata. ACL 2016</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Neural Summarization by Extracting Sentences and Words.  Cheng and Lapata. Arxiv 2016](https://arxiv.org/abs/1603.07252)
  - [ACL 2016 version: Neural Summarization by Extracting Sentences and Words. Cheng and Lapata. ACL 2016](https://www.aclweb.org/anthology/P16-1046/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
- For information 
  - [Towards Automatic Text Summarization: Extractive Methods on medium](https://medium.com/sciforce/towards-automatic-text-summarization-extractive-methods-e8439cd54715)
  - [Automatic Text Summarization with Machine Learning — An overview on medium](https://medium.com/luisfredgs/automatic-text-summarization-with-machine-learning-an-overview-68ded5717a25)
  - [Deep Learning Models for Automatic Summarization on toward data science](https://towardsdatascience.com/deep-learning-models-for-automatic-summarization-4c2b89f2a9ea)
    


