---
layout: post
title: QANet- Combining Local Convolution with Global Self-Attention for Reading Comprehension
subtitle: Title of paper - QANet- Combining Local Convolution with Global Self-Attention for Reading Comprehension
category: NLP papers - Question Answering
tags: [neural network, machine reading comprehension, question answering]
permalink: /2020/08/25/QANet_Combining_Local_Convolution_with_Global_Self-Attention_for_Reading_Comprehension/
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

This is a brief summary of paper for me to study and organize it, [QANet: Combining Local Convolution with Global Self-Attention for Reading Comprehension. Yu et al. ICLR 2018](https://openreview.net/forum?id=B14TlG-RW/) I read and studied. 
{% include MathJax.html %}

This paper proposed data augmentation technique and model, which execulsively used convolution and self-attention, for question answering task. 

Let's first start formulate the reading comprehension task:

**Machine Reading Comprehension Formulation:** The The reading comprehension task considered in this paper, is defined as follows. Given a context paragraph with n words C = {\\(c_1, c_2, ..., c_n)\\} and the query sentence with m words Q = {\\(q_1, q_2, ..., q_m)\\},
output a span S = {\\(c_i, c_{i+1}, ..., c_{i+j})\\} from the original paragraph C. In the following, we will use x to denote both the original word and its embedded vector, for any x ∈ C, Q.

The resulting representation from their model is encoded again with our recurrency-free encoder before finally decoding to the probability of each position being the start or end of the answer span as following:

![Yu et al. ICLR 2018](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/MRC/2020-08-25-QANet_Combining_Local_Convolution_with_Global_Self-Attention_for_Reading_Comprehension/QAnet.PNG)

They argued that the recurrency-free model make  their model faster than The RNN counterparts.

For the detailed model components, refer to [the paper, QANet: Combining Local Convolution with Global Self-Attention for Reading Comprehension. Yu et al. ICLR 2018](https://openreview.net/forum?id=B14TlG-RW/)

For data augmentation, they used back-translation techique for machine reading comprehension task that they are interested in. 

![Yu et al. ICLR 2018](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/MRC/2020-08-25-QANet_Combining_Local_Convolution_with_Global_Self-Attention_for_Reading_Comprehension/Data_augmentation.PNG)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Current end-to-end machine reading and question answering (Q&A) models are primarily based on recurrent neural networks (RNNs) with attention. Despite their success, these models are often slow for both training and inference due to the sequential nature of RNNs. They propose a new Q&A architecture called QANet, which does not require recurrent networks: Its encoder consists exclusively of convolution and self-attention, where convolution models local interactions and self-attention models global interactions. On the SQuAD dataset, our model is 3x to 13x faster in training and 4x to 9x faster in inference, while achieving equivalent accuracy to recurrent models. The speed-up gain allows us to train the model with much more data. They hence combine our model with data generated by backtranslation from a neural machine translation model. On the SQuAD dataset, their single model, trained with augmented data, achieves 84.6 F1 score1 on the test set, which is significantly better than the best published F1 score of 81.8.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://openreview.net/forum?id=B14TlG-RW/">The paper: QANet: Combining Local Convolution with Global Self-Attention for Reading Comprehension. Yu et al. ICLR 2018</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: QANet: Combining Local Convolution with Global Self-Attention for Reading Comprehension. Yu et al. Arxiv 2018](https://arxiv.org/abs/1804.09541)
  - [ICLR 2018 version: QANet: Combining Local Convolution with Global Self-Attention for Reading Comprehension. Yu et al. ICLR 2018](https://openreview.net/forum?id=B14TlG-RW/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    

