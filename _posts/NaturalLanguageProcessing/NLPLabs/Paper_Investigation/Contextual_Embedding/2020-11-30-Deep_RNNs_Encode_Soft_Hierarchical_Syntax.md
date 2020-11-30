---
layout: post
title: Deep RNNs Encode Soft Hierarchical Syntax
subtitle: Title of paper - Deep RNNs Encode Soft Hierarchical Syntax
category: NLP papers - Contextual Embedding
tags: [contextual embedding]
permalink: /2020/11/30/Deep_RNNs_Encode_Soft_Hierarchical_Syntax/
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

This is a brief summary of paper for me to study and organize it, [Deep RNNs Encode Soft Hierarchical Syntax (Blevins et al., ACL 2018)](https://www.aclweb.org/anthology/P18-2003/) that I read and studied. 
{% include MathJax.html %}

They show that the internal representations of RNNs trained on a variety of NLP tasks encode these syntactic features without explicit supervision. And they found that deeper layers in each model capture notions of syntax that are higher-level and more abstract, in the sense that higher-level constituents cover a larger span of the underlying sentence.

These findings suggest that models trained on NLP tasks are able to induce syntax even when direct syntactic supervision is unavailable. 

For experiment, They desing how to experiment for check if the RNN induced syntax information. 

Given a model that uses multi-layered RNNs, they collect the vector representation \\(x^{l}_{i}\\) of each word \\(i\\) at each hidden layer \\(l\\).

To determine what syntactic information is stored in each word vector, they try to predict part-of-speech from the vector alone.

Specifically, they predict the word’s part of speech (POS), as well as the first (parent), second (grand-parent), and third level (great-grandparent) constituent labels of the given word.

Consequently, they run a series of prediction tasks on the internal representations of deep NLP models as follows:

![Blevins et al., ACL 2018](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Contextual_Embedding/2020-11-30-Deep_RNNs_Encode_Soft_Hierarchical_Syntax/model.PNG)

They evaluate how well a simple feedforward classifier can detect these syntax features from the word representations produced by the RNN layers from deep NLP models trained on the tasks of dependency parsing, semantic role labeling, machine translation, and language modeling.

The prediction task to identfy if these RNNs are able to induce syntax without explicit linguaistic supervision is implement on the RNN models above.

![Blevins et al., ACL 2018](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Contextual_Embedding/2020-11-30-Deep_RNNs_Encode_Soft_Hierarchical_Syntax/POS_task.PNG)

Fro predictions task, they attempt to predict the POS tag and the parent, grandparent, and great-grandparent constituent labels of that word.

They found that the representations taken from deeper layers of the RNNs perform better on higher-level syntax tasks than hose from shallower layers, suggesting that these recurrent models induce a soft hierarchy over the encoded syntax. 

They said as follows

>> these results provide some insight as to why deep RNNs are able to model NLP tasks without annotated linguistic features. 

For detailed experiment analysis, you can found in [Deep RNNs Encode Soft Hierarchical Syntax (Blevins et al., ACL 2018)](https://www.aclweb.org/anthology/P18-2003/)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They present a set of experiments to demonstrate that deep recurrent neural networks (RNNs) learn internal representations that capture soft hierarchical notions of syntax from highly varied supervision. They consider four syntax tasks at different depths of the parse tree; for each word, they predict its part of speech as well as the first (parent), second (grandparent) and third level (great-grandparent) constituent labels that appear above it. These predictions are made from representations produced at different depths in networks that are pretrained with one of four objectives: dependency parsing, semantic role labeling, machine translation, or language modeling. In every case, they find a correspondence between network depth and syntactic depth, suggesting that a soft syntactic hierarchy emerges. This effect is robust across all conditions, indicating that the models encode significant amounts of syntax even in the absence of an explicit syntactic training supervision.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P18-2003/">The paper: Deep RNNs Encode Soft Hierarchical Syntax (Blevins et al., ACL 2018)</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: Deep RNNs Encode Soft Hierarchical Syntax (Blevins et al., arXiv 2018)](https://arxiv.org/abs/1805.04218)
  - [ACL Version: Deep RNNs Encode Soft Hierarchical Syntax (Blevins et al., ACL 2018)](https://www.aclweb.org/anthology/P18-2003/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


