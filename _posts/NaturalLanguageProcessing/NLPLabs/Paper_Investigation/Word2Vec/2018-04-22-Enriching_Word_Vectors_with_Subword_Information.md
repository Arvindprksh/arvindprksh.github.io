---
layout: post
title: Enriching Word Vectors with Subword Information
subtitle: Title of paper - Enriching Word Vectors with Subword Information
category: NLP papers
tags: [nlp, word2vec]
permalink: /2018/04/22/Enriching_Word_Vectors_with_Subword_Information/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

This paper have been arguing it is better on inference of words out of Vocabulary by using character levels n-gram. 

i.e. word2vec treats each word in corpus like an atomic entity and generates a vector for each word. 

But, in this paper, treats each word as compossed of character ngrams. 

So the vector for a word is made fo the sum of this character n grams. 

Let's see an example like this :

the word of **apple** is a sum of the vectors of the n-grams 

> "<ap", "app", "appl", "apple", "apple>", "ppl", "pple", "pple>", "ple", "ple>", "le>"

"<" and ">" is intended for order of word. 

On the example above, using hyperparameters for smallest ngram is 3 and largest ngram is 6. i.e. minimum is 3 and maximum is 6. 

that is why they argue on small size of corpus the vector using the character level n grams is better than the vector using word as atomic entity.

they present a word by the sum  of vector representations of its n-grams.

<div class="alert alert-success" role="alert"><i class="fa fa-check-square-o"></i> <b>Tip: </b>
be careful of how to handle n gram of character level <br/>
they dealt with the following  about "apple" : <br/>
> "<ap", "app", "appl", "apple", "apple>", "ppl", "pple", "pple>", "ple", "ple>", "le>" <br/>
i.e. ngram size is between 3 and 6 on the example above. 
</div>


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
Continuous word representations ingores the morphology of words, by assigning a distinct vector to each word. This is limitation, especially for languages with large vocabularies and many rare words. In this paper, they propose a enw approach based on the skip gram model, where each word is represented as a bag of character n-grams. A vector representation is associated to each character n-gram; words being represented as the sum of these representations.
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1607.04606v2">The paper: Enriching Word Vectors with Subword Information</a>
</div>

# Reference 

- Paper 
  - [Enriching Word Vectors with Subword Information](https://arxiv.org/abs/1607.04606v2)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
- Quora
  - [What is the main difference between word2vec and fastText?](https://www.quora.com/What-is-the-main-difference-between-word2vec-and-fastText)
   
  
