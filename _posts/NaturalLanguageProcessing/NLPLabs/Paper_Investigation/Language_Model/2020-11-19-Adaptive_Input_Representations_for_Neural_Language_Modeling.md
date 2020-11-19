---
layout: post
title: Adaptive Input Representations for Neural Language Modeling
subtitle: Title of paper - Adaptive Input Representations for Neural Language Modeling
category: NLP papers - Language Model
tags: [neural network, language model]
permalink: /2020/11/19/Adaptive_Input_Representations_for_Neural_Language_Modeling/
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

This is a brief summary of paper for me to study and simply arrange it, [Adaptive Input Representations for Neural Language Modeling (Baevski and Auli., ICLR 2019)](https://openreview.net/forum?id=ByxZX20qFQ) that I read and studied. 
{% include MathJax.html %}

They pointed out the trouble for a substantional part of the overall computation in softmax, the common approach to lower the computation burden is to strcture the output vocabulary so that not all probabilities need to be computed. 

Unlike the structure, the further method is adaptive softmax([Grave et al., arXiv 2017](https://arxiv.org/abs/1609.04309)) which introduces a variable capacity scheme for output word embeddings, assigning more parameters to frequent words and fewer parameters to rare words.  

So they applied the adaptive softmax into input embedding they called adative input embeddings which extend the adaptive softmax to input word representation. 

This factorization assigns more capacity to frequent words and reduces the capacity for less frequent words with the benefit of reducing to rare words. 

The adaptive softmax exploits the faction that the distrbution of word types in natural language follows a [Zipfian distribution](https://en.wikipedia.org/wiki/Zipf%27s_law) in order to imporves the computation of the output probabilities.

For adaptvie input embedding, they define a number of clusters that partitions the ferquency ordered vocbulary \\(V = v_1 \cup v_2, ..., v_{n-1} \cup v_n\\) such that \\(V_i \cap V_j =  \emptyset\\) for \\( \forall i, j\\) and \\(i \neq j\\), where \\(v_1\\) contains the most frequenc words and \\(v_n\\) the least frequenct words.

They reduce the capacity for each cluster which is that if words in \\(v_1\\) have dimension \\(d\\), then words in \\(v_n\\) have dimension \\(\frac{d}{k^{n-1}}\\). In their paper, they set up k as 4.

Next, they add linear projections \\(W_1 \in \Bbb R^{d \times d}, ..., W_n \in \Bbb R^{frac{d}{k^{n-1}} \times d} \\) to map the embeddings of each cluster to dimension \\(d\\) so that the concatenated output of the adaptive input embedding layer can be easily used by the subsequent model as shown figure below:

![Baevski and Auli., ICLR 2019](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Language_Model/2020-11-19-Adaptive_Input_Representations_for_Neural_Language_Modeling/adaptive_input_representation.PNG)

For detailed result about experiment, see their paper, [Adaptive Input Representations for Neural Language Modeling (Baevski and Auli., ICLR 2019)](https://openreview.net/forum?id=ByxZX20qFQ).

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They introduce adaptive input representations for neural language modeling which extend the adaptive softmax of Grave et al. (2017) to input representations of variable capacity. There are several choices on how to factorize the input and output layers, and whether to model words, characters or sub-word units. They perform a systematic comparison of popular choices for a self-attentional architecture. Their experiments show that models equipped with adaptive embeddings are more than twice as fast to train than the popular character input CNN while having a lower number of parameters. On the WIKITEXT-103 benchmark they achieve 18.7 perplexity, an improvement of 10.5 perplexity compared to the previously best published result and on the BILLION WORD benchmark, they achieve 23.02 perplexity
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://openreview.net/forum?id=ByxZX20qFQ">The paper:  Adaptive Input Representations for Neural Language Modeling  (Baevski and Auli., ICLR 2019)</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: Adaptive Input Representations for Neural Language Modeling  (Baevski and Auli., arXiv 2019)](https://arxiv.org/abs/1809.10853)
  - [ICLR Version: Adaptive Input Representations for Neural Language Modeling  (Baevski and Auli., ICLR 2019)](https://openreview.net/forum?id=ByxZX20qFQ)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [How to use MathJax on stackoverflow](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)
  - [Kor Ver. Zipian's law](https://statkclee.github.io/text/nlp-zipf-law.html)
  - [Eng Ver. Zipian's law](https://en.wikipedia.org/wiki/Zipf%27s_law)


























