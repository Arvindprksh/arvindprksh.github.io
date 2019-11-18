---
layout: post
title: Siamese Recurrent Architectures for Learning Sentence Similarity
subtitle: Title of paper - Siamese Recurrent Architectures for Learning Sentence Similarity
category: NLP papers - Text_similarity
tags: [neural_network, setence_similarity]
permalink: /2019/11/18/Siamese_Recurrent_Architectures_for_Learning_Sentence_Similarity/
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

This is a brief summary of paper for me to study and organize it, [Siamese Recurrent Architectures for Learning Sentence Similarity (Mueller and Thyagarajan. AAAI 2016)](https://www.aaai.org/ocs/index.php/AAAI/AAAI16/paper/viewPaper/12195) I read and studied. 
{% include MathJax.html %}

Thes propose a siamese neural network based on LSTM to compare a pair of sentences.

First, they encode two sentence of different length into fixed-size vectors using an LSTM as follows:

![Mueller and Thyagarajan. AAAI 2016](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Similarity/2019-11-18-Siamese_Recurrent_Architectures_for_Learning_Sentence_Similarity/Siamese_LSTM_neural_network.PNG)

As you can see, they used Manhattan distance as objective function.

In their paper, they use data augmentation for NLP(natural language processing) called synonym augmentation.

synonym augmentation replace random words with one of their synonyms, for example, using Wordnet. 

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They present a siamese adaptation of the Long Short-Term Memory (LSTM) network for labeled data comprised of pairs of variable-length sequences. Their model is applied to assess semantic similarity between sentences, where we exceed state of the art, outperforming carefully handcrafted features and recently proposed neural network systems of greater complexity. For these applications, They provide wordembedding vectors supplemented with synonymic information to the LSTMs, which use a fixed size vector to encode the underlying meaning expressed in a sentence (irrespective of the particular wording/syntax). By restricting subsequent operations to rely on a simple Manhattan metric, we compel the sentence representations learned by our model to form a highly structured space whose geometry reflects complex semantic relationships.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aaai.org/ocs/index.php/AAAI/AAAI16/paper/viewPaper/12195">The paper: Siamese Recurrent Architectures for Learning Sentence Similarity (Mueller and Thyagarajan. AAAI 2016)</a>
</div>

# Reference 

- Paper 
  - [AAAI 2019 version: Siamese Recurrent Architectures for Learning Sentence Similarity (Mueller and Thyagarajan. AAAI 2016)](https://www.aaai.org/ocs/index.php/AAAI/AAAI16/paper/viewPaper/12195)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)































