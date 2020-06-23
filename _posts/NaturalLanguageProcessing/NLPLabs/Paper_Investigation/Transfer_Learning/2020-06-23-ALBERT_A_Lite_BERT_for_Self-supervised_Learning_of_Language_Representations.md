---
layout: post
title: ALBERT- A Lite BERT for Self-supervised Learning of Language Representations
subtitle: Title of paper - ALBERT- A Lite BERT for Self-supervised Learning of Language Representations
category: NLP papers - Transfer Learning
tags: [transfer learning]
permalink: /2020/06/23/ALBERT_A_Lite_BERT_for_Self-supervised_Learning_of_Language_Representations/
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

This is a brief summary of paper for me to study and organize it, [ALBERT- A Lite BERT for Self-supervised Learning of Language Representations. Lan et al. ICLR 2020](https://openreview.net/forum?id=H1eA7AEtvS) I read and studied. 
{% include MathJax.html %}

They propose light version of BERT_based model by using two parameter redcutions.

There are several ways to reduce parameter as follows:

- prunining 
- weight sharing 
- Quatatization 
- Low-rank Approximation 
- Sparse Regularization 
- Distillation 

They used weight sharing and factoriztion of parameter in ALBERT they proposed.

- Factorized embedding parameterization

- Cross-layer parameter sharing

And then they used another loss against next sentence prediction loss utilized in BERT paper. 

It is **Inter-sentence coherence loss**.


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Increasing model size when pretraining natural language representations often results in improved performance on downstream tasks. However, at some point further model increases become harder due to GPU/TPU memory limitations and longer training times. To address these problems, they present two parameter reduction techniques to lower memory consumption and increase the training speed of BERT. Comprehensive empirical evidence shows that their proposed methods lead to models that scale much better compared to the original BERT. They also use a self-supervised loss that focuses on modeling inter-sentence coherence, and show it consistently helps downstream tasks with multi-sentence inputs.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://openreview.net/forum?id=H1eA7AEtvS">The paper: ALBERT- A Lite BERT for Self-supervised Learning of Language Representations. Lan et al. ICLR 2020</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: ALBERT- A Lite BERT for Self-supervised Learning of Language Representations. Lan et al. arXiv 2020](https://arxiv.org/abs/1909.11942)
  - [ICLR 2020 version: ALBERT- A Lite BERT for Self-supervised Learning of Language Representations. Lan et al. ICLR 2020](https://openreview.net/forum?id=H1eA7AEtvS)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [GLUE benchmark](https://gluebenchmark.com/)
  - [Lightweight Deep Learning with Model Compression](https://datalab.snu.ac.kr/~ukang/talks/19-BigComp19-tutorial/DeepModelCompression-2.pdf)
  
































