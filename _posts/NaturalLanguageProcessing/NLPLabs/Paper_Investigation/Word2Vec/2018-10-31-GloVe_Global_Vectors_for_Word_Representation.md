---
layout: post
title: GloVe-Global Vectors for Word Representation
subtitle: Title of paper - GloVe-Global Vectors for Word Representation
category: NLP papers
tags: [nlp, word2vec]
permalink: /2018/10/31/GloVe_Global_Vectors_for_Word_Representation/
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

{% include MathJax.html %}


This psoting is summary about the paper, "[GloVe: Global Vectors for Word Representation](https://nlp.stanford.edu/pubs/glove.pdf)"


There are two methodologies for distributional word representations.

The one is to be learned from count-based method like latent semantic anlaysis-LSA(Deer-wester et al., 1990) and hyperspace analogue to Language-HAL(Lund and Burgess, 1996).

  - based on frequencies of terms.
  
    1) In LSA, matrix of term-document type like bag-of-words matrix: rows correspond to words or terms, and the columns correspond to different documents in corpus.
    
    2) In HAL, matrix of term-term type like co-occurence matrix: rows correspond to words, and the columns correspond to the entries which is the number of times a given word occurs in the context of another given word.
       - In particular, co-occurence matrix could be transformed to an entropy- and asn correlations-based normalization.

    3) PPMI(Bullinaria and Levy 2007), square root type HPCA-Hellinger PCA(Lebret and Collobert, 2014) and so on.
    
The other is to be learned prediction-based method like Word2Vec(Mikolov et al., 2013), vLBL and ivLBL(Mnih and Kavukcuoglu 2013), Bengio et al.(2003), Collobert and Weston(2008), Collobert et al.(2011).


All the methods above could be separated into Matrix Factorization Method(i.e. NMF:Non-negative Factorization) and Shallow Winodw-Based Methods.


### GloVe

GloVe paper said the statistics of word occurence in a corpus is the primary source of information available to al unsupervised methods for learning  word representation.

So, GloVe utilized are the matrix word-word co-coccurence with context window size.

Above all, Let's see notation for equation of GloVe.


Let the matrix of word-word co-occurrence counts be denoted by X, whose entries \\(X_{ij}\\) tabulate the number of times word j occurs in the context of word i.

Let \\( X_{i}=\sum_{k}X_{ik} \\) be the number of times any word appears in the context of word i.

Finally, let \\( P_{ij}=P(j\|i)=X_{ij}/X_{i} \\) be the probability that word j appear in the context of word i.


How to correlate the co-occurence matrix to two words in some phase. 

The following table from the GloVe paper would explain it. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2018-10-31-GloVe_Global_Vectors_for_Word_Representation/Co-occurence_matrix_probability.png)


GloVe is log-bilinear regression model so the cost function is the same from the following


![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2018-10-31-GloVe_Global_Vectors_for_Word_Representation/Cost_function.png)

As you can see above, \\( f(X_{ij}) \\) is weighting function. The weigting function should be obey the following properties:

 - f(X) should be non-decreasing so that rara co-occurences are not overweighted.
 
 - f(X) should be relatively small for large value of X, so that frequent co-occurences are not overweighted.

f(X) function below was used in the GloVe paper

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2018-10-31-GloVe_Global_Vectors_for_Word_Representation/Weighting_function.png)

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2018-10-31-GloVe_Global_Vectors_for_Word_Representation/Weigting_function_equation.png)


As you can see the cost function, GloVe calculate by co-occurence matrix size to update 
\\( W_{i} \\) is word vector, ith row on co-occurence matrix.

Also

\\( W_{j} \\) is context word vector for the context of ith row vector on co-occurence matrix.

The cost function calculate the least square of the dot product of \\(W_{i}\\) and \\(W_{j}\\) - \\(log(X_{ij})\\)

\\(X_{ij}\\) is count of oc-occurence matrix.

<div class="alert alert-success" role="alert"><i class="fa fa-check-square-o"></i> <b>Tip: </b>
`\(W_{i}\)` and `\(W_{j}\)` is weight matrix(i.e. vector) and is equivalent and differ only as a result of their random initializations, and X(co-occurence matrix) is symmetric. the sum of `\(W_{i}\)` and `\(W_{j}\)` is used for word vector which boosts the performace in NLP task of thie paper
</div>

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
GloVe is another way to represent words into continuous vector space with two features which are global cooccurence matrix and log-bilinear regression model. GloVe utilize the familes like 1) global matrix factorization method, 2) local context window methods.
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://nlp.stanford.edu/projects/glove/">The paper: GloVe:Global Vectors for Word Representation</a>
</div>

<div id="tutorial-section">

  <div id="tutorial-title">GloVe Youtube</div>

  <ul class="nav nav-pills">
    <li class="active"><a data-toggle="tab" href="#refrigerator">Stanford Youtube</a></li>
    <li><a data-toggle="tab" href="#refrigerator_concept">DeepLearning AI</a></li>
  </ul>

  <div class="tab-content">
    <div id="refrigerator" class="tab-pane fade in active">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/ASn7ExxLZws" frameborder="0" allowfullscreen></iframe>
    </div>
    <div id="refrigerator_concept" class="tab-pane fade">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/CE3PXQkbupk" frameborder="0" allowfullscreen></iframe> </div>
  </div>
</div>


# Reference 

- Paper 
  - [GloVe:Global Vectors for Word Representation](https://nlp.stanford.edu/projects/glove/)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
- [TowardsdataScience about GloVe](https://towardsdatascience.com/emnlp-what-is-glove-part-i-3b6ce6a7f970)  
  
- online Learning
  - [Online Learning of Word Embeddings on Medium](https://medium.com/explorations-in-language-and-learning/online-learning-of-word-embeddings-7c2889c99704)
  
  - [Online Learning on Linkedin Slide](https://www.slideshare.net/queirozfcom/online-machine-learning-introduction-and-examples)
     * I think the aobve links I read a little is very interesting. later on I would read both of them and papers related to it.
  
 - [bilinear regression definition](https://www.statisticshowto.datasciencecentral.com/bilinear-regression/)

 - [StackExchange about bilinear](https://math.stackexchange.com/questions/878325/what-is-a-bilinear-form)
