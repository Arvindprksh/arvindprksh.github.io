---
layout: post
title: context2vec- Learning Generic Context Embedding with Bidirectional LSTM
subtitle: Title of paper - context2vec- Learning Generic Context Embedding with Bidirectional LSTM
category: NLP papers - Transfer_learning
tags: [neural_network, Context_Embedding]
permalink: /2019/11/25/Context2Vec_Learning_Learning_Generic_Context_Embedding_with_Bidirectional_LSTM/
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

This is a brief summary of paper for me to study and organize it, [context2vec: Learning Generic Context Embedding with Bidirectional LSTM Melamud et al. 2016 SIGNLL](https://www.aclweb.org/anthology/K16-1006/) I read and studied. 
{% include MathJax.html %}

This paper shows how to embed sentential context into a fixed-length vector with Bidirectional LSTM. 

As you can see the figure below, They used a Bidirectional LSTM, feeding one LSTM network with the sentence from left to right, and aother from right to left. The parameter of these two networks are completlely separate, including two separate sets fo left-to-right and right-to-left context word embedding. 

So as to represent sentential context to a embedding, they concatenate each context vectors from left to right ant from right to left as shown in figure1 b.   

Objective function is how likely the target word vector and sentential context vector is to a pair based on the CBOW method. They used negative sampling technique.

In their embedding, they used two special tokens, BOS and EOS signified as the end and beginning of a sentence.

![Melamud et al. 2016 SIGNLL](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Contextual_Embedding/2019-11-25-Context2Vec_Learning_Learning_Generic_Context_Embedding_with_Bidirectional_LSTM/context2_vec.PNG)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Context representations are central to various NLP tasks, such as word sense disambiguation, named entity recognition, coreference resolution, and many more. In this work they present a neural model for efficiently learning a generic context embedding function from large corpora, using bidirectional LSTM. With a very simple application of their context representations, they manage to surpass or nearly reach state-of-the-art results on sentence completion, lexical substitution and word
sense disambiguation tasks. They release their [code and pretrained models](http://u.cs.biu.ac.il/~nlp/resources/downloads/context2vec/), suggesting their method could be useful in a wide variety of NLP tasks.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/K16-1006/">The paper: context2vec- Learning Generic Context Embedding with Bidirectional LSTM Melamud et al. 2016 SIGNLL</a>
</div>

# Reference 

- Paper 
  - [ACL 2016 version: context2vec- Learning Generic Context Embedding with Bidirectional LSTM. Melamud et al. 2016 SIGNLL](https://www.aclweb.org/anthology/K16-1006/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
































