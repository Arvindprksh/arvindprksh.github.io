---
layout: post
title: Character n-gram Embeddings to Improve RNN Language Models
subtitle: Title of paper - Character n-gram Embeddings to Improve RNN Language Models
category: NLP papers - Language Model
tags: [neural network, language model]
permalink: /2020/05/06/Character_n-gram_Embeddings_to_Improve_RNN_Language_Models/
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

This is a brief summary of paper for me to study and simply arrange it, [Character n-gram Embeddings to Improve RNN Language Models. Takase et al. 2019 AAAI](https://www.aaai.org/ojs/index.php/AAAI/article/view/4440) I read and studied. 
{% include MathJax.html %}


They propose character n-gram embedding with simplified Multi-dimensional self embedding as follows:

![Takase et al. 2019 AAAI](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Language_Model/2020-05-06-Character_n-gram_Embeddings_to_Improve_RNN_Language_Models/simplified_multi-dimensional_self_embedding.PNG)

The Multi-dimensional self embedding used the Mutli-dimensional self attention.

The Multi-dimensional self attention compute weights for each dimension of given embeddings and sumps up the weighted embeddings(i.e., element-wise weighted sum). 

They used anothe way to improve perplexity. it is word tyiing which shared the embedidng matrix with weigth matrix to evaluate the probablity distribution. 

Aslo They showed the their model is superior on the application task such as machine translation and headline generation tasks.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
This paper proposes a novel Recurrent Neural Network (RNN) language model that takes advantage of character information. They focus on character n-grams based on research in the field of word embedding construction. Their proposed method constructs word embeddings from character ngram embeddings and combines them with ordinary word embeddings. We demonstrate that the proposed method achieves the best perplexities on the language modeling datasets: Penn Treebank, WikiText-2, and WikiText-103. Moreover, their conduct experiments on application tasks: machine translation and headline generation. The experimental results indicate that their proposed method also positively affects these tasks.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aaai.org/ojs/index.php/AAAI/article/view/4440">The paper: Character n-gram Embeddings to Improve RNN Language Models. Takase et al. 2019 AAAI</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Character n-gram Embeddings to Improve RNN Language Models. Takase et al. Arxiv 2019](https://arxiv.org/abs/1906.05506)
  - [AAAI 2019 version: Character n-gram Embeddings to Improve RNN Language Models. Takase et al. 2019 AAAI](https://www.aaai.org/ojs/index.php/AAAI/article/view/4440)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [How to use MathJax on stackoverflow](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)




























