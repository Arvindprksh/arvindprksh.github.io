---
layout: post
title: Distributed_Representations_Of_Sentences_and_Documents
subtitle: Title of paper - Distributed_Representations_Of_Sentences_and_Documents
category: NLP papers
tags: [nlp, word2vec, word_embedding]
permalink: /2018/03/28/Distributed_Representations_Of_Sentences_and_Documents/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---


I think sentence embeddings, document embeddings, and pragraph embedding have been studied in NLP, Because word embedding have beend tired in NLP field. 

Nowadays, it is important to embed sentences, documents, or paragraph on sentiment analysis and text classification. 

So I read a paper about how to embed setences and documents. 

The title of the paper is **Distributed Representations of Sentences and Documentes**.

Let's see the models they argue for paragraph vector. ahead of proceeding to the inpiration of their model. 

The inspired model is to predict next word if you know some context. let's say "the cat sat on ~" is a sentences to make word embeddings. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2018-03-28-Distributed_Representations_Of_Sentences_and_Documents/Learning_Vector_Representation_of_words.png)

The framework above is learning word vectors. this task is to predict a word given the other words in a context. 

The objective of the model above is to maximize the average of log probability. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2018-03-28-Distributed_Representations_Of_Sentences_and_Documents/Log_porability.png)

The prediction task is typically done via a multiclass classifier, such as softmax. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2018-03-28-Distributed_Representations_Of_Sentences_and_Documents/soft_max.png)

each yi in the fomulation above is unnormalized log-probability for each output word i, computed as 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2018-03-28-Distributed_Representations_Of_Sentences_and_Documents/For_soft_max.png)

On image above, U,b are the softmax parameters. h is constructed by a concatenation or average of word vector extracted from W. 

Let's see the two models they argue for paragraph vector. 

First is the Distributed Memory Model of Paragraph Vector(PV-DM). 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2018-03-28-Distributed_Representations_Of_Sentences_and_Documents/Distributed_Memory_model .png)

In the model above, The contexts are fixed-lenghth and sampled from a sliding window over the paragraph. The paragraph is shared across all contexts generated from the same paragraph but not across paragraph. The word vector matrix W, however, is shared across pargraphs. i.e. the vector for "powerful" is the same for all paragraph. 

Second is the Distributed Bag of words(PV-DBOW).

This model is simple, This way is to ignore the context words in the input, But force the model to predict words randomly sampled from the paragraph in the output. i.e. paragraph vector is trained to predict the words in a small window. 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2018-03-28-Distributed_Representations_Of_Sentences_and_Documents/Distributed_bag_of_model.png)


<div class="alert alert-success" role="alert"><i class="fa fa-check-square-o"></i> <b>Tip: </b>
when you set the window size for a context into a particular value and if your sentence or paragragph is less than the windows size, In the case fo their experiment, they pre-pad with a special NULL word symbol.  
</div>


They have proven How good their paragraph vector is at NLP task such sentiment analysis and informtional retrieval. 

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
They have two ways you can embed setences, document or paragraph. So they propose Pragraph Vector, an unsupervised framework that learns continuous distributed vector representations for pieces of text. Two models is called PV-DM and PV-DBOW. PV-DM is The Distributed Memory Model of Paragraph Vector. PV-DBOW is the Distributed Bag of Words version of paragraph vector 
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://arxiv.org/abs/1405.4053v2">The paper: Distributed Representations of Sentences and Documents</a>
</div>

# Reference 

 - Paper 
 -- [Distributed Representations of Sentences and Documents](https://arxiv.org/abs/1405.4053v2)
 
 - How to use html for alert
 -- [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
