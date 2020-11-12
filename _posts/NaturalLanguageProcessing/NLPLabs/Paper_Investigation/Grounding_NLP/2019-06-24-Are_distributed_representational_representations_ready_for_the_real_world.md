---
layout: post
title: Are Distributional Representations Ready for the Real World? Evaluating Word Vectors for Grounded Perceptual Meaning
subtitle: Title of paper - Are Distributional Representations Ready for the Real World? Evaluating Word Vectors for Grounded Perceptual Meaning
category: NLP papers - Grounding NLP
tags: [nlp, ground learning]
permalink: /2019/06/24/Are_distributed_representational_representations_ready_for_the_real_world/
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

This posting is summary for my study about the paper, "[Are distributed representational ready for the real world? Evaluating word vectors for grounded perceptual meaning, Lucy and Gauthier. RoboNLP-WS 2017)](https://www.aclweb.org/anthology/W17-2810)"

Befere entering deep, I was wondering what is the Language grounding. 

So I read [a blog](https://ehudreiter.com/2018/09/13/language-grounding/) which introduce the concept of Language Grounding. 

After reading the blog above, I think langauge grounding is mapping words into real world considering context. 

The context means a avariety of facets which is other data, expectation and interpretation, individual speakers, and discourse context and so on.

## Grounded learning

The auhtors doubt that the modern reperesenation of word is distributional representation which encode vector into the compact one using co-occurences, however, it could accurately encode facets of conceptual meaning. 
 
In order to identify the capability of how well these representations can predict perceptual and conceptual feature of concerete concepts. 

They evaluate it with two semantic norm datasets sourced from human participants. 

Finally, they find out that several standard word representationa fail to encode many salient perceptual features of concepts. 


They have two dataset of semantic feature norm for testing whether or not distributional represenation has the conceptual and perceptual meaning.

- First dataset is, [McRae et al.](https://sites.google.com/site/kenmcraelab/norms-data)(2005): Semantic feature productions norm for a large set of living and nonliving things.

Let's see an example of semantic norm data above. 

![a sample of McRae norm dataset](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Grounding_NLP/Are_distributed_representational_representations_ready_for_the_real_world/McRae_norm_dataset.JPG)


the concepts have various features which is related to perceptual and conceptual meaning.

- Second is CLBS(Devereux et al. 2014): The centre for speech, language and the grain(cslb) concept property norms.


As you can see the semantic norm dataset, concept means words and feature means characteristic the words have. 

For example, in order to explain feature of a word, airplane, there are a variety of features as follows: 

- airplane has_wings(visual-from_and_surface)
- airplane used_for_passengers(function)
- airplane found_in_airports(encclopaedic)
- airplane is_large(visual-form_and_surface)

They argued that the feature deficiencies affect word-word similarity measure and domain clustering. 


<div class="alert alert-success" role="alert"><i class="fa fa-check-square-o"></i> <b>Tip: </b>
They think of the feature as "has_legs" and "is_round", the test of perceptual meaing is whether distributional representation has it or not.
</div>

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note: </b>
Distributional word representation methods exploit word co-occurrences to build compact vector encodings of words. However it is unclear whether they accurately encode all necessary facets of conceptual meaning. they evaluated how well these representations can predict perceptual and conceptual features of concrete concepts with two semantic norm datasets sourced from human participants. they found that several standard word representations fail to encode many salient perceptual features of concepts, and show that these deficits correlate with word-word similarity prediction errors. 
</div>
  
  
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/W17-2810">The paper: Are distributed representational ready for the real world? Evaluating word vectors for grounded perceptual meaning</a> RoboNLP-WS 2017.
</div>

# Reference 

- Paper 
  - [RoboNLP-WS Version: Are distributed representational ready for the real world? Evaluating word vectors for grounded perceptual meaning. RoboNLP-WS 2017](https://www.aclweb.org/anthology/W17-2810)
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
  
  - [introduction to Language Groudning to vision and control on Carnegie Mellon school of computer science](https://katefvision.github.io/LanguageGrounding/Slides/LGVC_lecture_intro.pdf)

  - [McRaelabe's norm dataset](https://sites.google.com/site/kenmcraelab/norms-data)
  
  - [a proportion of McRae dataset](https://drive.google.com/file/d/0B2ga8vUirua7UlJ0VEJzaUJnVmc/view)
