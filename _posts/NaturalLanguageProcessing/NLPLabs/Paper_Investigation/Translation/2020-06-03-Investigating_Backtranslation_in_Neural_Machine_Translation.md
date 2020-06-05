---
layout: post
title: Investigating Backtranslation in Neural Machine Translation
subtitle: Title of paper - Investigating Backtranslation in Neural Machine Translation
category: NLP papers - Translation
tags: [neural network, translation]
permalink: /2020/06/03/Investigating_Backtranslation_in_Neural_Machine_Translation/
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

This is a brief summary of paper for me to note it, [Investigating Backtranslation in Neural Machine Translation. Poncelas et al. ArXiv 2018](https://arxiv.org/abs/1804.06189v1)

{% include MathJax.html %}

This paper explore empirically how effective the back-traslationt technique is in NMT system. 

As in their saying, There is a scenario where there are not enough authentic data (human-translated parallel data) available to obtain high-quality results. 

So many research for NMT used back-translated data to retrain NMT system with data augmentation.

But They hypothesize that NMT with 'imperfect' data will - at some point - undo any benefit from the 'perfect' (human-translated) data , and lead the NMT to degrade in performance.

They implemented three scenarios which are authentic data only, syntenthic data only, and hybrid data.

When they evalute the performance, they used a number of common evaluation metrics – BLEU, TER, METEOR, and CHRF– to give a more comprehensive estimation of the comparative translation quality.

With the exception of TER, the higher the score, the better the performance; for TER which is an error metric, the lower the score, the better the quality.

They showed that hybrid model is better than model with authentic data only, and then the quality of hybrid starts degrading as the synthetic data overpowers the authentic.

In their experimental set-up and data, they reached that point at a synthetic-to-authentic ratio of 2:1. 

They argue adding incrementally larger amounts of back-translated data is less harmful than they expect.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
A prerequisite for training corpus-based machine translation (MT) systems – either Statistical MT (SMT) or Neural MT (NMT) – is the availability of high-quality parallel data. This is arguably more important today than ever before, as NMT has been shown in many studies to outperform SMT, but mostly when large parallel corpora are available; in cases where data is limited, SMT can still outperform NMT. Recently researchers have shown that back-translating monolingual data can be used to create synthetic parallel corpora, which in turn can be used in combination with authentic parallel data to train a highquality NMT system. Given that large collections of new parallel text become available only quite rarely, backtranslation has become the norm when building state-of-the-art NMT systems, especially in resource-poor scenarios. However, we assert that there are many unknown factors regarding the actual effects of back-translated data on the translation capabilities of an NMT model. Accordingly, in this work we investigate how using back-translated data as a training corpus – both as a separate standalone dataset as well as combined with human-generated parallel data – affects the performance of an NMT model. We use incrementally larger amounts of back-translated data to train a range of NMT systems for German-to-English, and analyse the resulting translation performance.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1804.06189v1">The paper: Investigating Backtranslation in Neural Machine Translation. Poncelas et al. ArXiv 2018</a>
</div>

# Reference 

- Paper 
  - [ArXiv version: Investigating Backtranslation in Neural Machine Translation. Poncelas et al. ArXiv 2018](https://arxiv.org/abs/1804.06189v1)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
