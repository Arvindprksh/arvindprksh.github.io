---
layout: post
title: Linguistic Regularities in Continuous Space Word Representations for Word2Vec investigation
subtitle: Title of paper - Linguistic Regularities in Continuous Space Word Representations
category: NLP papers
tags: [nlp, word2vec, svm]
permalink: /2018/01/14/Linguistic_Regularities_In_Continuous_Space_Word_Representations/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

The paper, "Linguisitic Regularities in Continuous Space Word Representation" explains how to evaluate sytantic and semantic regularities between the induced word vectors, with a form as "king - Man + Woman" result in a vector veryl clost to "Queen".

i.e. When you evaluate syntatic and semantic regularities with word vector representations in continous space. you have to create a test set of analogy questions of the form "a is to b as c is to \_\_\_".  i.e. If you know a, b, and c words. what is \_\_\_?

> A : B = C : \_\_\_

The above computation is so easy. it is observed as constant vetor offsets between pairs of words sharing a particular relationship.

Their relationship is like : 

> base/comparative/superlative forms of adjectives;  
singular/plural forms of commmon nouns;   
possessive/non-possessive froms of common nouns;  
base, past and 3rd person present tense forms of verbs.  

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2018-01-14-Linguistic_Regularities_In_Continuous_Space_Word_Representations/vector_offset_relationship.png)


Using vector offsets, this paper tested the relationship of words vector to check how well the vectors represents syntantic and semantic regularities. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2018-01-14-Linguistic_Regularities_In_Continuous_Space_Word_Representations/Test set pattern.png)


So when they created verification set of words relationship. they used tagged 276M words of newspaper text with PennTreebank POS tags. and they selected 100 of the most frequent comparatives adjectives, (words labeled JJR); 100 of the most frequent plural nouns (NNS); 100 of the most frequent possessive nouns(NN_POS); and 100 of the most frequent base form verbs(VB)

With 100 words from each set of the above thing, they then systematically generated analogy quesions by randomly matching each of the 100 words with 5 other words from the same category, and creating variants as indicated in the above figure, Table 1. 

Total test set size is 8000.
 
<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
In continous space for word vector, The key point is similar words are likely to have similar vectors. Thus, When the model parameters are adjusted in response to a particular word or word-sequence, The improvements will carry over to occurences of similar words and sequences.</br>
</br>
If you want to download the data set this paper used, visit here http://research.microsoft.com/en-us/projects/rnn/default.aspx
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/N13-1090">The paper: Linguistic  Regularities in Continous Space Word Representations</a>
</div>

# Reference 

- Paper 
  - [Linguistic Regularities in Continuous Space Word Representations](https://www.aclweb.org/anthology/N13-1090)
 
- [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
