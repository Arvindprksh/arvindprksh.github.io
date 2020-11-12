---
layout: post
title: Linguistic Knowledge and Transferability of Contextual Representations. Liu et al. NAACL. 2019.
subtitle: Title of paper - Linguistic Knowledge and Transferability of Contextual Representations. Liu et al. NAACL. 2019.
category: NLP papers - Contextual Embedding
tags: [neural network, contextual embedding]
permalink: /2019/12/26/Linguistic_Knowledge_and_Transferability_of_Contextual_Representations/
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

This is a brief summary of paper for me to study and organize it, [Linguistic Knowledge and Transferability of Contextual Representations. Liu et al. NAACL 2019](https://www.aclweb.org/anthology/N19-1112/) I read and studied. 
{% include MathJax.html %}

This paper investigated the linguistic knowledge and transferability on contextual representation (e.g. ELMo, BERT) as follows:

![Liu et al. NAACL 2019](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Contextual_Embedding/2019-12-26-Linguistic_Knowledge_and_Transferability_of_Contextual_Representations/Linguistic_Knowledge_N_transferability_0.PNG)

They said their analysis reveals interesting insights: 

>>1. Linear models trained on top of frozen CWRs are competitive with state-of-the-art taskspecific models in many cases, but fail on tasks requiring fine-grained linguistic knowledge. In these cases, we show that tasktrained contextual features greatly help with encoding the requisite knowledge.    
>>2. The first layer output of long short-term memory (LSTM) recurrent neural networks is consistently the most transferable, whereas it is the middle layers for transformers.   
>>3. Higher layers in LSTMs are more taskspecific (and thus less general), while the transformer layers do not exhibit this same monotonic increase in task-specificity   
>>4. Language model pretraining yields representations that are more transferable in general than eleven other candidate pretraining tasks, though pretraining on related tasks yields the strongest results for individual end tasks.  

In summary, unlike Transformer, bidirectional LSTM language model yeilds the presentations that are more transferable in general that othe candidate tasks (i.e. supervied tasks)

Aslo, LSTM-based ELMo indicate the transferability and linguistic knowledge in lower layers but Transformer is in middel layer. 

Unlike transformer, LSTM-based ELMo indicate the task-specific information in higher layer than lower layer.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Contextual word representations derived from large-scale neural language models are successful across a diverse set of NLP tasks, suggesting that they encode useful and transferable features of language. To shed light on the linguistic knowledge they capture, they study the representations produced by several recent pretrained contextualizers (variants of ELMo, the OpenAI transformer language model, and BERT) with a suite of sixteen diverse probing tasks. They find that linear models trained on top of frozen contextual representations are competitive with state-of-the-art task-specific models in many cases, but fail on tasks requiring fine-grained linguistic knowledge (e.g., conjunct identification). To investigate the transferability of contextual word representations, they quantify differences in the transferability of individual layers within contextualizers, especially between recurrent neural networks (RNNs) and transformers. For instance, higher layers of RNNs are more taskspecific, while transformer layers do not exhibit the same monotonic trend. In addition, to better understand what makes contextual word representations transferable, they compare language model pretraining with eleven supervised pretraining tasks. For any given task, pretraining on a closely related task yields better performance than language model pretraining (which is better on average) when the pretraining dataset is fixed. However, language model pretraining on more data gives the best results.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/N19-1112/">The paper: Linguistic Knowledge and Transferability of Contextual Representations. Liu et al. NAACL 2019</a>
</div>

# Reference 

- Paper 
  - [arXiv version: Linguistic Knowledge and Transferability of Contextual Representations. Liu et al. arXiv 2019](https://arxiv.org/abs/1903.08855)
  - [NAACL 2019 version: Linguistic Knowledge and Transferability of Contextual Representations. Liu et al. NAACL 2019](https://www.aclweb.org/anthology/N19-1112/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [NAACL 2019 Highlight on Ruder.io](http://ruder.io/naacl2019/)
  
  - Slide 
    - [Transfer Learning in Natural Language Processing tutorial on NAACL-HLT 2019](https://docs.google.com/presentation/d/1fIhGikFPnb7G5kr58OvYC3GN4io7MznnM0aAgadvJfc/edit#slide=id.g5888218f39_177_4)
































