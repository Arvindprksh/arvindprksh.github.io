---
layout: post
title: Character-Aware Neural Language Models
subtitle: Title of paper - Character-Aware Neural Language Models
category: NLP papers
tags: [neural_network, memory_network]
permalink: /2018/11/30/Character-Aware_Neural_Language_Models/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

<!-- \\( X_{i}=\sum_{k}X_{ik} \\) -->

{% include MathJax.html %}

This article is just brief summary of [Character-Aware Neural Language Models](https://arxiv.org/abs/1508.06615v4) and posting for me to study what the memory network is. 

Their neural network consists of CNN for character-level as input, also high-way network before LSTM and finally LSTM-LM(Language model).

A Statical [Languae model](https://en.wikipedia.org/wiki/Language_model) is probability distribution over sequences of words. Given such a sequence like of length m, LM assigns a probability  \\( P(w_{1}, ....... , w_{m}) \\) to the whole sequence.

This task of Language model on Natural Languge is difficult, becuase there is no specification of the usages of natural Language.

Or another definition of LM is probabilistic that are able to predict the next word in the sequence given the words that precede it. 

the definition that LM predicts the next words given a sequence of words is from [Machine Learning Mastery](https://machinelearningmastery.com/statistical-language-modeling-and-neural-language-models/)

let's say the length of a sequence is 3, if we want to predict fourth word. the pobability of next word is conditional probability distribution is like :

- \\(  P(w_{3} \| w_{1}, w_{2}) = P(w_{1})\*P(w_{2}\|w_{1})\*P(w_(3)\|w_{1}, w_{2})  \\)

they estimate the probability of LM withe their model. 

Let's see their model!! 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Language_Model/2018-11-30-Character-Aware_Neural_Language_Models/Character-Aware_Neural_Language_Models.png)

They used CNN, Highway network and LSTM.

in particular, Let's see the highway network, recently proposed by Srivastava et al.(2015).

one layer of a highway nework does the following :

- \\( z = t \odot g(W_{H}y + b_{H}) + (1 - t) \odot y \\) where g is a nonliearity.

- \\( t = \sigma(W_{T}y + b_{T}) \\) is called tranform gate, and (1 - t) is called carry gate.


Also let's the result of Learned word representation

Word embeddings obtained through NLMs show you the property whereby semantically close words are likewise close in the induced vector space. 

Let's see the figure below with this intution about Word embeddings.

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Language_Model/2018-11-30-Character-Aware_Neural_Language_Models/Character-Aware Neural Language Models_figure2.png)


![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Language_Model/2018-11-30-Character-Aware_Neural_Language_Models/haracter-Aware Neural Language Models_table6.png)


Also, I realized What the hierarchical softmax is.


Let's see the hierarchical softmax they used 

they pcik the number of cluster  \\( c = \lceil \sqrt{\|V\|} \rceil \\), and randomly split \\( V \\)  into mutually exclusive and collectively exhastive subsets \\( V_{1}, ....... , V_{c} \\) of approximately equal size. 

The \\( Pr(W_{i} = j \| W_{1:t}) = \[ \frac{exp(h_{t} \cdot s^r + t^r)}{\sideset{_}{_r'=1^c}\sum exp(h_{t} \cdot s^r' + t^r')} \times \frac{exp(h_{t} \cdot P_{r}^j + q_{r}^j)}{\sideset{_}{_j'\inV_{r}}\sum exp(h_{t} \cdot P_{r}^j' + q_{r}^j')} \] \\)

Wherer r is the cluster index such that \\( j \in V_{r} \\). The first term is imple the porbability of picking cluster r, and the second term is the probability of picking word j given that cluster r is picked.


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
they used CNN network for LM(Language model) on morphologically richer languages depending on character-level inputs. But. Predications are still word-level as output. the whole structure of the network is convolutional neural network(CNN) and a highway network over the characters, whose output is given to a long short-term model(RNN-LM). the analysis of word representations obtained from the character composition part of the model reveals that the model is able to encode, from character only, both semantic and orthographic information. 
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1508.06615v4">The paper: Character-Aware Neural Language Models</a>
</div>

# Reference 

- Paper 
  - [Character-Aware Neural Language Models](https://arxiv.org/abs/1508.06615v4)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
 
- For your information
  - [What is the language model on wikipedia](https://en.wikipedia.org/wiki/Language_model)
  - [affine transformation on stackexchange](https://datascience.stackexchange.com/questions/13405/what-is-affine-transformation-in-regards-to-neural-networks)
  - [affine transforamtion on Medium](https://medium.com/wwblog/transformation-in-neural-networks-cdf74cbd8da8)
  - [Language model on Machine Learning Mastery](https://machinelearningmastery.com/statistical-language-modeling-and-neural-language-models/)
  - [list of Latex symbol on LaTeX Wiki](http://latex.wikia.com/wiki/List_of_LaTeX_symbols)






























