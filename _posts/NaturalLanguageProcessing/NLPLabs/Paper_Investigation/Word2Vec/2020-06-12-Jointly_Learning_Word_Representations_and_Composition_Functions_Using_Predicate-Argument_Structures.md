---
layout: post
title: Dependency-Based Word Embeddings
subtitle: Title of paper - Dependency-Based Word Embeddings
category: NLP papers - Word Embedding
tags: [neural network, word embedding, dependency embedding]
permalink: /2020/05/15/Dependency_Based_Word_Embeddings/
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

This is a brief summary of paper for me to study and arrange it, [Jointly Learning Word Representations and Composition Functions Using Predicate-Argument Structures. Hashimoto et al. EMNLP 2014](https://www.aclweb.org/anthology/D14-1163/) I read and studied. 
{% include MathJax.html %}

They focus on the dependecy embedding with predictate-arguemtne structure as follows:

![Hashimoto et al. EMNLP 2014](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Word2Vec/2020-06-12-Jointly_Learning_Word_Representations_and_Composition_Functions_Using_Predicate-Argument_Structures/predict_argument_structure1.PNG)

In order for them to resolve the word disambiguation, they used POS information by combine word with POS taggging such as cause_NN.

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
They introduce a novel compositional language model that works on PredicateArgument Structures (PASs). their model jointly learns word representations and heir composition functions using bagof-words and dependency-based contexts. Unlike previous word-sequencebased models, their PAS-based model composes arguments into predicates by using he category information from the PAS. his enables our model to capture longrange dependencies between words and o better handle constructs such as verbobject and subject-verb-object relations.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/D14-1163/">The paper: Jointly Learning Word Representations and Composition Functions Using Predicate-Argument Structures. Hashimoto et al. EMNLP 2014</a>
</div>

# Reference 

- Paper 
  - [EMNLP 2014 Ver: Jointly Learning Word Representations and Composition Functions Using Predicate-Argument Structures. Hashimoto et al. EMNLP 2014](https://www.aclweb.org/anthology/D14-1163/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    






















































