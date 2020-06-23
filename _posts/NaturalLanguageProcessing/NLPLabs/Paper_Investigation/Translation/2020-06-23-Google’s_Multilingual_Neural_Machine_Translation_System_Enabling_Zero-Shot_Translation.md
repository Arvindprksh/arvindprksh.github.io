---
layout: post
title: Google's Multilingual Neural Machine Translation System- Enabling Zero-Shot Translation
subtitle: Title of paper - Google's Multilingual Neural Machine Translation System- Enabling Zero-Shot Translation
category: NLP papers - Translation
tags: [translation]
permalink: /2020/06/23/Google's_Multilingual_Neural_Machine_Translation_System_Enabling_Zero-Shot_Translation/
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

This is a brief summary of paper for me to note it, [Google’s Multilingual Neural Machine Translation System: Enabling Zero-Shot Translation. Johnson et al. TACL 2017](https://www.aclweb.org/anthology/Q17-1024/)

{% include MathJax.html %}


They use a model sharing weight between multilingual language pair. 

They only amend to data which introduce artificial token at the beginning of the input sentence to specify the required target sentence.

The basic model is the following:

![Johnson et al. TACL 2017](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2020-06-23-Google’s_Multilingual_Neural_Machine_Translation_System_Enabling_Zero-Shot_Translation/translation_model.PNG)


Their method's strength is explained as follows:

- Simplicity: 

>>Since no changes are made to the architecture of the model, scaling to more languages is trivial — any new data is simply added, possibly with over- or under-sampling such that all languages are appropriately represented, and used with a new token if the target language changes.   
>>Since no changes are made to the training procedure, the mini-batches for training are just sampled from the overall mixed-language training data just like for the single-language case.   
>>Since no a-priori decisions about how to allocate parameters for different languages are made the system adapts automatically to use the total number of parameters efficiently to minimize the global loss.     
>>A multilingual model architecture of this type also simplifies production deployment significantly since it can cut down the total number of models necessary when dealing with multiple languages.   
>>Note that at Google, They support a total of over 100 languages as source and target, so theoretically 1002 models would be necessary for the best possible translations between all pairs, if each model could only support a single language pair.     
>>Clearly this would be problematic in a production environment.    
>>Even when limiting to translating to/from English only, we still need over 200 models.   
>>Finally, batching together many requests from potentially different source and target languages can significantly improve efficiency of the serving system.   
>>In comparison, an alternative system that requires language-dependent encoders, decoders or attention modules does not have any of the above advantages.  

- Low-resource language improvements:

>>In a multilingual NMT model, all parameters are implicitly shared by all the language pairs being modeled.   
>>This forces the model to generalize across language boundaries during training.   
>>It is observed that when language pairs with little available data and language pairs with abundant data are mixed into a single model, translation quality on the low resource language pair is significantly improved.  

- Zero-shot translation: 

>>A surprising benefit of modeling several language pairs in a single model is that the model can learn to translate between language pairs it has never seen in this combination during training (zero-shot translation) — a working example of transfer learning within neural translation models.   
>>For example, a multilingual NMT model trained with Portuguese→English and English→Spanish examples can generate reasonable translations for Portuguese→Spanish although it has not seen any data for that language pair.    
>>They show that the quality of zero-shot language pairs can easily be improved with little additional data of the language pair in question (a fact that has been previously confirmed for a related approach which is discussed in more detail in the next section).  

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They propose a simple solution to use a single Neural Machine Translation (NMT) model to translate between multiple languages. Their solution requires no changes to the model architecture from a standard NMT system but instead introduces an artificial token at the beginning of the input sentence to specify the required target language. The rest of the model, which includes an encoder, decoder and attention module, remains unchanged and is shared across all languages. Using a shared wordpiece vocabulary, their approach enables Multilingual NMT using a single model without any increase in parameters, which is significantly simpler than previous proposals for Multilingual NMT. On the WMT’14 benchmarks, a single multilingual model achieves comparable performance for English→French and surpasses state-of-the-art results for English→German. Similarly, a single multilingual model surpasses state-of-the-art results for French→English and German→English on WMT’14 and WMT’15 benchmarks, respectively. On production corpora, multilingual models of up to twelve language pairs allow for better translation of many individual pairs. In addition to improving the translation quality of language pairs that the model was trained with, their models can also learn to perform implicit bridging between language pairs never seen explicitly during training, showing that transfer learning and zero-shot translation is possible for neural translation. Finally, they show analyses that hints at a universal interlingua representation in their models and show some interesting examples when mixing languages.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/Q17-1024/">The paper: Google’s Multilingual Neural Machine Translation System: Enabling Zero-Shot Translation. Johnson et al. TACL 2017</a>
</div>

# Reference 

- Paper 
  - [ArXiv version: Google’s Multilingual Neural Machine Translation System: Enabling Zero-Shot Translation. Johnson et al. ArXiv 2017](https://arxiv.org/abs/1611.04558)
  - [TACL version: Google’s Multilingual Neural Machine Translation System: Enabling Zero-Shot Translation. Johnson et al. TACL 2017](https://www.aclweb.org/anthology/Q17-1024/)
  
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
