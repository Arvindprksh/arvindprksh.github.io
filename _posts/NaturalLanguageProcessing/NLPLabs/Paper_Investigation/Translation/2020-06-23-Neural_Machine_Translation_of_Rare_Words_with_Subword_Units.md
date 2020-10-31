---
layout: post
title: Neural Machine Translation of Rare Words with Subword Units
subtitle: Title of paper - Neural Machine Translation of Rare Words with Subword Units
category: NLP papers - Translation
tags: [translation]
permalink: /2020/06/23/Neural_Machine_Translation_of_Rare_Words_with_Subword_Units/
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

This is a brief summary of paper for me to study and organize it, [Neural Machine Translation of Rare Words with Subword Units. Sennrich et al. ACL 2016](https://www.aclweb.org/anthology/P16-1162/) I read and studied. 
{% include MathJax.html %}

This paper introduce the subword unit into Neural Machine translation task to well handle rare or unseen words. 

In other words, On the translation task, the translation of rare words is an open problem.

They said as follows:

>> The vocabulary of neural models is typically limited to 30,000–50,000 words, but translation is an open-vocabulary problem, and especially for languages with productive word formation processes such as agglutination and compounding, translation models require mechanisms that go below the word level.

On translation task, they verify the suitability of different word segmentation techniques, including simple character n-gram models and a segmentation based on the **byte pair encoding** compression algorithm.

In order to generate segmentation to subword units, they used an algorithm, also known as compressiont algorithm, byte-pair encoding.

This paper is based on the intuition that various word classes arr translatable via smaller units that words, for example name (via character copying or transliteration), compounds (via compoosition translation), and cognates and loanwords (vias phonological and morphological transofrmations).


They argue this paper has two main contributions:

- We show that open-vocabulary neural machine translation is possible by encoding (rare) words via subword units. We find our architecture simpler and more effective than using large vocabularies and back-off dictionaries (Jean et al., 2015; Luong et al., 2015b).

- We adapt byte pair encoding (BPE) (Gage, 1994), a compression algorithm, to the task of word segmentation. BPE allows for the representation of an open vocabulary through a fixed-size vocabulary of variable-length character sequences, making it a very suitable word segmentation strategy for neural network models.


They use neural network-based machine translation model with recurrent neural network such as [Bahdanau et al. (2015)](https://arxiv.org/abs/1409.0473).

The nueral machine translation system is implemented as an encoder-decoder network with recurrent enural network.

The encoder is a bidirectional neural network with gated recurrent units ([Cho et tl., 2014](https://arxiv.org/abs/1406.1078)) that read as in put sequence x = (\\( x_1, ..., x_m \\)) and calcuates a forward sequence of hidden states (\\( \overrightarrow h_1, ..., \overrightarrow h_m \\)), and a backward sequence (\\(\overleftarrow h_1, ..., \overleftarrow h_m \\)). The hidden state \\( \overrightarrow h_j \\) and \\( \overleftarrow h_j \\) are concatenated to obtain the annotation vector \\( h_j \\).

The decoder is a reccurent neural network that predicts a target sequence y = (\( y_1, ..., y_n \)). Each \( y_i \)  is predicted based on a recurrent hidden state \( s_i \), the previously predicted word \( y_{i-1} \), and a context vector \( c_i \). \( c_i \) is computed as a weighted sum of the annotation of \( h_j \). The weight of each annotation \( h_j \) is computed throught an alignment model \( a_{ij} \), which models the probablity that \( y_i \) is anligned to \( x_j \). The alignment model is a single-layer feedforward neuarl network that is learned joinlty with the rest of the network through backpropagation. 





<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Neural machine translation (NMT) models typically operate with a fixed vocabulary, but translation is an open-vocabulary problem. Previous work addresses the translation of out-of-vocabulary words by backing off to a dictionary. In this paper, they introduce a simpler and more effective approach, making the NMT model capable of open-vocabulary translation by encoding rare and unknown words as sequences of subword units. This is based on the intuition that various word classes are translatable via smaller units than words, for instance names (via character copying or transliteration), compounds (via compositional translation), and cognates and loanwords (via phonological and morphological transformations). They discuss the suitability of different word segmentation techniques, including simple character ngram models and a segmentation based on the byte pair encoding compression algorithm, and empirically show that subword models improve over a back-off dictionary baseline for the WMT 15 translation tasks English→German and English→Russian by up to 1.1 and 1.3 BLEU, respectively.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P16-1162/">The paper: Neural Machine Translation of Rare Words with Subword Units. Sennrich et al. ACL 2016</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Neural Machine Translation of Rare Words with Subword Units. Sennrich et al. arXiv 2016](https://arxiv.org/abs/1508.07909)
  - [ACL 2016 version: Neural Machine Translation of Rare Words with Subword Units. Sennrich et al. ACL 2016](https://www.aclweb.org/anthology/P16-1162/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


