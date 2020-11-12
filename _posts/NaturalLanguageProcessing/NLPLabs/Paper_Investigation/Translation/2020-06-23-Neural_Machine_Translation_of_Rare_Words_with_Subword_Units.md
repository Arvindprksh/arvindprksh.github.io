---
layout: post
title: Neural Machine Translation of Rare Words with Subword Units. Sennrich et al. ACL. 2016.
subtitle: Title of paper - Neural Machine Translation of Rare Words with Subword Units. Sennrich et al. ACL. 2016.
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

The decoder is a reccurent neural network that predicts a target sequence y = (\\( y_1, ..., y_n \\)). Each \\( y_i \\)  is predicted based on a recurrent hidden state \\( s_i \\), the previously predicted word \\( y_{i-1} \\), and a context vector \\( c_i \\). \\( c_i \\) is computed as a weighted sum of the annotation of \\( h_j \\). The weight of each annotation \\( h_j \\) is computed throught an alignment model \\( a_{ij} \\), which models the probablity that \\( y_i \\) is anligned to \\( x_j \\). The alignment model is a single-layer feedforward neuarl network that is learned joinlty with the rest of the network through backpropagation. 


The Byte pair Encoding(BPE) is refered to in their paper as follow:

>> a simpoe data comporession techinique that iteratively replaces the most frequent pair of bytes in a sequence with a sinlge, unused byte. They adapt this alogrithm for word segmentation. Instead of merging frequent pairs of bytes, they merge characters or shcaracter sequences.   

>> Firstly, they initialize the symbol vocabulary with the character vocabulary, and represent each word as a sequence of characters, plus a special end-of-word symble which allows us to restore the original tokenization after translation. They iteratively count all symbol pairs and replace each occurence of the most frequent pair ('A', 'B') with a new symbol ('AB'). Each merge operation produces a new symbol which represents a character n-gram. Frequent character n-grams (or whole words) are eventually merged into a single symbol, thus BPE requires no shortlist. The final symbol vocabulary is equal to the size of the initial vocabulary, plus the number of merge operations - the latter is the only hyperparameter of the algorithm.

>> The algorith m can be run on the dictionary extracted from a text, with each word being weighted by its frequency. 

They didn't consider pairs cross the boudary of word for the efficience.

In their evaluation, they used as baseline a simple segmentation of words into character n-grams, i.e. bi-gram.

They evaluate two methods of applying BPE:

 - learning two independent encodings, one for the source vocabulary and one for the target vocabulary.
 - learning the encoding on the union of the two vocabulariese they called **joint BPE**.

The detalied result can be found in [Sennrich et al. ACL 2016](https://www.aclweb.org/anthology/P16-1162/)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Neural machine translation (NMT) models typically operate with a fixed vocabulary, but translation is an open-vocabulary problem. Previous work addresses the translation of out-of-vocabulary words by backing off to a dictionary. In this paper, they introduce a simpler and more effective approach, making the NMT model capable of open-vocabulary translation by encoding rare and unknown words as sequences of subword units. This is based on the intuition that various word classes are translatable via smaller units than words, for instance names (via character copying or transliteration), compounds (via compositional translation), and cognates and loanwords (via phonological and morphological transformations). They discuss the suitability of different word segmentation techniques, including simple character ngram models and a segmentation based on the byte pair encoding compression algorithm, and empirically show that subword models improve over a back-off dictionary baseline for the WMT 15 translation tasks English→German and English→Russian by up to 1.1 and 1.3 BLEU, respectively.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P16-1162/">The paper: Neural Machine Translation of Rare Words with Subword Units. Sennrich et al. ACL 2016</a>
</div>

# Reference 

- Paper 
  - [arxiv Version: Neural Machine Translation of Rare Words with Subword Units. Sennrich et al. arXiv 2016](https://arxiv.org/abs/1508.07909)
  - [ACL Version: Neural Machine Translation of Rare Words with Subword Units. Sennrich et al. ACL 2016](https://www.aclweb.org/anthology/P16-1162/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


