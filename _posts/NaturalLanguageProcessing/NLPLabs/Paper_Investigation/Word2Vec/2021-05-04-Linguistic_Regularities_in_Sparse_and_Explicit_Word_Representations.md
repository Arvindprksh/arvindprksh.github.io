---
layout: post
title: Linguistic Regularities in Sparse and Explicit Word Representations
subtitle: Title of paper - Linguistic Regularities in Sparse and Explicit Word Representations
category: NLP papers - Word Embedding
tags: [word vector, linguistic reularity]
permalink: /2021/05/04/Linguistic_Regularities_in_Sparse_and_Explicit_Word_Representations/
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

This is a brief summary of paper for me to study and organize it, [Linguistic Regularities in Sparse and Explicit Word Representations (Levy and Goldberg, CoNLL 2014)](https://www.aclweb.org/anthology/W14-1618/) that I read and studied. 
{% include MathJax.html %}

They demonstrated that the linguistic regularity in word embedding is also captured by the traditional distributed word representation, which is the co-occurence matrix with word and context word. 

In other words, for word embedding by neural network, it has the property: words that appear in similar contexts will be close to each other in the projected space.

The property makes word embedding share semantic or syntactic  properties or capture linguistic regularities and relational similarties. 

Those properties also can be captured by the word-context co-occurence matrix. 

To sump their saying up, The linguistic regularities apparent in neural embedding are not a consequence of the embedding process, but rather are well preserved by neural embedding.

In order to prove it, they suggest new objective function to eevaluate liguistic regularity using logarithm.

For detailed experiment analysis, you can found in [Linguistic Regularities in Sparse and Explicit Word Representations (Levy and Goldberg, CoNLL 2014)](https://www.aclweb.org/anthology/W14-1618/)
  
<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Recent work has shown that neural embedded word representations capture many relational similarities, which can be recovered by means of vector arithmetic in the embedded space. They show that Mikolov et al.’s method of ﬁrst adding and subtracting word vectors, and then searching for a word similar to the result, is equivalent to searching for a word that maximizes a linear combination of three pairwise word similarities. Based on this observation, they suggest an improved method of recovering relational similarities, improving the state-of-the-art results on two recent word-analogy datasets. Moreover, they demonstrate that analogy recovery is not restricted to neural word embeddings, and that a similar amount of relational similarities can be recovered from traditional distributional word representations.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/W14-1618/">The paper: Linguistic Regularities in Sparse and Explicit Word Representations (Levy and Goldberg, CoNLL 2014)</a>
</div>

# Reference 

- Paper 
  - [CoNLL 2014 : Linguistic Regularities in Sparse and Explicit Word Representations (Levy and Goldberg, CoNLL 2014)](https://www.aclweb.org/anthology/W14-1618/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


