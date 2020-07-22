---
layout: post
title: Towards Universal Paraphrastic Sentence Embeddings
subtitle: Title of paper - Towards Universal Paraphrastic Sentence Embeddings
category: NLP papers - Sentence Embedding
tags: [neural network, sentence embedding]
permalink: /2020/07/21/Towards_Universal_Paraphrastic_Sentence_Embeddings/
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

This is a brief summary of paper for me to study and arrange it, [Towards Universal Paraphrastic Sentence Embeddings. Wieting et al. ICLR 2016](https://arxiv.org/abs/1511.08198) I read and studied. 
{% include MathJax.html %}


They propose six compositional function on word sequence for text similarity task. 

They argued that the simplest averaging model is competitive for universal sentence embeddings. 

They compared six compostionality function for sentence embedding. 


From now on, I will explain the six compoistion models which they used. 

Their purpose is to represent sequences into a low-dimenstional space and they experimented with six models of increasing complexity. 

- The simplest model embeds a word sequence \\(x = <x_1, x_2, ..., x_n>\\) by averaging the vectors of its tokens. The only parameters learned by this model are the word embedding matrix $W_w$
:  

$$g_{paragram-phrase}(x) = \frac{1}{n} \sum_{i=1}^{n}W_{w}^{x_i}$$  

Where \((W_{w}^{x_i}\)) is the word embedding for word \((x_i\)). They call the learned embeddins PARAGRAM-PHARASE embeddings.

- The second model is to projection the simplest model as follows:

$$g_{proj}(x) = W_p (\frac{1}{n}\sum_{i=1}^{n} W_{w}^{x_i}) + b$$

Where \((W_p\)) is the projections matrix and \((b\)) is a bias vector.

- The third model is the deep averaging network which is generalization of the above models that uses mulitple layers as well as nonlinear activation functions.

- The fourth model is a standard recurrent network(RNN) with randomly initialized weight matrices and nonlinea activations:

$$h_i = f(W_xW_w^{x_t} + W_hh_{t-1}+b)$$

$$g_{RNN}(x) = h_{-1}$$

where \((f\)) is the activation function (either tanh or rectified linear unit: the choice is tuned), \((W_x\)) and \((W+h\)) are parameter matrices \((b\)) is a bias vector, and \((h_{-1}\)) refers to the hidden vector of the last token.

- The fifth model is a special RNN which we call an **identity-RNN**. In the **identity-RNN**, the weight matrices are initialized to identity, the bias is initialized to zero, and the activation is the identity function. They divide the final output vector of the **identity-RNN** by the number of tokens in the sequence.

Thus, before any updates to the parameters, the **identity-RNN** simply averages the word embeddings. They also regularize the **identity-RNN** parameters to their initial values. That is, the idea with high regularization is  the **identity-RNN** is simply averaging word embedding. 

However it is a richer architecture and can take into account word order and hopefully improve upon the averaging baseline.

- The sixth model is long short-term memory(LSTM) which is the mose complex in their compositionality function for sentence embedding. The LSTM is peephole version.

$$i_t = \sigma(W_{xi}W_w^{x_t} + W_{hi}h_{t-1} + W_{ci}c_{t-1} + b_i)$$

$$f_t = \sigma(W_{xf}W_w^{x_t} + W_{hf}h_{t-1} + W_{cf}c_{t-1} + b_f)$$

$$c_t = f_tc_{t-1} + i_ttanh(W_{xc}W_w^{x_t} + + W_{hc}h_{t-1} + b_c)$$

$$o_t = \sigma(W_{xo}W_w^{x_t} + W_{ho}h_{t-1} + W_{co}c_{t} + b_o)$$

$$h_t = o_ttanh(c_t)$$

$$g_{LSTM}(x) = h_{-1}$$

where \((\sigma\)) is the logistic sigmoid funciton. They found that the choice of whether or not ot include the output gate had a significant impact on performance, so they used two versions of the LSTM model, one with the output gate and one without. 

In their experiment, for all models above, they learn the word embeddings themselves, denoting the trainable word ebmedding parameters by \((W_w\)). They denote all other trainable parameters by \((W_c\)) ("compositional parameters"), though the PARAGRAM_PHRASE model has no compositional paramters. They initialized \((W_w\)) using some embeddings pretrained from large corpora.

In their result, they empirically demonstrated the averaging model is better in in-domain data but LSTM in out-domain data.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They consider the problem of learning general-purpose, paraphrastic sentence embeddings based on supervision from the Paraphrase Database. They compare six compositional architectures, evaluating them on annotated textual similarity datasets drawn both from the same distribution as the training data and from a wide range of other domains. They find that the most complex architectures, such as long short-term memory (LSTM) recurrent neural networks, perform best on the in-domain data. However, in out-of-domain scenarios, simple architectures such as word averaging vastly outperform LSTMs. Their simplest averaging model is even competitive with systems tuned for the particular tasks while also being extremely efficient and easy to use. In order to better understand how these architectures compare, they conduct further experiments on three supervised NLP tasks: sentence similarity, entailment, and sentiment classification. They again find that the word averaging models perform well for sentence similarity and entailment, outperforming LSTMs. However, on sentiment classification, they find that the LSTM performs very strongly—even recording new state-of-the-art performance on the Stanford Sentiment Treebank.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/N16-1162/">The paper: Learning Distributed Representations of Sentences from Unlabelled Data. Hill et al. NAACL 2016</a>
</div>

# Reference 

- Paper 
  - [arXiv version: Towards Universal Paraphrastic Sentence Embeddings. Wieting et al. ICLR 2016](https://arxiv.org/abs/1511.08198)
  - [ICRL 2016 version: Towards Universal Paraphrastic Sentence Embeddings. Wieting et al. 2016](https://www.aclweb.org/anthology/N16-1162/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    






























