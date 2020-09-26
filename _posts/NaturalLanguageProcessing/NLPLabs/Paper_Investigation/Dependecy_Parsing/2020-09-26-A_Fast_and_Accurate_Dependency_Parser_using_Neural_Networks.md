---
layout: post
title: A Fast and Accurate Dependency Parser using Neural Networks
subtitle: Title of paper - A Fast and Accurate Dependency Parser using Neural Networks
category: NLP papers - Dependency Parsing
tags: [dependency parsing]
permalink: /2020/09/26/A_Fast_and_Accurate_Dependency_Parser_using_Neural_Networks/
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

This is a brief summary of paper for me to study and organize it, [A Fast and Accurate Dependency Parser using Neural Networks. Chen and Manning. EMNLP 2014](https://www.aclweb.org/anthology/D14-1082/) I read and studied. 
{% include MathJax.html %}

This paper propose the model based on neural network for dependecy parsing task in NLP.

They address the problem that feature is sparsness and depends on expertise for developer for depedency parsing task or something in NLP. 

Especially back then using property that low-dimensional, dense word embedding can effectively alleviate sparsity by sharing statistical strength between similar wors, and can provide them a good starting poit to construct features of words and their interactions.


![Chen and Manning. EMNLP 2014](img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Dependecy_Parsing/2020-09-26-A_Fast_and_Accurate_Dependency_Parser_using_Neural_Networks/transition_based_dependency_parsing_architecture.PNG)


They propose the denpendecy parsing system with transition-based arc-standard, briefly saying how for the arc-standard-based transition-based dependency parsing to work.

![Chen and Manning. EMNLP 2014](img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Dependecy_Parsing/2020-09-26-A_Fast_and_Accurate_Dependency_Parser_using_Neural_Networks/transition_based_dependency_parsing.PNG)


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Almost all current dependency parsers classify based on millions of sparse indicator features. Not only do these features generalize poorly, but the cost of feature computation restricts parsing speed significantly. In this work, they propose a novel way of learning a neural network classifier for use in a greedy, transition-based dependency parser. Because this classifier learns and uses just a small number of dense features, it can work very fast, while achieving an about 2% improvement in unlabeled and labeled attachment scores on both English and Chinese datasets. Concretely, our parser is able to parse more than 1000 sentences per second at 92.2% unlabeled attachment score on the English Penn Treebank.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P16-1009/">The paper: Improving Neural Machine Translation Models with Monolingual Data. Sennrich et al. ACL 2016</a>
</div>

# Reference 

- Paper 
  - [EMNLP 2014 version: A Fast and Accurate Dependency Parser using Neural Networks. Chen and Manning. EMNLP 2014](https://www.aclweb.org/anthology/D14-1082/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


