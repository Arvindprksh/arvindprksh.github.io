---
layout: post
title: Dependency-Based Word Embeddings
subtitle: Title of paper - Dependency-Based Word Embeddings
category: NLP papers - Word Embedding
tags: [neural network, word embedding, depedency_embedding]
permalink: /2020/05/14/Dependency-Based_Word_Embeddings/
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

This is a brief summary of paper for me to study and arrange it, [Dependency-Based Word Embeddings. Levy and Goldberg. ACL 2014](https://www.aclweb.org/anthology/P14-2050/) I read and studied. 
{% include MathJax.html %}

Previous work on neural word embeddings take the contexts of a word to be its linear context – words that precede and follow the target word, typically in a window of k tokens to each side. In this work, we generalize the SKIPGRAM model, and move from linear bag-of-words contexts to arbitrary word contexts.

They prposed the arbitrary context for word embedding based on the syntactic relations the word participates in. In other words. They generalize SKIPGRAM by replacing the bag-of-words contexts with arbitrary contexts.

This is implemented by parsing technology that allow parsing to syntactic dependencies.

They filter out “coincidental” contexts which are within the window but not directly related to the target word (e.g. Australian is not used as the context for discovers). In addition, the contexts are typed, indicating, for example, that stars are objects of discovery and scientists are subjects.

They thus expect the syntactic contexts to yield more focused embeddings, capturing more functional and less topical similarity 

The following is an example of dependency-base context extraction.

![Levy and Goldberg. ACL 2014](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-05-14_Dependency-Based_Word_Embeddings/Dependency_base_embedding.PNG)

They found out that BOW find words that associate with w, while DEPS find words that behave like w and then observe that while both BOW5 and BOW2 yield topical similarities, the larger window size result in more topicality, as expected

The result shwo up on Table 1 figure below. 

![Levy and Goldberg. ACL 2014](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-05-14_Dependency-Based_Word_Embeddings/Dependency_base_embedding_result.PNG)

The neural word-embeddings are considered opaque, in the sense that it is hard to assign meanings to the dimensions of the induced representation. They show that the SKIPGRAM model does allow for some introspection by querying it for contexts that are “activated by” a target word. This allows us to peek into the learned representation and explore the contexts that are found by the learning process to be most discriminative of particular words (or groups of words).

Neural word embeddings are often considered opaque and uninterpretable, unlike sparse vector space representations in which each dimension corresponds to a particular known context, or LDA models where dimensions correspond to latent topics. While this is true to a large extent, they observe that SKIPGRAM does allow a non-trivial amount of introspection. Although they cannot assign a meaning to any particular dimension, they can indeed get a glimpse at the kind of information being captured by the model, by examining which contexts are “activated” by a target word.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
While continuous word embeddings are gaining popularity, current models are based solely on linear contexts. In this work, they generalize the skip-gram model with negative sampling introduced by Mikolov et al. to include arbitrary contexts. In particular, they perform experiments with dependency-based contexts, and show that they produce markedly different embeddings. The dependencybased embeddings are less topical and exhibit more functional similarity than the original skip-gram embeddings.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P14-2050/">The paper: Dependency-Based Word Embeddings. Levy and Goldberg. ACL 2014</a>
</div>

# Reference 

- Paper 
  - [ACL 2014 Ver: Dependency-Based Word Embeddings. Levy and Goldberg. ACL 2014](https://www.aclweb.org/anthology/P14-2050/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    






























