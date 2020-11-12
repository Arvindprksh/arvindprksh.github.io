---
layout: post
title: Contextual String Embeddings for Sequence Labeling
subtitle: Title of paper - Contextual String Embeddings for Sequence Labeling
category: NLP papers - Tagging
tags: [tagging]
permalink: /2020/05/28/Contextual_String_Embeddings_for_Sequence_Labeling/
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

This is a brief summary of paper for me to study and arrange for [Contextual String Embeddings for Sequence Labeling. Akbik et al. COLING 2018](https://www.aclweb.org/anthology/C18-1139/) I read and studied. 
{% include MathJax.html %}

They propose the pre-training model to language model, most of research train language model based on word level. 

However, they train the model language model dealing with a sentence as a character sequence. 

They propose a novel type of contextualized characterlevel word embedding which they hypothesize to combine the best attributes of the embeddings; namely, the ability to (1) pre-train on large unlabeled corpora, (2) capture word meaning in context and therefore produce different embeddings for polysemous words depending on their usage, and (3) model words and context fundamentally as sequences of characters, to both better handle rare and misspelled words as well as model subword structures such as prefixes and endings.

To sum up , they present a method to generate such a contextualized embedding for any string of characters in a sentential context, and thus refer to the proposed representations as contextual string embeddings as follows:

![Akbik et al. COLING 2018](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-05-28-Contextual_String_Embeddings_for_Sequence_Labeling/contextualized_string_embedding_1.PNG)

The following show they extracter wored embedding from character sequence language model. 

![Akbik et al. COLING 2018](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tagging/2020-05-28-Contextual_String_Embeddings_for_Sequence_Labeling/contextualized_string_embedding_2.PNG)


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Recent advances in language modeling using recurrent neural networks have made it viable to model language as distributions over characters. By learning to predict the next character on the basis of previous characters, such models have been shown to automatically internalize linguistic concepts such as words, sentences, subclauses and even sentiment. In this paper, they propose to leverage the internal states of a trained character language model to produce a novel type of word embedding which we refer to as contextual string embeddings. **Their proposed embeddings have the distinct properties that they (a) are trained without any explicit notion of words and thus fundamentally model words as sequences of characters, and (b) are contextualized by their surrounding text, meaning that the same word will have different embeddings depending on its contextual use.** 
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/C18-1139/">The paper: Contextual String Embeddings for Sequence Labeling. Akbik et al. 2018 COLING</a>
</div>

# Reference 

- Paper 
  - [COLING Version: Contextual String Embeddings for Sequence Labeling. Akbik et al. COLING 2018](https://www.aclweb.org/anthology/C18-1139/)
  
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    




























