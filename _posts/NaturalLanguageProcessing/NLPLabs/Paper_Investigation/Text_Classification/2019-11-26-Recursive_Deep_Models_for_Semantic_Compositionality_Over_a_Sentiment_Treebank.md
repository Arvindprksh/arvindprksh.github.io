---
layout: post
title: Recursive Deep Models for Semantic Compositionality Over a Sentiment Treebank
subtitle: Title of paper - Recursive Deep Models for Semantic Compositionality Over a Sentiment Treebank
category: NLP papers - Text_classification
tags: [neural_network, text_classification]
permalink: /2019/11/26/Recursive_Deep_Models_for_Semantic_Compositionality_Over_a_Sentiment_Treebank/
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

This is a brief summary of paper for me to study and organize it, [Recursive Deep Models for Semantic Compositionality Over a Sentiment Treebank. (Socher et al. EMNLP 2013)](https://www.aclweb.org/anthology/D13-1170/) I read and studied. 
{% include MathJax.html %}

This paper focused on the compositionalty of semantic vector space based on a well-structed tree. 

They suggest model and how to compositionality of sentimental data as followings: 

![Socher et al. EMNLP 2013](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Classification/2019-11-26-Recursive_Deep_Models_for_Semantic_Compositionality_Over_a_Sentiment_Treebank/SENT_tree_bank1.PNG)

They provide a new model to embed the compositionality of new dataset called the [Stanford Sentiment Treebank](https://nlp.stanford.edu/sentiment/)

They called the model RNTN (recursive neural tensor network).

They said in recent years, 

>> sentiment accuracies even for binary positive/negative classification for single sentences has not exceeded 80% for several years. For the mor difficult multiclass case including a neutral class, accuary is oftne below 60% for short meassages on Twitter.   
>> From a linguistic or conginitive standpoint, ignoring word order in the treatment of a semantic task is no plausible.


Also they found 

>> some from labeling sentences based on reader's perception is that many of them could be considered neutral. Besides they found that stronger sentiment often builds up in longer phrases and majority of the shorter phrases are neutral. Another observation is that most of annotators moved slider to on e fo the five position: negative, somewhat negative, neutral, somewhat positive, or positive. the extreme values were rarely used and the slider was not often left in between the ticks.

They used softmax as classifier on each node as followings: 

![Socher et al. EMNLP 2013](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Classification/2019-11-26-Recursive_Deep_Models_for_Semantic_Compositionality_Over_a_Sentiment_Treebank/SENT_tree_bank2.PNG)

As you can see the figure above, they use word vectors immediately as parameters to optimize and as feature input to a softmax classifier.

Let's walk through recursive neural network ahead of getting to their model RNTN.

The simplest member of the family of recursive neural networks is the **standard recursive neural network**

First, it is determined which parent already has all its children computed. In the above exmple figure, \\(p_1\\) has its two children's vectors since both are words. the standard recursive neural network(RNN) uses the following equations to compute the parent node vectors:

![Socher et al. EMNLP 2013](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Classification/2019-11-26-Recursive_Deep_Models_for_Semantic_Compositionality_Over_a_Sentiment_Treebank/SENT_tree_bank_equation1.PNG)

Where $f=tanh$ is a standard element-wise nonlinearity. The dimensionality of parent node vectors is the same from that of childrens for recursive composition.

The second member of RNNs is Matrix-Vector RNN (MV-RNN) that is linguistically motivated in that most of the parameters are associated with words and each composition function that computes vectors for longer phrases depends on the actual words being combined.

For this model, each n-gram is represented as al ist of (vector, matrix) paris, together with the parse tree. For the tree with (vector, matrix) nodes: 

![Socher et al. EMNLP 2013](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Classification/2019-11-26-Recursive_Deep_Models_for_Semantic_Compositionality_Over_a_Sentiment_Treebank/SENT_tree_bank_equation_2.PNG)

Where \\(W_M \in \mathbb R^{d \times 2d}\\) and the result is againa \\(d \times d \\) matrix

Finally, Their resulting model to resolve the one problem with the MV-RNN is RNTN(recursive Neural Tensor Netowrk) as followings:

![Socher et al. EMNLP 2013](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Text_Classification/2019-11-26-Recursive_Deep_Models_for_Semantic_Compositionality_Over_a_Sentiment_Treebank/SENT_tree_bank_equation3.PNG)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Semantic word spaces have been very useful but cannot express the meaning of longer phrases in a principled way. Further progress towards understanding compositionality in tasks such as sentiment detection requires richer supervised training and evaluation resources and more powerful models of composition. To remedy this, they introduce a Sentiment Treebank. It includes fine grained sentiment labels for 215,154 phrases in the parse trees of 11,855 sentences and presents new challenges for sentiment compositionality. To address them, they introduce the Recursive Neural Tensor Network. When trained on the new treebank, this model outperforms all previous methods on several metrics. It pushes the state of the art in single sentence positive/negative classification from 80% up to 85.4%. The accuracy of predicting fine-grained sentiment labels for all phrases reaches 80.7%, an improvement of 9.7% over bag of features baselines. Lastly, it is the only model that can accurately capture the effects of negation and its scope at various tree levels for both positive and negative phrases.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/D13-1170/">The paper: Recursive Deep Models for Semantic Compositionality Over a Sentiment Treebank. (Socher et al. EMNLP 2013)</a>
</div>

# Reference 

- Paper 
  - [ACL 2018 version: Recursive Deep Models for Semantic Compositionality Over a Sentiment Treebank. (Socher et al. EMNLP 2013)](https://www.aclweb.org/anthology/D13-1170/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [Supplementary Material: Recursive Deep Models for Semantic Compositionality Over a Sentiment Treebank. (Socher et al. EMNLP 2013)](https://www.aclweb.org/anthology/attachments/D13-1170.Attachment.pdf)
  - [Sentiment Analysis by Stanford NLP Group](https://nlp.stanford.edu/sentiment/)





























