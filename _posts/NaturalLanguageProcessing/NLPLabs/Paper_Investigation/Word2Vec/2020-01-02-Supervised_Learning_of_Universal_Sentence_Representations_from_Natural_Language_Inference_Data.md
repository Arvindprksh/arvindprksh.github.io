---
layout: post
title: Supervised Learning of Universal Sentence Representations from Natural Language Inference Data
subtitle: Title of paper - Supervised Learning of Universal Sentence Representations from Natural Language Inference Data
category: NLP papers - Sentence Embedding
tags: [neural network, sentence embedding]
permalink: /2020/01/02/Supervised_Learning_of_Universal_Sentence_Representations_from_Natural_Language_Inference_Data/
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

This is a brief summary of paper for me to study and organize it, [Supervised Learning of Universal Sentence Representations from Natural Language Inference Data. Conneau et al. EMNLP 2017](https://www.aclweb.org/anthology/D17-1070/) I read and studied. 
{% include MathJax.html %}

This paper propose the method to encode a sentence in a vector training on NLI task corpus.

In other words, they said the sentence vector from supervised data (NLI) contain semantic information of input sentence than other model trained on unsupervised corpus.

First of all, befoer diving into model to encode sentence in a vector, let's see the what NLI (natural language inference) task is :

![Conneau et al. EMNLP 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-01-02-Supervised_Learning_of_Universal_Sentence_Representations_from_Natural_Language_Inference_Data/NLI_Sentence_vector_1.PNG)

As you can see above, Models can be trained on SNLI in two different way

1) sentence encodeind-based model that explicitly separate the encoding of the indivisual sentences
2) joint methods that allow to use encoding of both sentences (to use cross-features or attention from one sentence ot the other)

They used a variety of models to generate sentence vector. 

First, Bi-LSTM max pooling network

![Conneau et al. EMNLP 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-01-02-Supervised_Learning_of_Universal_Sentence_Representations_from_Natural_Language_Inference_Data/NLI_Sentence_vector_2.PNG)

Second, inner attention network 

![Conneau et al. EMNLP 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-01-02-Supervised_Learning_of_Universal_Sentence_Representations_from_Natural_Language_Inference_Data/NLI_Sentence_vector_3.PNG)

Third, Hieraachical ConvNet architecture.

![Conneau et al. EMNLP 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-01-02-Supervised_Learning_of_Universal_Sentence_Representations_from_Natural_Language_Inference_Data/NLI_Sentence_vector_4.PNG)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Many modern NLP systems rely on word embeddings, previously trained in an unsupervised manner on large corpora, as base features. Efforts to obtain embeddings for larger chunks of text, such as sentences, have however not been so successful. Several attempts at learning unsupervised representations of sentences have not reached satisfactory enough performance to be widely adopted. In this paper, They show how universal sentence representations trained using the supervised data of the Stanford Natural Language Inference datasets can consistently outperform unsupervised methods like SkipThought vectors (Kiros et al., 2015) on a wide range of transfer tasks. Much like how computer vision uses ImageNet to obtain features, which can then be transferred to other tasks, our work tends to indicate the suitability of natural language inference for transfer learning to other NLP tasks.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/D17-1070/">The paper: Supervised Learning of Universal Sentence Representations from Natural Language Inference Data. Conneau et al. EMNLP 2017</a>
</div>

# Reference 

- Paper 
  - [arXiv version: Supervised Learning of Universal Sentence Representations from Natural Language Inference Data. Conneau et al. arXiv 2018](https://arxiv.org/abs/1705.02364)
  - [EMNLP 2017 version: Supervised Learning of Universal Sentence Representations from Natural Language Inference Data. Conneau et al. EMNLP 2017](https://www.aclweb.org/anthology/D17-1070/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    






























