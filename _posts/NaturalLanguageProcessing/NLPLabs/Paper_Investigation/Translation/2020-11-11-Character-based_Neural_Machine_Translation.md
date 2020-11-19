
---
layout: post
title: Character-based Neural Machine Translation
subtitle: Title of paper - Character-based Neural Machine Translation
category: NLP papers - Translation
tags: [translation]
permalink: /2020/11/11/Character-based_Neural_Machine_Translation/
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

This is a brief summary of paper for me to study and organize it, [Character-based Neural Machine Translation (Ling et al., arXiv 2015.)](https://arxiv.org/abs/1511.04586)
 that I read and studied. 
{% include MathJax.html %}


This paper propose a neural translation model that learns to encode and decode using character level. 

In other words, they used composition model to make character embedding into word embedding in input and output layer.

First of all, they designed a attention-based neural translation model presented by [Bahdanau et al.(2015)](https://arxiv.org/abs/1409.0473)  which is described as follows:

![Ling et al., arXiv 2015.](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2020-11-11-Character-based_Neural_Machine_Translation/basic_model.PNG)

Since the attention-based neural machine translation model is word-based neural network model, it has a problem which has to bottleneck of softmax. 

In order for them to resolve this problem, they adapt the word-based neural machine translation model to operate over character sequences rather than word sequence.

However, they retain the notion of words when using the character embedding in each input and output layer. 


In input layer, they use bidirectional LSTM to represent character sequence into word embedding like this:

![Ling et al., arXiv 2015.](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2020-11-11-Character-based_Neural_Machine_Translation/input_embedding.PNG)

Their composition model for word vector from characters builds a representation of the words using characters, by reading character left-to-right and vice versa. 

The representation of the word is obtained by combining each final state from forward LSTM and backward LSTM.


In output layer, they also use bidirectional LSTM such as the method of input layer. The figure belwo shows the generation of words from characters in output layer:

![Ling et al., arXiv 2015.](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2020-11-11-Character-based_Neural_Machine_Translation/output_embedding.PNG)

The disticntion between input and output layer is that the output use the alignment and output context. 


For detailed experiment analysis, you can found in [Character-based Neural Machine Translation (Ling et al., arXiv 2015)](https://arxiv.org/abs/1511.04586)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>

</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1511.04586">The paper: Character-based Neural Machine Translation (Ling et al., arXiv 2015)</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: Character-based Neural Machine Translation (Ling et al., arXiv 2015)](https://arxiv.org/abs/1511.04586)

  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


