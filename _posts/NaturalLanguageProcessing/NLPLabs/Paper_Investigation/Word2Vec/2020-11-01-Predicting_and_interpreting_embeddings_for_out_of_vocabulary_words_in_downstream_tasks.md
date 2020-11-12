---
layout: post
title: Predicting and interpreting embeddings for out of vocabulary words in downstream tasks. Garneau et al. EMNLP-WS. 2018.
subtitle: Title of paper - Predicting and interpreting embeddings for out of vocabulary words in downstream tasks. Garneau et al. EMNLP-WS. 2018.
category: NLP papers - OOV Embedding
tags: [OOV Embedding]
permalink: /2020/11/01/Predicting_and_interpreting_embeddings_for_out_of_vocabulary_words_in_downstream_tasks/
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

This is a brief summary of paper for me to study and organize it, [Predicting and interpreting embeddings for out of vocabulary words in downstream tasks. Garneau et al. EMNLP 2018](https://www.aclweb.org/anthology/W18-5439/) I read and studied. 
{% include MathJax.html %}

This paper focus on handling the OOV words for downstream task. 

OOV(out-of-vocabulary) words make NLP tasks underestimated but due to the lack of proper way to handle OOV words. 

Most researches often resort to simple assign random embedding sto unknown words or to map them to a unique "unknown" embedding, nevertheless hoping their model will generalize well.

For their an OOV predictions module, First the left context, right context and word characters are fed to three bi-LSTM to produce seperate encodings. 

These three hidden states are then passed to a linear layer on which a softmax is applied to determine their relative importance (i.e. their degree of attention). 

The output of this layer is then used to produce a weighted sum of the hidden states. Finally, a simple layer compoute an embedding from this sum.

If you want to know the result of their experiment, refer to [Predicting and interpreting embeddings for out of vocabulary words in downstream tasks. Garneau et al. EMNLP 2018](https://www.aclweb.org/anthology/W18-5439/)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They propose a novel way to handle out of vocabulary (OOV) words in downstream natural language processing (NLP) tasks. They implement a network that predicts useful embeddings for OOV words based on their morphology and on the context in which they appear. Their model also incorporates an attention mechanism indicating the focus allocated to the left context words, the right context words or the word’s characters, hence making the prediction more interpretable. The model is a “drop-in” module that is jointly trained with the downstream task’s neural network, thus producing embeddings specialized for the task at hand. When the task is mostly syntactical, they observe that our model aims most of its attention on surface form characters. On the other hand, for tasks more semantical, the network allocates more attention to the surrounding words. In all their tests, the module helps the network to achieve better performances in comparison to the use of simple random embeddings.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/W18-5439/">The paper: Predicting and interpreting embeddings for out of vocabulary words in downstream tasks. Garneau et al. EMNLP 2018</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Predicting and interpreting embeddings for out of vocabulary words in downstream tasks. Garneau et al. arXiv 2019](https://arxiv.org/abs/1903.00724)
  - [EMNLP 2018 version: Predicting and interpreting embeddings for out of vocabulary words in downstream tasks. Garneau et al. EMNLP-WS 2018](https://www.aclweb.org/anthology/W18-5439/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


