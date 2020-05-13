---
layout: post
title: A Convolutional Neural Network for Modelling Sentences
subtitle: Title of paper - A Convolutional Neural Network for Modelling Sentences
category: NLP papers - Sentence Embedding
tags: [neural network, sentence embedding]
permalink: /2020/05/12/A_Convolutional_Neural_Network_for_Modelling_Sentences/
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

This is a brief summary of paper for me to study and arrange it, [A Convolutional Neural Network for Modelling Sentences. Kalchbrenner et al. ACL 2014](https://www.aclweb.org/anthology/P14-1062/) I read and studied. 
{% include MathJax.html %}

This paper propose sentence embedding method by convoutionala neural network with dynamic max pooling operation. 

Their method complements the Time-Delay Neural Network(TDNN), in particular, MAX-TDNN.

The architecture is the following:

![Kalchbrenner et al. ACL 20146](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-05-12-A_Convolutional_Neural_Network_for_Modelling_Sentences/dynamic_pooling.PNG)

As you can see figure above, their propose K-Max pooling which extract K highest valures in time sequence of p(i.e a sequence p). 

The order of K-max pooling corresponds to their orignal order of p. 

In the figure above, K-max pooling extracts K highest valures in time sequence of p. 

The Dynamic K-max pooling is to choose k dynamically depending on the number of convolutional layer and K in final k-max pooling.

The folding is simple way to give rise to dependencies in differenc row in sentence maxtrix by summing the fow in the maxtrix element-wise.


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
The ability to accurately represent sentences is central to language understanding. They describe a convolutional architecture dubbed the Dynamic Convolutional Neural Network (DCNN) that they adopt for the semantic modelling of sentences. The network uses Dynamic k-Max Pooling, a global pooling operation over linear sequences. The network handles input sentences of varying length and induces a feature graph over the sentence that is capable of explicitly capturing short and long-range relations. The network does not rely on a parse tree and is easily applicable to any language. 
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P14-1062/">The paper: A Convolutional Neural Network for Modelling Sentences. Kalchbrenner et al. ACL 2014</a>
</div>

# Reference 

- Paper 
  - [arXiv version: A Convolutional Neural Network for Modelling Sentences. Kalchbrenner et al. arXiv 2014](https://arxiv.org/abs/1404.2188)
  - [ACL 2014 version: A Convolutional Neural Network for Modelling Sentences. Kalchbrenner et al. ACL 2014](https://www.aclweb.org/anthology/P14-1062/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    






























