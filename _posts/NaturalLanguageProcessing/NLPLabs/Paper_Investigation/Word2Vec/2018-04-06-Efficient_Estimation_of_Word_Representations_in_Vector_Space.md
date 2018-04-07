---
layout: post
title: Efficient Estimation of Word Representations in Vector Space
subtitle: Title of paper - Efficient Estimation of Word Representations in Vector Space
category: NLP papers
tags: [nlp, word2vec, word_embedding]
permalink: /2018/04/06/Efficient_Estimation_of_Word_Representations_in_Vector_Space/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

Overall, This paper is saying about comparing computational time with each other model, and extension of NNLM which turns into two step. one is training word vector and then the other step is using the trained vector on The NNLM.

In estimaiting continuous representations of words including the well-known Latent Semantic Analysis(LSA) and Latent Dirichlet Allocation(LDA). 

They are saying the neural network is performing better thatnn LSA for preserving linear regularities among words. even LDA becomes computationally very expensive on large data sets.

In this paper, the computational time complexity is defined as follows: 

> The training complexity is proportional to :    
> O = E * T * Q

Where E is number of the training epochs, T is the number of the words in the training set and Q is defined further for each model architecture.

They are saygint when you compute computational time, it heavily depens on the number of output units or hidden layer units. 

The best expensive one of two units is first output units, after that, the second one is hidden layer.

So They implemented hiararchical softmax with huffman tree to reduce  output unit. but the bottleneck situation remains in hidden layer. 

Finally they got rid of the hidden layer, so their model heavily depends on the efficiency of the softmax normalizations.

The models are called CBOW(continuous bag of word) and skip gram. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2018-04-06-Efficient_Estimation_of_Word_Representations_in_Vector_Space/Word2vec_models.png)

Let's see an examle they used for testing syntactic and semantic questions. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2018-04-06-Efficient_Estimation_of_Word_Representations_in_Vector_Space/Example_of_five_types_of_semantic_and_nine_types_of_syntactic_qeustion.png)


<div class="alert alert-success" role="alert"><i class="fa fa-check-square-o"></i> <b>Tip: </b>
They are providing a set of test about syntactic and semantic regularities, The test set is available at <a href="http://www.fit.vutbr.cz/~imikolov/rnnlm/word-test.v1.txt">word-test.v1.txt</a><br/>
Some of the resulting word vectors were made available for future research and comparison : <br/>
  - <a href="http://ronan.collobert.com/senna/">Senna</a><br/>
  - <a href="http://metaoptimize.com/projects/wordreprs/">Metaoptimize-wordreprs</a><br/>
  - <a href="http://www.fit.vutbr.cz/~imikolov/rnnlm/">RNNLM</a><br/>
  - <a href="http://ai.stanford.edu/~ehhuang/">AI stanford</a><br/>
</div>


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
It is was found that computational time depens on output and hidden layer, But In thi paper, they used hiarachical softmax for output layer and got rid of hidden layer. it is totally for reducing the computational time. <br/>
Their idea to create new model for the continous represenation of words is from that neural network language model can successfully trained in two steps: first continuous word vectors are learned using simple model, and then the N-gram NNLM is trained on top of these distributed representations of words.  <br/>
They introduced two model based on their ideas. those are called one is CBOW and The other is Skip gram. <br/>

CBOW : predicting a word with future and history words before and after a middle word, so The weight matrix between the input and the projection layer is shared for all word positions in the same way in the NNLM. <br/>
Skip gram : this model used each current words as an input to a log-linear classifier with continuous projections layer, and predict words within a certain range before and after the current word.  <br/>
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1301.3781v3">The paper: Efficient Estimation of Word Representations in Vector Space</a>
</div>

# Reference 

- Paper 
  - [Efficient Estimation of Word Representations in Vector Space](https://arxiv.org/abs/1301.3781v3)
  - [word test set: syntactic and semantic regularities](http://www.fit.vutbr.cz/~imikolov/rnnlm/word-test.v1.txt) 
 
- Quoar
  - [What is meant by a ditributed representation in Deep learning](https://www.quora.com/Deep-Learning-What-is-meant-by-a-distributed-representation) 
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
- My github repository to translate the test set of semantic and syntactic into Korean test set
  - [Hyunyoung2 Korean test set v1](https://github.com/hyunyoung2/Hyunyoung2_Korean_test_set_v1)
