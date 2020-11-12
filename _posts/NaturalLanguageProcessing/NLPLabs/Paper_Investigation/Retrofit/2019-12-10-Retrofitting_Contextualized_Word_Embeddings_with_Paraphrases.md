---
layout: post
title: Retrofitting Contextualized Word Embeddings with Paraphrases
subtitle: Title of paper - Retrofitting Contextualized Word Embeddings with Paraphrases
category: NLP papers - Retrofitting
tags: [neural network, text classification]
permalink: /2019/12/10/Retrofitting_Contextualized_Word_Embeddings_with_Paraphrases/
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

This is a brief summary of paper for me to study and organize it, [Contextualized Word Embeddings with Paraphrases. Shi et al. EMNLP and IJCNLP 2019](https://www.aclweb.org/anthology/D19-1113/) I read and studied. 
{% include MathJax.html %}

Retrofitting means semantic speicalization of distrobutional word vector. i.e. already trained vector can be retrofitted with external knowledges like lexicon-semantic knowledge, as known as semantic specialization. 

Except for the retrofitting called post-processing retrofitting models, which is fine-tune pre-trained distributional vectors to better reflect external linguistic contraints, 

There are tow phases of specialization methods:

1) joint specialization methods, which augment distributional learning objectives with external linguistic constraints, 
2) the most recently proposed post-specialization methods that generalize the perturbations of the post-processing methods to the whole distributional space.

However, this paper exaplain how to retrofit context information of paraphrases, suggestting the figure below:

![Shi et al. 2019 EMNLP](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Retrofit/2019-12-10-Retrofitting_Contextualized_Word_Embeddings_with_Paraphrases/Retrofit_1.PNG)

They said 

>  These embedding models encode both words and their contexts and generate context-specific representations. While contextualized embeddings are useful, we observe that a language model-based embedding model, ELMo, cannot accurately capture the semantic equivalence of contexts. 

Without retraining the parameters of an existing model, In order to learns the transformation to minimize the difference of the contextualized representations of the shared word in paraphrased contexts, while differentiating between those in other contexts.

They propose the model called paraphrase-aware Retrofitting (PAR) below:

![Shi et al. 2019 EMNLP](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Retrofit/2019-12-10-Retrofitting_Contextualized_Word_Embeddings_with_Paraphrases/retrofit_2.PNG)

PAR learns an orthogonal transformation $M \in \mathbbR^{k*k}$ to reshap the input representation into a specific space to complement the collocate.

Given two contexts S1 and S2 that both contain a shared word w, the contextual difference of a input representation w is defined by the L2 distance:

![Shi et al. 2019 EMNLP](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Retrofit/2019-12-10-Retrofitting_Contextualized_Word_Embeddings_with_Paraphrases/retrofit_3.PNG)

![Shi et al. 2019 EMNLP](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Retrofit/2019-12-10-Retrofitting_Contextualized_Word_Embeddings_with_Paraphrases/Retrofit_4.PNG)

The training objective of PAR is the dentoed as follows:

![Shi et al. 2019 EMNLP](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Retrofit/2019-12-10-Retrofitting_Contextualized_Word_Embeddings_with_Paraphrases/retrofit_5.PNG)


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Contextualized word embedding models, such as ELMo, generate meaningful representations of words and their context. These models have been shown to have a great impact on downstream applications. However, in many cases, the contextualized embedding of a word changes drastically when the context is paraphrased. As a result, the downstream model is not robust to paraphrasing and other linguistic variations. To enhance the stability of contextualized word embedding models, they propose an approach to retrofitting contextualized embedding models with paraphrase contexts. their method learns an orthogonal transformation on the input space, which seeks to minimize the variance of word representations on paraphrased contexts. Experiments show that the retrofitted model significantly outperforms the original ELMo on various sentence classification and language inference tasks.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/D19-1113/">The paper: Retrofitting Contextualized Word Embeddings with Paraphrases. Shi et al. 2019 EMNLP</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: Retrofitting Contextualized Word Embeddings with Paraphrases. Shi et al. arXiv 2019](https://arxiv.org/abs/1909.09700)
  - [EMNLP Version: Retrofitting Contextualized Word Embeddings with Paraphrases. Shi et al. EMNLP and IJCNLP 2019](https://www.aclweb.org/anthology/D19-1113/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [EMNLP 2019 Tutorial on Semantic Specialization of Distributional Word Vectors](https://www.emnlp-ijcnlp2019.org/program/tutorials/)
  




























