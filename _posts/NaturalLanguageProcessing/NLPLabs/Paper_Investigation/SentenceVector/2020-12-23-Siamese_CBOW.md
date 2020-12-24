---
layout: post
title: Siamese CBOW- Optimizing Word Embeddings for Sentence Representations
subtitle: Title of paper - Siamese CBOW- Optimizing Word Embeddings for Sentence Representations
category: NLP papers - Sentence Representation
tags: [sentence representation]
permalink: /2020/12/23/Siamese_CBOW/
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

This is a brief summary of paper for me to study and organize it, [Siamese CBOW: Optimizing Word Embeddings for Sentence Representations (Kenter et al., ACL 2016)](https://www.aclweb.org/anthology/P16-1089/)
   that I read and studied. 
{% include MathJax.html %}


They propose the siamese CBOW for sentence representation as follows:

![Kenter et al., ACL 2016](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/SentenceVector/2020-12-23-Siamese_CBOW/Siamese_CBOW.PNG)

The keyword, the siamese in their method denotes sharing a word embedding matrix matrix for projection layer. 

In order to optimizing word embeddings directly for the purpos of being averaged, given a pair of sentences \\((s_i, s_j)\\), the probability \\(p(s_i, s_j)\\) that reflects how likely it is for the sentences to be adjacent to one another in the training data is calculated by softmax as follows:

$$ p_{\theta} = \frac{e^{cos(s_i^{\theta}, s_j^{\theta})}}{\sum_{k \in S} e^{cos(s_x^{\theta},s_k^{\theta})}} $$

where \\(s_x^{\theta}\\) denotes the embeding for sentence \\(s_x\\) based on the model parameters \\(\theta\\). 

Theoretically, the summation in the dnominator of the equation above should cover over all possible sentences \\(S\\), which is not feasible in practice.

Therefore, they replace the set \\(S\\) with union of the set \\(S^+\\) of sentences that occur next to the sentence \\(s_i\\) in the training data, and a set of \\(n\\) randomly chosen sentences\\(S^-\\) that are not observed next to the sentences \\(s_i\\) in training data. 

Finally, the loss function of the netword for the purpose of being averaged is calcaulated cross-entropy:


$$ L = - \sum_{s_j \in \{s^+ \\cup S^-\}} p(s_i, s_j) \cdot log(p_{\theta}(s_i, s_j)) $$


Where \\(p(\cdot)\\) is the taget probability the network should produce, and \\(p_{\theta}(\cdat)\\) is the prediction it estimates based on parameters \\(\theta\\), using softmax function.

The taget distribution simply is :


$$ p(s_i, p_j) =  \begin{Bmatrix}
                   \frac{1}{S^+}, if s_j \in S^+ \\
                   0, if s_j \in S^- \\
                   \end{Bmatrix}  $$

For example, if there are 2 positive examples (the sentences preceding and following the input sentence) and 2 negative example, the target distribution is \\((0.5, 0.5, 0, 0)\\).

They prove the quality for sentence representation by measuring similarity score of sentence pair. 

At the time, they used the Pearsons correlation correlation between scores annotated by human and cosine similarity score as the metric.

For OOV word, which have no word embedding, they omitted it when create sentence embedding by averaging word embeddings in a sentence. 

For detailed experiment analysis, you can found in [Siamese CBOW: Optimizing Word Embeddings for Sentence Representations (Kenter et al., ACL 2016)](https://www.aclweb.org/anthology/P16-1089/)
  
<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>

</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P16-1089/">The paper: Siamese CBOW: Optimizing Word Embeddings for Sentence Representations (Kenter et al., ACL 2016)</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: Siamese CBOW: Optimizing Word Embeddings for Sentence Representations (Kenter et al., arXiv 2019)](https://arxiv.org/abs/1606.04640)
  - [ACL Version: Siamese CBOW: Optimizing Word Embeddings for Sentence Representations (Kenter et al., ACL 2016)](https://www.aclweb.org/anthology/P16-1089/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


