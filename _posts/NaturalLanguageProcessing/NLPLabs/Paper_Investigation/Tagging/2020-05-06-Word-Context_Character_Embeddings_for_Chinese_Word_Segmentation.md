---
layout: post
title: Word-Context Character Embeddings for Chinese Word Segmentation
subtitle: Title of paper - Word-Context Character Embeddings for Chinese Word Segmentation
category: NLP papers - Tagging
tags: [tagging]
permalink: /2020/05/06/Word-Context_Character_Embeddings_for_Chinese_Word_Segmentation/
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

This is a brief summary of paper for me to study and arrange for [Word-Context Character Embeddings for Chinese Word Segmentation. Zhou et al. EMNLP 2017](https://www.aclweb.org/anthology/D17-1079/) I read and studied. 
{% include MathJax.html %}

This paper is a research ralted to chinese segmenataion for cross domain. 

**They also used label embedding to use segmentation label information in the pre-training of character embedding**

The model below is the baseline for Chinese Word segmenatation task they used.

![Zhou et al. EMNLP 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-05-06-Word-Context_Character_Embeddings_for_Chinese_Word_Segmentation/word-context_characte_embedding.PNG)

They are inspired by skip-gram embedding model for pre-trainig of word-context character embedding.

Like image below, in order to train word-context character embedding, they used the context of character with the window size c, together with their corresponding segment labels. 

![Zhou et al. EMNLP 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-05-06-Word-Context_Character_Embeddings_for_Chinese_Word_Segmentation/word_context.PNG)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Neural parsers have benefited from automatically labeled data via dependencycontext word embeddings. They investigate training character embeddings on a word-based context in a similar way.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/D17-1079/">The paper: Word-Context Character Embeddings for Chinese Word Segmentation. Zhou et al. EMNLP 2017</a>
</div>

# Reference 

- Paper 
  - [EMNLP version: Word-Context Character Embeddings for Chinese Word Segmentation. Zhou et al. EMNLP 2017](https://www.aclweb.org/anthology/D17-1079/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    




























