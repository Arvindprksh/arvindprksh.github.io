---
layout: post
title: Massively Multilingual Sentence Embeddings for Zero-Shot Cross-Lingual Transfer and Beyond
subtitle: Title of paper - Massively Multilingual Sentence Embeddings for Zero-Shot Cross-Lingual Transfer and Beyond
category: NLP papers - Cross-lingual Sentence Embedding
tags: [cross_lingual_sentence_embedding]
permalink: /2020/06/16/Massively_Multilingual_Sentence_Embeddings_or_Zero-Shot_Cross-Lingual_Transfer_and_Beyond/
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

This is a brief summary of paper for me to study and arrange for [Massively Multilingual Sentence Embeddings for Zero-Shot Cross-Lingual Transfer and Beyond. (Artetxe and Schwenk., arXiv 2019)](https://arxiv.org/abs/1812.10464) I read and studied. 
{% include MathJax.html %}

This paper propose sentence embedding by using a BiLSTM encoder sharing a large number of languages as follows:

The interesting point they used is byte-pair encoding vocabulary with 50K operations, which is learned on the concatenation of all training corpora.

![Artetxe and Schwenk., 2019 ArXiv](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Cross_lingual_embedding/2020-06-16-Massively_Multilingual_Sentence_Embeddings_or_Zero-Shot_Cross-Lingual_Transfer_and_Beyond/sentence_embedding_for_cross_embedding.PNG)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They introduce an architecture to learn joint multilingual sentence representations for 93 languages, belonging to more than 30 different families and written in 28 different scripts. Their system uses a single BiLSTM encoder with a shared BPE vocabulary for all languages, which is coupled with an auxiliary decoder and trained on publicly available parallel corpora. This enables us to learn a classifier on top of the resulting embeddings using English annotated data only, and transfer it to any of the 93 languages without any modification. Their experiments in cross-lingual natural language inference (XNLI dataset), cross-lingual document classification (MLDoc dataset) and parallel corpus mining (BUCC dataset) show the effectiveness of their approach. They also introduce a new test set of aligned sentences in 112 languages, and show that our sentence embeddings obtain strong results in multilingual similarity search even for low-resource languages. Their implementation, the pretrained encoder and the multilingual test set are available at https://github.com/facebookresearch/LASER.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1812.10464">The paper: Massively Multilingual Sentence Embeddings for Zero-Shot Cross-Lingual Transfer and Beyond (Artetxe and Schwenk., arXiv 2019)</a>
</div>

# Reference 

- Paper 
   - [arXiv Version: Massively Multilingual Sentence Embeddings for Zero-Shot Cross-Lingual Transfer and Beyond (Artetxe and Schwenk., arXiv 2019)](https://arxiv.org/abs/1812.10464)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    




























