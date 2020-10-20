---
layout: post
title: Multilingual Part-of-Speech Tagging with Bidirectional Long Short-Term Memory Models and Auxiliary Loss
subtitle: Title of paper - Multilingual Part-of-Speech Tagging with Bidirectional Long Short-Term Memory Models and Auxiliary Loss
category: NLP papers - Tagging
tags: [tagging]
permalink: /2020/10/15/Multilingual_Part-of-Speech_Tagging_with_Bidirectional_Long_Short-Term_Memory_Models_and_Auxiliary_Loss/
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

This is a brief summary of paper for me to study and organize it, [Multilingual Part-of-Speech Tagging with Bidirectional Long Short-Term Memory Models and Auxiliary Loss. Plank et al. ACL 2016](https://www.aclweb.org/anthology/P16-2067/) I read and studied. 
{% include MathJax.html %}


They performed the experiment on POS tagging with multiple languages. 

They used character embedding and byte embedding to handle rare words as follows:

![Plank et al. ACL 2016](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-10-15-Multilingual_Part-of-Speech_Tagging_with_Bidirectional_Long_Short-Term_Memory_Models_and_Auxiliary_Loss/pos_bi_lstm_wih_fre.PNG)

on their model, they train the bi-LSTM tagger to predict both the tags of the sequence, as well as a label that represents the log frequency of the next token as estimated from the training data

**log frequency label : \\(int(log(fre_{train}(w)))\\)**

They measured the performance with respect to label noise, data size, and rare word. 

The result showed

- For rare word, the rare token benefits from sub-token representation
- For data size, the bi-LSTM model is better with more data but the TNT, based on a second order HHM, is better with little data. The bi-LSTM model always wins over CRF.
- For label noise, bi-LSTMs are less robust, showing higher drops in accuracy compared to TNT.


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Bidirectional long short-term memory (biLSTM) networks have recently proven successful for various NLP sequence modeling tasks, but little is known about their reliance to input representations, target languages, data set size, and label noise. They address these issues and evaluate bi-LSTMs with word, character, and unicode byte embeddings for POS tagging. They compare bi-LSTMs to traditional POS taggers across languages and data sizes. They also present a novel biLSTM model, which combines the POS tagging loss function with an auxiliary loss function that accounts for rare words. The model obtains state-of-the-art performance across 22 languages, and works especially well for morphologically complex languages. Their analysis suggests that biLSTMs are less sensitive to training data size and label corruptions (at small noise levels) than previously assumed.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P16-2067/">The paper: Multilingual Part-of-Speech Tagging with Bidirectional Long Short-Term Memory Models and Auxiliary Loss. Plank et al. ACL 2016</a>
</div>

# Reference 

- Paper 
   - [Arxiv 2016 version: Multilingual Part-of-Speech Tagging with Bidirectional Long Short-Term Memory Models and Auxiliary Loss. Plank et al. arXiv 2016](https://arxiv.org/abs/1604.05529)
   - [ACL 2016 version: Multilingual Part-of-Speech Tagging with Bidirectional Long Short-Term Memory Models and Auxiliary Loss. Plank et al. ACL 2016](https://www.aclweb.org/anthology/P16-2067/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


