---
layout: post
title: Character-based Bidirectional LSTM-CRF with words and characters for Japanese Named Entity Recognition
subtitle: Title of paper - Character-based Bidirectional LSTM-CRF with words and characters for Japanese Named Entity Recognition
category: NLP papers - Tagging
tags: [tagging]
permalink: /2020/05/25/Character-based_Bidirectional_LSTM-CRF_with_words_and_characters_for_Japanese_Named_Entity_Recognition/
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

This is a brief summary of paper for me to study and arrange for [Character-based Bidirectional LSTM-CRF with words and characters for Japanese Named Entity Recognition. Misawa et al. SCLeM 2017](https://www.aclweb.org/anthology/W17-4114/) I read and studied. 
{% include MathJax.html %}

This paper is a research ralted to Japanese NER task applying, back then, the cutting-edge model to Japanese.

Most of neural network focused on English, So they verified neural network worked well on Japanese comparing to the conventional method of Japanese NER task.

Also while the CNN layer help performance of NER taks achieve hier performance becuase CNN can capture sub-information of a word which is capitalization, suffixes, and prefixes. 

But They said the CNN has a problem in extracting sub-information in Japanese.

The reason is Japanese words tend to be shorter than English and Japanese character has no capitalization.

And They Japanese has boundary conflict problem when a part of a word compose an entity. So they finally argue the chacater-based than word-based model.

They propose character-based model to predict a tag for a character with word embeddign as follows:

![Misawa et al. SCLeM 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-05-25-Character-based_Bidirectional_LSTM-CRF_with_words_and_characters_for_Japanese_Named_Entity_Recognition/)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Recently, neural models have shown superior performance over conventional models in NER tasks. These models use CNN to extract sub-word information along with RNN to predict a tag for each word. However, these models have been tested almost entirely on English texts. It remains unclear whether they perform similarly in other languages. They worked on Japanese NER using neural models and discovered two obstacles of the state-of-the-art model. First, CNN is unsuitable for extracting Japanese sub-word information. Secondly, a model predicting a tag for each word cannot extract an entity when a part of a word composes an entity. The contributions of this work are (1) verifying the effectiveness of the state-of-the-art NER model for Japanese, (2) proposing a neural model for predicting a tag for each character using word and character information.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/W17-4114/">The paper: Character-based Bidirectional LSTM-CRF with words and characters for Japanese Named Entity Recognition. Misawa et al. SCLeM 2017</a>
</div>

# Reference 

- Paper 
  - [SCLeM 2017 version: Character-based Bidirectional LSTM-CRF with words and characters for Japanese Named Entity Recognition. Misawa et al. SCLeM 2017](https://www.aclweb.org/anthology/W17-4114/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    




























