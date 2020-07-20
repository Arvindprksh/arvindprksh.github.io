---
layout: post
title: Bag-of-Embeddings for Text Classification
subtitle: Title of paper - Bag-of-Embeddings for Text Classification
category: NLP papers - Multi-prototype Embedding
tags: [neural network, word embedding]
permalink: /2020/07/20/Bag-of-Embeddings_for_Text_Classification/
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

This is a brief summary of paper for me to study and arrange it, [Bag-of-Embeddings for Text Classification. Jin et al. IJCAI 2016](https://dl.acm.org/doi/10.5555/3060832.3061016) I read and studied. 
{% include MathJax.html %}

They thought One useful feature beyond bag-of-words as bag-of-ngrams.

In particular they said bigrams offer a certain degree of compositionality while being relatively less sparse compared with larger n-gram features with text below: 

'''
For example, the bigram “abnormal return” strongly indicates finance, although both “abnormal” and “return” can be common across difference classes. Similar examples include “world cup” and “large bank”, where bi-grams indicate text classes, but the words do not.  

One intuitive reason behind the strength of bigrams is that they resolve the ambiguity of polysemous words. In the above examples the words ”return”, ”cup”, and ”bank” have different meanings under different document classes, and the correct identification of their word sense under a ngram context is useful for identifying the document class. For example, when the word ”bank” exists under a context with words such as ”card” and ”busy”, it strongly indicates the ”finance” sense. This fact suggests a simple extension to bag-of-word features by incorporating context and word sense information. We propose a natural extension to the skip-gram word embedding model
'''

With article above, They proposed bag-of-embedding by exploiting using multi-prototype word embedding as follows:

![Jin et al. IJCAI 2016](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-07-20-Bag-of-Embeddings_for_Text_Classification/bag-of-embedding.PNG)

As you can see image above, they are different from the skip-gram model in the definition of target and context embeddings in that the target embeddings are class-dependent, and each word can have different target embeddings in different classes. On the other hand, each word has a unique context embedding across classes.

While based on Skip-gram model, on constrary to handling input on original Skip-gram model, they used context vector as input and target vector as output.

For a text classifier, they bulit by using a Naive Bayes model with bag-of-embeddings probabilities. 

Their result showed the bag-of-embedding model exploits contextual information by deriving the probabilities of class-sensitive embedding vectors from their inner product with context words.


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Words are central to text classification. It has been shown that simple Naive Bayes models with word and bigram features can give highly competitive accuracies when compared to more sophisticated models with part-of-speech, syntax and semantic features. Embeddings offer distributional features about words. They study a conceptually simple classification model by exploiting multiprototype word embeddings based on text classes. The key assumption is that words exhibit different distributional characteristics under different text classes. Based on this assumption, they train multiprototype distributional word representations for different text classes. Given a new document, its text class is predicted by maximizing the probabilities of embedding vectors of its words under the class.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://dl.acm.org/doi/10.5555/3060832.3061016">The paper: Bag-of-Embeddings for Text Classification. Jin et al. IJCAI 2016</a>
</div>

# Reference 

- Paper 
  - [IJCAI 2016 version: Bag-of-Embeddings for Text Classification. Jin et al. IJCAI 2016](https://www.ijcai.org/Proceedings/16/Papers/401.pdf)
  - [IJCAI 2016 version on ACM library: Bag-of-Embeddings for Text Classification. Jin et al. IJCAI 2016](https://dl.acm.org/doi/10.5555/3060832.3061016)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    






























