---
layout: post
title: Neural Machine Translation of Rare Words with Subword Units
subtitle: Title of paper - Neural Machine Translation of Rare Words with Subword Units
category: NLP papers - Translation
tags: [translation]
permalink: /2020/06/23/Neural_Machine_Translation_of_Rare_Words_with_Subword_Units/
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

This is a brief summary of paper for me to study and organize it, [Neural Machine Translation of Rare Words with Subword Units. Sennrich et al. ACL 2016](https://www.aclweb.org/anthology/P16-1162/) I read and studied. 
{% include MathJax.html %}

This paper introduce the subword unit into Neural Machine translation task to well handle rare or unseen words. 

In order to generate segmentation to subword units, they used an algorithm, also known as compressiont algorithm, byte-pair encoding.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Neural machine translation (NMT) models typically operate with a fixed vocabulary, but translation is an open-vocabulary problem. Previous work addresses the translation of out-of-vocabulary words by backing off to a dictionary. In this paper, they introduce a simpler and more effective approach, making the NMT model capable of open-vocabulary translation by encoding rare and unknown words as sequences of subword units. This is based on the intuition that various word classes are translatable via smaller units than words, for instance names (via character copying or transliteration), compounds (via compositional translation), and cognates and loanwords (via phonological and morphological transformations). They discuss the suitability of different word segmentation techniques, including simple character ngram models and a segmentation based on the byte pair encoding compression algorithm, and empirically show that subword models improve over a back-off dictionary baseline for the WMT 15 translation tasks English→German and English→Russian by up to 1.1 and 1.3 BLEU, respectively.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P16-1162/">The paper: Neural Machine Translation of Rare Words with Subword Units. Sennrich et al. ACL 2016</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Neural Machine Translation of Rare Words with Subword Units. Sennrich et al. arXiv 2016](https://arxiv.org/abs/1508.07909)
  - [ACL 2016 version: Neural Machine Translation of Rare Words with Subword Units. Sennrich et al. ACL 2016](https://www.aclweb.org/anthology/P16-1162/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


