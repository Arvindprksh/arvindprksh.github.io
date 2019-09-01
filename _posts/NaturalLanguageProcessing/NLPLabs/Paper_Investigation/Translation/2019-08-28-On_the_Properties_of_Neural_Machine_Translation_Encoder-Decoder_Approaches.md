---
layout: post
title: On the Properties of Neural Machine Translation: Encoder-Decoder Approaches
subtitle: Title of paper - On the Properties of Neural Machine Translation: Encoder-Decoder Approaches
category: NLP papers - Translation
tags: [neural_network, translation]
permalink: /2019/08/28/On_the_Properties_of_Neural_Machine_Translation_Encoder-Decoder_Approaches/
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

This is a brief summary of paper for me to note it, [On the Properties of Neural Machine Translation: Encoder-Decoder Approaches, Cho et al. (2014)](https://www.aclweb.org/anthology/W14-4012)

{% include MathJax.html %}

They analyzed the properties of machine translation model based on neural network. 

Since most of neural-netwrok-based translation model is sequence-to-seqeunc model, the translation model has a encoder and a decoder. 

![Cho et al. (2014)](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2019-08-28-On_the_Properties_of_Neural_Machine_Translation_Encoder-Decoder_Approaches/Sequence_to_sequence.JPG)

Encoder summarize input sentence (source sentence) into a fixed-length vector and Decoder generate output sentence (target sentence).

To sum up their results. When the number of unkown words and the length of sentence increase, the performance is degraded.

Above all, before entering to what kind of encoder they use, note that they use an RNN with gated hidden units (GRU) as a decoder.

Let's see the Recurrent Neural Network with Gated Hidden Neurons. 

![Cho et al. (2014)](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2019-08-28-On_the_Properties_of_Neural_Machine_Translation_Encoder-Decoder_Approaches/Recurrent_network.JPG)


A recurrent neural network works on a variable-length sequence \\(x = (x_1,X_2,...,X_T)\\) by maintaining a hidden state **h** over time. At each timestip t, the hidden state \\(h^{(t)}\\) is updated by:

$$h^{t} = f(h^{t-1}, x_t)$$

where **f** is an activation function. Often **f** is as simple as performing a linear transformation on the input vectors, summing them, and applying an element-wise logisitic sigmoid function.

They used new activation fucntion which augments the usual logisitc sigmoid activation function with two gating units called reset gate, **r** and update gate, **z**. Each gate depends on the previous hidden state \\(h^{t-1}\\), and the current intput , \\(x_t\\) controls the flow of information.

Let's see the Gated Recursive Convolutional Neural Network. 

![Cho et al. (2014)](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2019-08-28-On_the_Properties_of_Neural_Machine_Translation_Encoder-Decoder_Approaches/Gated_Recursive_Convolution_Neural_Network.JPG)

They also introduce a new binary convolutional neural network whose weights are recursively applied to the input sequence until it outputs a single fixed-length vector. 

Let \\(x = (x_1, x_2, ... , X_T) \\) be an input sequence, where \\(x_t \in \mathbbR^d\\). The proposed gated recursive convolutional neural network consists fo four weight matrices \\(W^l, W^r, G^l\\) and \\(G^r\\). At each recursion level \\(t \in [1, T-1]\\), the activation of the j-th hidden unit \\(h_j^{t}\\) is computed by:

$$ \begin{matrix} h_j^{(t)} = w_c\bar{h_j^{(t)} + w_l{h_{j-1}^{(t-1)} + w_r{h_j^{(t-1)} &  (1)    \end{matrix}$$

where \\(w_c, w_l\\) and \\(w_r\\) are the values of a gater that sum to 1. The hidden unit is initialized as 

$$ \begin{matrix} h_j^{(0)} = Ux_j &  (2)    \end{matrix}$$

Where **U** projects the input into a hidden space.

The new activation \\(\barh_j^{t}\\) is computed as usual :

$$ \begin{matrix} \barh_j^{(t)} = \sigma(W^lh_{j-1}^{(t)} + W^rh_j^{(t)}) &  (3)    \end{matrix}$$

Where \\(\sigma\\) is an element-wise nonlinearity.

The gating coefficients \\(w's\\) are computed by:

$$ \begin{matrix} w_c \\ w_l \\ w_r \\ \end{matrix} = \frac{Z}{1}exp(G^lh_{j-1}^{(t)} + G^rh_j^{(t)}) $$

Where \\(G^l, G^r \in \mathbbR^{3xd}\\) and Z is normalized term :

$$ \begin{matrix} Z = \sum_{k=1}^{3}[exp(G^lh_{j-1}^{(t)} + G^rh_j^{(t)})]_k &  (3)    \end{matrix}$$

According to this activation, one can think of the activation of a single node at recursion level **t** as a choice between either a enw activation computed from both left and right children, the activation from the left child, or the activation from right child. 

The choice allows the overal structure of the recursive convolution to change adaptively with respect to an input sample.


When they generate target sentence, they use a basic form of beam-search to find a translation that maximizes the conditional probability given by a specific models.

it is better than [Greed search](https://youtu.be/Er2ucMxjdHE).  

If you want to know what beam-search is, see the following (e.g. Youtube lecture)

<div id="tutorial-section">

  <div id="tutorial-title">Youtube of Deeplearning Ai</div>

  <ul class="nav nav-pills">
    <li class="active"><a data-toggle="tab" href="#refrigerator">Beam search</a></li>
    <li><a data-toggle="tab" href="#refrigerator_concept">Refinements to beam search</a></li>
    <li><a data-toggle="tab" href="#refrigerator_concept2">Error Analysis of Beam Search</a></li>
  </ul>

  <div class="tab-content">
    <div id="refrigerator" class="tab-pane fade in active">
      <iframe width="1205" height="753" src="https://www.youtube.com/embed/RLWuzLLSIgw?list=PLCSzVeDv57Z1y0uWZXYX2kq5UUpqA0Mk2" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
    <div id="refrigerator_concept" class="tab-pane fade">
      <iframe width="1205" height="753" src="https://www.youtube.com/embed/gb__z7LlN_4?list=PLCSzVeDv57Z1y0uWZXYX2kq5UUpqA0Mk2" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
     <div id="refrigerator_concept2" class="tab-pane fade">
      <iframe width="1205" height="753" src="https://www.youtube.com/embed/ZGUZwk7xIwk?list=PLCSzVeDv57Z1y0uWZXYX2kq5UUpqA0Mk2" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe> 
     </div>
  </div>
 
</div>


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Neural machine translation is a relatively new approach to statistical machine translation based purely on neural networks. The neural machine translation models often consist of an encoder and a decoder. The encoder extracts a fixed-length representation from a variable-length input sentence, and the decoder generates a correct translation from this representation. In thi spaper, they focus on analyzing the properties of the neural machine translation using two models; RNN Encoder–Decoder and a newly proposed gated recursive convolutional neural network. they show that the neural machine translation performs relatively well on short sentences without unknown words, but its performance degrades rapidly as the length of the sentence and the number of unknown words increase. Furthermore, we find that the proposed gated recursive convolutional network learns a grammatical structure of a sentence automatically.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/W14-4012">The paper: On the Properties of Neural Machine Translation: Encoder-Decoder Approaches, Cho et al. (2014)</a>
</div>

# Reference 

- Paper 
  - [ArXiv version: On the Properties of Neural Machine Translation: Encoder-Decoder Approaches, Cho et al. (2014)](https://arxiv.org/abs/1409.1259)
  - [ACL version: On the Properties of Neural Machine Translation: Encoder-Decoder Approaches, Cho et al. (2014)](https://www.aclweb.org/anthology/W14-4012)
  
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)

- For your information
  - [Beam Search - A Search Strategy on HACKERNOON](https://hackernoon.com/beam-search-a-search-strategy-5d92fb7817f)
