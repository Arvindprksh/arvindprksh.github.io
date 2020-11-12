---
layout: post
title: Bidirectional Attention Flow for Machine Comprehension
subtitle: Title of paper - Bidirectional Attention Flow for Machine Comprehension
category: NLP papers - Machine Reading Comprehension
tags: [neural network, machine reading comprehension]
permalink: /2019/12/18/Bidirectional_Attention_Flow_for_Machine_Comprehension/
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

This is a brief summary of paper for me to study and organize it, [Bidirectional Attention Flow for Machine Comprehension. Seo et al. ICLR 2017](https://openreview.net/forum?id=HJ0UKP9ge) I read and studied. 
{% include MathJax.html %}


They propose the bidirectional attention flow, i.e. they separate the attention layer and modeling layer in contrary with dynamically learning the attention within modeling layer like the previous work ([Bahdanau et al. 2015 ICLR](https://arxiv.org/abs/1409.0473))

That is, they use similarity matrix (called affinity matrix in another way) to make Context-to-query attention and Query-to-Context attention.

And then they make query-aware representation of context words with the two attentions whichs serve as input of modeling layer for QA task.

The following is their multi-stage hierarchical model structure:

![Seo et al. ICLR 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/MRC/2019-12-18-Bidirectional_Attention_Flow_for_Machine_Comprehension/BIDAF_1.PNG)

For simple explanation of their model, 

Their machine comprehension model is a hierarchical multi-stage process and consists of six layers as you can see figure above.

1. Character Embedding Layer maps each word to a vector space using character-level CNNs.
2. Word Embedding Layer maps each word to a vector space using a pre-trained word embedding model.
3. Contextual Embedding Layer utilizes contextual cues from surrounding words to refine the embedding of the words. These first three layers are applied to both the query and context.
4. Attention Flow Layer couples the query and context vectors and produces a set of queryaware feature vectors for each word in the context.
5. Modeling Layer employs a Recurrent Neural Network to scan the context.
6. Output Layer provides an answer to the query.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Machine comprehension (MC), answering a query about a given context paragraph, requires modeling complex interactions between the context and the query. Recently, attention mechanisms have been successfully extended to MC. Typically these methods use attention to focus on a small portion of the context and summarize it with a fixed-size vector, couple attentions temporally, and/or often form a uni-directional attention. In this paper we introduce the Bi-Directional Attention Flow (BIDAF) network, a multi-stage hierarchical process that represents the context at different levels of granularity and uses bi-directional attention flow mechanism to obtain a query-aware context representation without early summarization.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://openreview.net/forum?id=HJ0UKP9ge">The paper: Bidirectional Attention Flow for Machine Comprehension. Seo et al. ICLR 2017</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: Bidirectional Attention Flow for Machine Comprehension. Seo et al. arXiv 2017](https://arxiv.org/abs/1611.01603)
  - [ICLR Version: Bidirectional Attention Flow for Machine Comprehension. Seo et al. ICLR 2017](https://openreview.net/forum?id=HJ0UKP9ge)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [publicly avaviable code of Bidirectional Attention Flow for Machine Comprehension. Seo et al. ICLR 2017](https://allenai.github.io/bi-att-flow/)
  - [Bidirectional Attention Flow for Machine Comprehension. Seo et al. ICLR 2017 on Papers With Code](https://paperswithcode.com/paper/bidirectional-attention-flow-for-machine)
  - [Neural Machine Translation by Jointly Learning to Align and Translate. Bahdanau et al. 2015 ICLR](https://arxiv.org/abs/1409.0473)
  - [What is the 1 D convolution on the StackExchange](https://stats.stackexchange.com/questions/292751/is-a-1d-convolution-of-size-m-with-k-channels-the-same-as-a-2d-convolution-o)
  - [What is the 1 D convolution on the Stackoverflow](https://stackoverflow.com/questions/42883547/intuitive-understanding-of-1d-2d-and-3d-convolutions-in-convolutional-neural-n)
  - [Introduction to 1D Convolutional Neural Networks in Keras for Time Sequences on goodaudience blog](https://blog.goodaudience.com/introduction-to-1d-convolutional-neural-networks-in-keras-for-time-sequences-3a7ff801a2cf)


























