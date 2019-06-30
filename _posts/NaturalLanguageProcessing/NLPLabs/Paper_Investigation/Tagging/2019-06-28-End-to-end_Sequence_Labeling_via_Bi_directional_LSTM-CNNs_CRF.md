---
layout: post
title: End-to-end Sequence Labeling via Bi-directional LSTM-CNNs-CRF
subtitle: Title of paper - End-to-end Sequence Labeling via Bi-directional LSTM-CNNs-CRF
category: NLP papers
tags: [nlp, word2vec, tagging]
permalink: /2019/06/28/End-to-end_Sequence_Labeling_via_Bi_directional_LSTM-CNNs_CRF/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

This paper, [End-to-end Sequence Labeling via Bi directional LSTM-CNNs-CRF,(Xuezhe Ma and Eduard Hovy 2016)](https://www.aclweb.org/anthology/P16-1101), proposed a neural network architectural for sequence labeling, which is NER and POS.

Their models is end-to-end models relying on no task-specific resources, feature engineering or data pre-procsessing.

They use convolutiona neural network to extract morphogical information from characters of words and encode it inot neural representations as follows.

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/tagging/2019-06-28-End-to-end_Sequence_Labeling_via_Bi_directional_LSTM-CNNs_CRF/CNN_with_char.JPG)

The whole model architecture they argued is the following

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/tagging/2019-06-28-End-to-end_Sequence_Labeling_via_Bi_directional_LSTM-CNNs_CRF/BLSTM_CNN_CRF.JPG)

As you can see their model above, they used character-level representation by concating word vector as input of Bidirectional LSTM.

on decoding label, they used conditional random field(CRF) which is beneficail to consider the correlations between labels in neighborhoods and jointly decode the best chain of labels for a given input sequence.

They used a variety of deeplearnig technique like dropout and pertrained word embedding.

Also they argued that their model can be further improved by exploring multi-task learnig approaches to combine more useful and correlated information as the future of works. 

For example, they said their model can be jointly trained with both the POS and NER tags to improve the intermediate representation learned from their network.

<div class="alert alert-success" role="alert"><i class="fa fa-check-square-o"></i> <b>Tip: </b>
CNN is an effective approach to extract morphological information (like the prefix or suffix of a word) from characters of words and encode it into neural representations
</div>


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
State-of-the-art sequence labeling systems traditionally require large amounts of task-specific knowledge in the form of handcrafted features and data pre-processing. In this paper, we introduce a novel neutral network architecture that benefits from both word- and character-level representations automatically, by using combination of bidirectional LSTM, CNN and CRF.
their model is truely end-to-end, requiring no feature engineering or data pre-processing.
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1603.01354">The paper: End-to-end Sequence Labeling via Bi-directional LSTM-CNNs-CRF on arXive version</a>
  <a href="https://www.aclweb.org/anthology/P16-1101">The paper: End-to-end Sequence Labeling via Bi-directional LSTM-CNNs-CRF on ACL version</a>
</div>



<div id="tutorial-section">

  <div id="tutorial-title">GloVe Youtube</div>

  <ul class="nav nav-pills">
    <li class="active"><a data-toggle="tab" href="#refrigerator">Youtube</a></li>
    <li><a data-toggle="tab" href="#refrigerator_concept">DeepLearning ai</a></li>
  </ul>

  <div class="tab-content">
    <div id="refrigerator" class="tab-pane fade in active">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/BBYnIoGrf8Y" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
    <div id="refrigerator_concept" class="tab-pane fade">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/ArPaAX_PhIs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
  </div>
</div>

# Reference 

- Paper 
  - [End-to-end Sequence Labeling via Bi-directional LSTM-CNNs-CRF on arXive version](https://arxiv.org/abs/1603.01354)
  - [End-to-end Sequence Labeling via Bi-directional LSTM-CNNs-CRF on ACL version](https://www.aclweb.org/anthology/P16-1101)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
- Example with tensorflow
  - [WILDML's Understanding Convolutional Neural Networks for NLP](http://www.wildml.com/2015/11/understanding-convolutional-neural-networks-for-nlp/)
  - [stackexchange cnn translation invariant](https://stats.stackexchange.com/questions/208936/what-is-translation-invariance-in-computer-vision-and-convolutional-neural-netwo)
  - [stackoverflow understanding 1D, 2D, 3D in convolutional Neural Network](https://stackoverflow.com/questions/42883547/intuitive-understanding-of-1d-2d-and-3d-convolutions-in-convolutional-neural-n)
  - [CNN 1D, 2D on stackexchange](https://stats.stackexchange.com/questions/292751/is-a-1d-convolution-of-size-m-with-k-channels-the-same-as-a-2d-convolution-o)
  
