---
layout: post
title: Finding Function in Form- Compositional Character Models for Open Vocabulary Word Representation
subtitle: Title of paper - Finding Function in Form- Compositional Character Models for Open Vocabulary Word Representation
category: NLP papers - OOV Embedding
tags: [OOV Embedding]
permalink: /2020/11/02/Finding_Function_in_Form_Compositional_Character_Models_for_Open_Vocabulary_Word_Representation/
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

This is a brief summary of paper for me to study and organize it, [Finding Function in Form: Compositional Character Models for Open Vocabulary Word Representation. Ling et al. EMNLP 2015](https://www.aclweb.org/anthology/D15-1176/) I read and studied. 
{% include MathJax.html %}

This paper proposed the method to use character embedding instead of word look up table, which cannot generate representations for previously unseen words.

They said as follows:

>>Although models based on word lookup tables are often observed to learn that cats, kings, and queens exist in roughly the same linear correspondences to each other as cat, king, and queen do, the model does not represnt the fact that adding an **s** at the end of the words is evidence for this transformation. This means that word lookup tables cannot generate representations for previously unseen words, such as Frenchification, even if the components, French and -ification, are observed in other contexts.
 
They use bidirectional LSTMs to read character sequence that comprise each word and combine them into a vector representation of the word. 

Their model assumes that each character type is associated with a vector, and the LSTM parameters encode both idiosyncratic lexical and regular morphological knowledge.

C2W model(i.e. their compositional character to word model) is based on bidirectional LSTM  as follow:

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-11-02-Finding_Function_in_Form_Compositional_Character_Models_for_Open_Vocabulary_Word_Representation/C2W_model.PNG)

as shown in the figure above, The input of the C2W model use an alphabet of characters \\(C\\). 

The input word \\(w\\)is decomposed into a sequence of characters \\(c_1, ..., c_n\\), where m is the length of \\(w\\). 

Each \\(c_i\\) is defined as a one hot vector \\(1_{c_i}\\), with one on the index of \\(c_i\\) in vocabulary \\(M\\). 

They defined the projection layer \\(P_C \in \mathbb R^{d_c \times \|C\|}\\), where \\(d_C\\) is the number of parameters for each character in the character set \\(C\\).

That is, this is just character look up table. 

They implemented the C2W model on two tasks such as POS tagging and Language modeling. 

The following is for language modeling:

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-11-02-Finding_Function_in_Form_Compositional_Character_Models_for_Open_Vocabulary_Word_Representation/C2W_language_model.PNG)

The following is for POS tagging 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-11-02-Finding_Function_in_Form_Compositional_Character_Models_for_Open_Vocabulary_Word_Representation/C2W_pos_tagging.PNG)

The detailed result can be found in Finding Function in Form: Compositional Character Models for Open Vocabulary Word Representation. Ling et al. EMNLP 2015](https://www.aclweb.org/anthology/D15-1176/)


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They introduce a model for constructing vector representations of words by composing characters using bidirectional LSTMs. Relative to traditional word representation models that have independent vectors for each word type, their model requires only a single vector per character type and a fixed set of parameters for the compositional model. Despite the compactness of this model and, more importantly, the arbitrary nature of the form–function relationship in language, their “composed” word representations yield state-of-the-art results in language modeling and part-of-speech tagging. Benefits over traditional baselines are particularly pronounced in morphologically rich languages (e.g., Turkish).
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/D15-1176/">The paper: Finding Function in Form: Compositional Character Models for Open Vocabulary Word Representation. Ling et al. EMNLP 2015</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Finding Function in Form: Compositional Character Models for Open Vocabulary Word Representation. Ling et al. arXiv 2015](https://arxiv.org/abs/1508.02096)
  - [EMNLP 2015 version: Finding Function in Form: Compositional Character Models for Open Vocabulary Word Representation. Ling et al. EMNLP 2015](https://www.aclweb.org/anthology/D15-1176/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


