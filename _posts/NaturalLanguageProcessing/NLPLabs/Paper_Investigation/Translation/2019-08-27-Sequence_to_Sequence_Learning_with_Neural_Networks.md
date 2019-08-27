---
layout: post
title: Sequence to Sequence Learning with Neural Networks
subtitle: Title of paper - Sequence to Sequence Learning with Neural Networks
category: NLP papers - Translation
tags: [neural_network, translation]
permalink: /2019/08/27/Sequence_to_Sequence_Learning_with_Neural_Networks/
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

This is a brief summary of paper for me to note it, [Sequence to Sequence Learning with Neural Networks, Sutskever et al. (2014)](https://arxiv.org/abs/1409.3215) 

{% include MathJax.html %}

Their architecture is end-to-end neural network with two LSTM(one for input sequence, another for output sequence). 

The goal of the LSTM is to estimate the conditional probability \\(p(y_1, . . . , y_{T′} |x_1, . . . , x_T)\\) where \\((x_1, . . . , x_T )\\) is an input sequence and \\(y_1, . . . , y_{T′}\\) is its corresponding output sequence whose length \\(T′\\) may differ from \\(T\\). The LSTM computes this conditional probability by first obtaining the fixeddimensional representation \\(v\\) of the input sequence \\((x_1, . . . , x_T )\\) given by the last hidden state of the LSTM, and then computing the probability of \\(y_1, . . . , y_{T′}\\) with a standard LSTM-LM formulation whose initial hidden state is set to the representation \\(v\\) of \\(x_1, . . . , x_T\\)

$$p(y_1,...,y_{T'}|x_1,...,x_T) = \prod_{t=1}^{T'} p(y_t+v, y_1,...,y_{t-1})$$

In this equation, each \\(p(y_t|v, y_1, . . . , y_{t−1})\\) distribution is represented with a softmax over all the words in the vocabulary. Note that we require that each sentence ends with a special end-of-sentence symbol “<EOS>”, which enables the model to define a distribution over sequences of all possible lengths. The overall scheme is outlined in figure below, where the shown LSTM computes the representation of “A”, “B”, “C”, “<EOS>” and then uses this representation to compute the probability of “W”, “X”, “Y”, “Z”, “<EOS>”.

The one below is simple illustration of their architecture.

![Sutskever et al. (2014)](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2019-08-27-Sequence_to_Sequence_Learning_with_Neural_Networks/sequence_to_sequence_learning_with_neural_networks.JPG)

This paper for translation task in NLP field propose three key points.

 - How to deal with sequence data like text which has a variable length sequence in both input and output with two LSTMs(i.e. one is encoder, the other is decorder)
 - They use a reversed input(source sequence) to tackle long range temporal dependencies but target sequences are not reversed.
 - They use left-to-right beam search(i.e. beam size of 1, 2, or 12) in decoder for the better target sequences which is maaintains a small number B of partial hypotheses.

They implemente their model on the WMT'14 English to French translation task.

For train and test time, they were able to do well on long sentences **because they reversed the order of words in the source sentence but not the target sentences in the training and test set.**

As you can see below, **the representation shows that the representations are sensitive to the order of words, while being fairly insensitive to the replacement of an active voice with a pssive voice.**

![Sutskever et al. (2014)](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2019-08-27-Sequence_to_Sequence_Learning_with_Neural_Networks/sequence_to_sequence_learning_with_neural_networks_pca.JPG)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Deep Neural Networks (DNNs) are powerful models that have achieved excellent performance on difficult learning tasks. Although DNNs work well whenever large labeled training sets are available, they cannot be used to map sequences to sequences. In this paper, they present a general end-to-end approach to sequence learning that makes minimal assumptions on the sequence structure. their method uses a multilayered Long Short-Term Memory (LSTM) to map the input sequence to a vector of a fixed dimensionality, and then another deep LSTM to decode the target sequence from the vector. Additionally, the LSTM did not have difficulty on long sentences. The LSTM also learned sensible phrase and sentence representations that are sensitive to word order and are relatively invariant to the active and the passive voice. Finally, they found that reversing the order of the words in all source sentences (but not target sentences) improved the LSTM’s performance markedly, because doing so introduced many short term dependencies between the source and the target sentence which made the optimization problem easier.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://papers.nips.cc/paper/5346-sequence-to-sequence-learning-with-neural-networks.pdf">The paper: Sequence to Sequence Learning with Neural Networks, Sutskever et al. (2014)</a>
</div>

# Reference 

- Paper 
  - [ArXiv version: Sequence to Sequence Learning with Neural Networks, Sutskever et al. (2014)](https://arxiv.org/abs/1409.3215)
  - [NIPS version: Sequence to Sequence Learning with Neural Networks, Sutskever et al. (2014)](https://papers.nips.cc/paper/5346-sequence-to-sequence-learning-with-neural-networks.pdf)
  
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)

