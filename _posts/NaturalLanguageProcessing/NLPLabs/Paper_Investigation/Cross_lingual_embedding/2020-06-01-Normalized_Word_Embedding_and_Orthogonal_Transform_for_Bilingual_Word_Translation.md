---
layout: post
title: Normalized Word Embedding and Orthogonal Transform for Bilingual Word Translation
subtitle: Title of paper - Normalized Word Embedding and Orthogonal Transform for Bilingual Word Translation
category: NLP papers - Cross-lingual Word Embedding
tags: [cross_lingual_word_embedding]
permalink: /2020/06/01/Normalized_Word_Embedding_and_Orthogonal_Transform_for_Bilingual_Word_Translation/
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

This is a brief summary of paper for me to study and arrange for [Normalized Word Embedding and Orthogonal Transform for Bilingual Word Translation. Xing et al. NAACL 2015](https://www.aclweb.org/anthology/N15-1104/) I read and studied. 
{% include MathJax.html %}

This paper propose handling the inconsistence among the objective function used to learn word vectors (maximum likelihood based on inner product), the distance measurement for word vectors (cosine distance), and the objective function used to learn the linear transform(mean square error). Conjecturing this inconsistence may lead to suboptimal estimation for both word vectors and the bilingual transform.

So, they solved the inconsistence by normalizing the word vectors. Specifically, the word vectors are enforced to be in a unit length during the learning of the embedding. By this constraint, all the word vectors are located on a hypersphere and so the inner product falls back to the cosine distance:

![Xing, et al. 2015 NAACL](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Cross_lingual_embedding/2020-06-01-Normalized_Word_Embedding_and_Orthogonal_Transform_for_Bilingual_Word_Translation/normalized_vector.PNG)

This hence solves the inconsistence between the embedding and the distance measurement. To reflect the normalization constraint on word vectors, the linear transform in the bilingual projection has to be constrained as an orthogonal transform. Finally, the cosine distance is used when we train the orthogonal transform, in order to achieve full consistence

They prove their method's performance on word similarity task and bilingual word traslation which can be categorized into projection-based approaches and regularizationbased approaches.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Word embedding has been found to be highly powerful to translate words from one language to another by a simple linear transform. However, they found some inconsistence among the objective functions of the embedding and the transform learning, as well as the distance measurement. This paper proposes a solution which normalizes the word vectors on a hypersphere and constrains the linear transform as an orthogonal transform. The experimental results confirmed that the proposed solution can offer better performance on a word similarity task and an English-toSpanish word translation task.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/N15-1104/">The paper: Normalized Word Embedding and Orthogonal Transform for Bilingual Word Translation. Xing, et al. 2015 NAACL</a>
</div>

# Reference 

- Paper 
   - [NAACL version: Normalized Word Embedding and Orthogonal Transform for Bilingual Word Translation. Xing et al. NAACL 2015](https://www.aclweb.org/anthology/N15-1104/)
  
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    




























