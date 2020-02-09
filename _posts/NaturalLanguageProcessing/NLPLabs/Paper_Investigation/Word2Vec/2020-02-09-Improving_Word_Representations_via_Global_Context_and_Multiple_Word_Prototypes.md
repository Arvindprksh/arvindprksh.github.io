---
layout: post
title: Improving Word Representations via Global Context and Multiple Word Prototypes
subtitle: Title of paper - Improving Word Representations via Global Context and Multiple Word Prototypes
category: NLP papers - Word Embedding
tags: [neural network, word embedding]
permalink: /2019/08/06/Universal_Language_Model_Fine_tuning_for_Text_Classification/
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

This is a brief summary of paper for me to study and organize it, [Improving Word Representations via Global Context and Multiple Word Prototypes. Huang et al. ACL 2012](https://www.aclweb.org/anthology/P12-1092/) I read and studied. 
{% include MathJax.html %}

They propose new language model using both local and global context. 

Also, They release the new dataset for simlilarity on a pair of words in sentential context.

The new dataset included pairs of the homonymous and polysemous words. 

When they used the global context, they used **tf-idf** as weighting function to generate the context vector. 

The following figure indicates their model architecture.

Besides global context, They used multi-prototypes to represent the word vector. 

In other words, The existing distributed representation of words is problematic with single prototype representaiton. 

If words is represented as single prototype, the polysemous and homonymous words is represented as the same vector. 

It cannont represent any one of the meanings well as it is influenced by all meaning s of the word. 

So, they used multi-prototype approach for vector space model, which uses multiple representations to capture different senses and usages of a word.

In order for them to learn the multi-prototype approach, they use weighted average of context words' vectors.

They alos used **idf-weighting** as weighting functions for context vector.

Finally, for multi-prototype approach, each occurence in the corpus is re-labeled to its associated cluster and is used to train the word representation for that cluster.

The following is the architecture using **global context**.

![Huang et al. ACL 2012](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-02-09-Improving_Word_Representations_via_Global_Context_and_Multiple_Word_Prototypes/multi-prototypes.PNG)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Unsupervised word representations are very useful in NLP tasks both as inputs to learning algorithms and as extra word features in NLP systems. However, most of these models are built with only local context and one representation per word. This is problematic because words are often polysemous and global context can also provide useful information for learning word meanings. They present a new neural network architecture which 1) learns word embeddings that better capture the semantics of words by incorporating both local and global document context, and 2) accounts for homonymy and polysemy by learning multiple embeddings per word. They also introduce a new dataset with human judgments on pairs of words in sentential context.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P12-1092/">The paper: Improving Word Representations via Global Context and Multiple Word Prototypes. Huang et al. ACL 2012</a>
</div>

# Reference 

- Paper 
  - [ACL 2012 version: Improving Word Representations via Global Context and Multiple Word Prototypes. Huang et al. ACL 2012](https://www.aclweb.org/anthology/P12-1092/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [ICML 2008: A unified architecture for natural language processing: deep neural networks with multitask learning. Collobert and Weston. ICML 2008. ](https://dl.acm.org/doi/10.1145/1390156.1390177)
  - [EMNLP 2010: A Mixture Model with Sharing for Lexical Semantics. Reisinger and Mooney. EMNLP 2010](https://www.aclweb.org/anthology/D10-1114/7)
  - [NAACL 2010: Multi-Prototype Vector-Space Models of Word Meaning.  Reisinger and Mooney. NAACL 2010](https://www.aclweb.org/anthology/N10-1013/)
  






























