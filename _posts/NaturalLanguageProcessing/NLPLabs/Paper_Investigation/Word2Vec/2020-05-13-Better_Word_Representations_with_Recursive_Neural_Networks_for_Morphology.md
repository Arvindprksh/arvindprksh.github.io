---
layout: post
title: Better Word Representations with Recursive Neural Networks for Morphology
subtitle: Title of paper - Better Word Representations with Recursive Neural Networks for Morphology
category: NLP papers - Word Embedding
tags: [neural network, word embedding, morpheme embedding]
permalink: /2020/05/13/Better_Word_Representations_with_Recursive_Neural_Networks_for_Morphology/
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

This is a brief summary of paper for me to study and arrange it, [2020-05-13-Better_Word_Representations_with_Recursive_Neural_Networks_for_Morphology. Luong et al. CoNLL 2013](https://www.aclweb.org/anthology/W13-3512/) I read and studied. 
{% include MathJax.html %}

They said that The existing methods treat each full-form word as indentity entity adn fail to capture the explicit relationship among morphologidcal variants of a word.

These models have no capability of building representations for ansy new unseen word comprised of known morphemes. 

Therefore, they propose Recursive Neural Network as compostional function form morphemes to a word.

In orther words, this model focuses on contructing word vector from its morphemes without the context information which used for the distributed representataion of the word.

The context-insensitive morphological RNN

![Luong et al. CoNLL 2013](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-05-13-Better_Word_Representations_with_Recursive_Neural_Networks_for_Morphology/MRNN.PNG)

The following based on ngram neural language model has two layer. The first is to construct word embedding from its morphemes and the second is n gram neural network with ranking-type cost function.

The context-sensitive morphological RNN below separates morphemes(stem + affix) and word which is the minimum meaning-bearing unit. 

![Luong et al. CoNLL 2013](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-05-13-Better_Word_Representations_with_Recursive_Neural_Networks_for_Morphology/CMRNN.PNG)

They train the models above with ranking-type cost function to minimize in defining their objective funtion as below:

$$J(\theta) = \sum_{i=1}^N max\{0, 1 - s(n_i) + s(\bar n_i)\}$$

Here, N is the number of all avaliable ngrams in the training corpus, whereas \\(\bar n_i\\) is a **corrected** ngram created from $n_i$ by replacing its last word with a random word. 


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Vector-space word representations have been very successful in recent years at improving performance across a variety of NLP tasks. However, common to most existing work, words are regarded as independent entities without any explicit relationship among morphologically related words being modeled. As a result, rare and complex words are often poorly estimated, and all unknown words are represented in a rather crude way using only one or a few vectors. This paper addresses this shortcoming by proposing a novel model that is capable of building representations for morphologically complex words from their morphemes. They combine recursive neural networks (RNNs), where each morpheme is a basic unit, with neural language models (NLMs) to consider contextual information in learning morphologicallyaware word representations. 
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/W13-3512/">The paper: 2020-05-13-Better_Word_Representations_with_Recursive_Neural_Networks_for_Morphology. Luong et al. CoNLL 2013</a>
</div>

# Reference 

- Paper 
  - [CoNLL  2013 Ver: 2020-05-13-Better_Word_Representations_with_Recursive_Neural_Networks_for_Morphology. Luong et al. CoNLL 2013](https://www.aclweb.org/anthology/W13-3512/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    






























