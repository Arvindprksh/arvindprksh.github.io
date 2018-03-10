---
layout: post
title: Centroid-based Text Summarization through Compositionality of Word Embeddings for Text summarization
subtitle: Title of paper - Centroid-based Text Summarization through Compositionality of Word Embeddings
category: NLP papers
tags: [nlp, word2vec, word_embedding, text_summarization]
permalink: /2018/03/09/Centroid-based_Text_Summarization_through_Compositionality_of_Word_Embeddings/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

This paper is about text summarization based on cetroid, and then they experiment multi-documents and a multi-lingual sigle document.

This paper's idea is using word embedding which is better on what words is similar on syntantic and semantic relationship rather than BOW(bag-of-words). 

Representation from BOW is orthogonal when they don't have word even though their meaning is the same.

BUT neural network language model is better rather than the relationship above. I mean inference using linear algebra of syntactic and semantic relationship.

Method for text summarization of this paper that I am introducing  is extrating centroid words which is represntative for each document per document. 

Then they are just comparing centroid vector to sentence vector in a document to select the representative summary of sentences in the document like this.

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Summarization/2018-03-09-Centroid-based_Text_Summarization_through_Compositionality_of_Word_Embeddings/figure1.png)

This paper argue word embedding is great on the effectivness of the compositionality to encode the semantic relation between words through vector dense representations.

I got idea about the effectiveness of compositionality of word embedding is better that encoding the semantic relations between words through vector dense representations. 

**This paper emphasizes about representation learning, when you summarize text, you could external knowledge. this means representation of word embedding from other corpus could be used to do something like NLP in the original corpus.** 

<!--
Let's see the procedure of this paper's work as I undertood. 

1. preprocessing document which is normal when you deal with natural language processing. 
 
   - just split the document into a sentence line by line, changing all text to lowercase, removing stopword. 
 
 <div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: what if I adapt this idea into korean language, I mena what preprocessing I have to do </b>

2. extrainting centorid words using topic threshold with tf*idf

 <div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: another way to extract centroid words using another way</b>
 
3. creating sentence vector just using a summing the vectors for each word in the sentence. 

dataset :  

- each 10 documents in 50 clusters from Associated Press and New York newswire - multidocuments

- 30 documents for each of 38 languages.

-->



<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
The textual similarity is a crucial aspect for many extractive text summarization methods. due to difficulty of text summarization, research work focused on the extractive aspect of summarization, where the generated summary is a selection of relevant sentences from a document(or a set of documents) in a copy-and-paste manner.
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="http://www.aclweb.org/anthology/W17-1003">The paper: Centroid-based Text Summarization through Compositionality of Word Embeddings</a>
</div>

# Reference 

 - Paper 
 -- [Centroid-based Text Summarization through Compositionality of Word Embeddings](http://www.aclweb.org/anthology/W17-1003)
 
 - How to use html for alert
 -- [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
