---
layout: post
title: On Using Very Large Target Vocabulary for Neural Machine Translation
subtitle: Title of paper - On Using Very Large Target Vocabulary for Neural Machine Translation
category: NLP papers - Translation
tags: [translation]
permalink: /2020/11/02/On_Using_Very_Large_Target_Vocabulary_for_Neural_Machine_Translation/
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

This is a brief summary of paper for me to study and organize it, [On Using Very Large Target Vocabulary for Neural Machine Translation. Jean et al. ACL and IJCNLP 2015](https://www.aclweb.org/anthology/P15-1001/) I read and studied. 
{% include MathJax.html %}

Despite its recent success to neural machine translation, the neural machine translation has its limitation in handling a larger vocabulary.
 
So, they propose new alorithm to resolve the problem that neural network-based machine translation. 

There is one of the maine difficulties in training this neural machine traslation model. 

It is the comptutational complexity involved in the target word probability. 

They explained two model-specific approaches to this issue of large target vocabulary. 

- The first approach is to stochastically approximate the target word probability

- Other than these model-specific approaches, there exist translation-specific approaches. A translation-specific approach exploits the properties of the rare target words.

They used a model-specific approacah that allows them to tarin a neural network machine translation model with a very large target vocabulary. 

In other word, they also used the small subset of the target vocabulary at each update.

Once training is over, Their method can use the full target vocabulary to compute the output probabliity of each target word. 

For their approach, since the number of parameter being updated for each sentence pair cannot be controlled, they partitions the training corpus and define a subset \\(v^{`}\\) of target vocabulary for each partition prior to training.

That is, before training begins, they sequentially examine each target sentence in the training corpus and accumulate unique target words until the number of unique target words reaches the predefined threshold τ.

The accumulated vocabulary will be used for this partition of the corpus during training. 

They repeat this until the end of the training set is reached. 

They also used the most likely target words as shortlist to deconding and call it a candidate list.

If you want to know the result of their experiment, I refer you to [On Using Very Large Target Vocabulary for Neural Machine Translation. Jean et al. ACL and IJCNLP 2015](https://www.aclweb.org/anthology/P15-1001/)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Neural machine translation, a recently proposed approach to machine translation based purely on neural networks, has shown promising results compared to the existing approaches such as phrasebased statistical machine translation. Despite its recent success, neural machine translation has its limitation in handling a larger vocabulary, as training complexity as well as decoding complexity increase proportionally to the number of target words. In this paper, they propose a method based on importance sampling that allows them to use a very large target vocabulary without increasing training complexity. They show that decoding can be efficiently done even with the model having a very large target vocabulary by selecting only a small subset of the whole target vocabulary. The models trained by the proposed approach are empirically found to match, and in some cases outperform, the baseline models with a small vocabulary as well as the LSTM-based neural machine translation models. 
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P15-1001/">The paper: On Using Very Large Target Vocabulary for Neural Machine Translation. Jean et al. ACL and IJCNLP 2015</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: On Using Very Large Target Vocabulary for Neural Machine Translation. Jean et al. arXiv 2015](https://arxiv.org/abs/1412.2007)
  - [ACL and IJCNLP 2015 version: On Using Very Large Target Vocabulary for Neural Machine Translation. Jean et al. ACL and IJCNLP 2015](https://www.aclweb.org/anthology/P15-1001/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


