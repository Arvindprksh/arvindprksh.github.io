---
layout: post
title: Universal Neural Machine Translation for Extremely Low Resource Languages
subtitle: Title of paper - Universal Neural Machine Translation for Extremely Low Resource Languages
category: NLP papers - Translation
tags: [translation]
permalink: /2020/06/17/Universal_Neural_Machine_Translation_for_Extremely_Low_Resource_Languages/
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

This is a brief summary of paper for me to note it, [Universal Neural Machine Translation for Extremely Low Resource Languages. Gu et al. NAACL 2018](https://www.aclweb.org/anthology/N18-1032/)

{% include MathJax.html %}


They proposed the model which is useful at low-resource language pair in machine translation.

Auxiliary languages are used to extracter universal token embedding and sentence embeddding.

To sum up, they approach utilizes multi-lingual neural translation system to share lexical and sentence level representations across multiple source languages into one target language:

![Gu et al. NAACL 2018](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2020-06-17-Universal_Neural_Machine_Translation_for_Extremely_Low_Resource_Languages/ULR_and_MoLE_architecture.PNG)

In figure above, the part shaded is learned for NMT training process. 

Their model has two key points.

(1) Lexical-level Sharing 

Conventionally, a multilingual NMT model has a vocabulary that represents the union of the vocabularies of all source languages. Therefore, the multi-lingual words do not practically share the same embedding space since each word has its own representation. This does not pose a problem for languages with sufficiently large amount of data, yet it is a major limitation for extremely low resource languages since most of the vocabulary items will not have enough, if any, training examples to get a reliably trained models.

A possible solution is to share the surface form of all source languages through sharing sub-units such as subwords or characters.  However, for an arbitrary lowresource language we cannot assume significant overlap in the lexical surface forms compared to the high-resource languages. The low-resource language may not even share the same character set as any high-resource language. It is crucial to create a shared semantic representation across all languages that does not rely on surface form overlap.

(2) Sentence-level Sharing

It is also crucial for lowresource languages to share source sentence representation with other similar languages. For example, if a language shares syntactic order with another language it should be feasible for the lowresource language to share such representation with another high recourse language. It is also important to utilize monolingual data to learn such representation since the low or zero resource language may have monolingual resources only.

They aslo showed that it is more reasonable to have similar languages as auxiliary languages. 

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
In this paper, they propose a new universal machine translation approach focusing on languages with a limited amount of parallel data. Their proposed approach utilizes a transfer-learning approach to share lexical and sentence level representations across multiple source languages into one target language. The lexical part is shared through a Universal Lexical Representation to support multilingual word-level sharing. The sentencelevel sharing is represented by a model of experts from all source languages that share the source encoders with all other languages. This enables the low-resource language to utilize the lexical and sentence representations of the higher resource languages.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/N18-1032/">The paper: Universal Neural Machine Translation for Extremely Low Resource Languages. Gu et al. NAACL 2018</a>
</div>

# Reference 

- Paper 
  - [ArXiv version: Universal Neural Machine Translation for Extremely Low Resource Languages. Gu et al. ArXiv 2018](https://arxiv.org/abs/1802.05368)
  - [NAACL version: Universal Neural Machine Translation for Extremely Low Resource Languages. Gu et al. NAACL 2018](https://www.aclweb.org/anthology/N18-1032/)
  
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
