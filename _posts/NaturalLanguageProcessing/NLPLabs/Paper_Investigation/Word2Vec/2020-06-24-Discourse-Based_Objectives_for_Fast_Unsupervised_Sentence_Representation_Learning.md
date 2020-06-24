---
layout: post
title: Discourse-Based Objectives for Fast Unsupervised Sentence Representation Learning
subtitle: Title of paper - Discourse-Based Objectives for Fast Unsupervised Sentence Representation Learning
category: NLP papers - Sentence Embedding
tags: [neural network, sentence embedding]
permalink: /22020/06/24/Discourse-Based_Objectives_for_Fast_Unsupervised_Sentence_Representation_Learning/
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

This is a brief summary of paper for me to study and arrange it, [Discourse-Based Objectives for Fast Unsupervised Sentence Representation Learning. Jernite et al. 2017](https://arxiv.org/abs/1705.00557) I read and studied. 
{% include MathJax.html %}

This paper proposed three objective to traing unlabeled text data as self-supervised learning. 

The basis of their method is coherence relation in discourse as follows:

![Jernite et al. 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-06-24-Discourse-Based_Objectives_for_Fast_Unsupervised_Sentence_Representation_Learning/discourse_coherence.PNG)


- Binary Ordering of Sentences 
>> Many coherence relations have an inherent direction. For example, if S1 is an elaboration of S0, S0 is not generally an elaboration of S1. Thus, being able to identify these coherence relations implies an ability to recover the original order of the sentences. Our first task, which we call ORDER, consists in taking pairs of adjacent sentences from text data, switching their order with probability 0.5, and training a model to decide whether they have been switched. It should be noted that since some of these relations are unordered, it is not always possible to recover the original order based on discourse coherence alone  


![Jernite et al. 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-06-24-Discourse-Based_Objectives_for_Fast_Unsupervised_Sentence_Representation_Learning/order.PNG)

- Next Sentence
>> Many coherence relations are transitive by nature, so that any two sentences from the same paragraph will exhibit some coherence. However, two adjacent sentences will generally be more coherent than two more distant ones. This leads us to formulate the NEXT task: given the first three sentences of a paragraph and a set of five candidate sentences from later in the paragraph, the model must decide which candidate immediately follows the initial three in the source text.   


![Jernite et al. 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-06-24-Discourse-Based_Objectives_for_Fast_Unsupervised_Sentence_Representation_Learning/next.PNG)

- Conjunction Prediction
>> Finally, information about the coherence relation between two sentences is sometimes apparent in the text: this is the case whenever the second sentence starts with a conjunction phrase.  

![Jernite et al. 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-06-24-Discourse-Based_Objectives_for_Fast_Unsupervised_Sentence_Representation_Learning/conjunction.PNG)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
This work presents a novel objective function for the unsupervised training of neural network sentence encoders. It exploits signals from paragraph-level discourse coherence to train these models to understand text. Our objective is purely discriminative, allowing us to train models many times faster than was possible under prior methods, and it yields models which perform well in extrinsic evaluations.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1705.00557">The paper: Discourse-Based Objectives for Fast Unsupervised Sentence Representation Learning. Jernite et al. 2017</a>
</div>

# Reference 

- Paper 
  - [arXiv version: Discourse-Based Objectives for Fast Unsupervised Sentence Representation Learning. Jernite et al. 2017](https://arxiv.org/abs/1705.00557)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    






























