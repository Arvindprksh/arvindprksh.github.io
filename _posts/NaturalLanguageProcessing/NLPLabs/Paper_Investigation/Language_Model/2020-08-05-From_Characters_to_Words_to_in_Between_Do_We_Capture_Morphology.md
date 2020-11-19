---
layout: post
title: From Characters to Words to in Between- Do We Capture Morphology?
subtitle: Title of paper - From Characters to Words to in Between- Do We Capture Morphology?
category: NLP papers - Language Model
tags: [neural network, language model]
permalink: /2020/08/05/From_Characters_to_Words_to_in_Between_Do_We_Capture_Morphology/
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

This is a brief summary of paper for me to study and simply arrange it, [From Characters to Words to in Between: Do We Capture Morphology? (Vania and Lopez., ACL 2017)](https://www.aclweb.org/anthology/P17-1184/) I read and studied. 
{% include MathJax.html %}

They investigated the composotion function on word using character, morphem, and word with language model task as follows:

![Vania and Lopez. 2017 ACL](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Language_Model/2020-08-05-From_Characters_to_Words_to_in_Between_Do_We_Capture_Morphology/LSTM_LM.PNG)

They found out the Bi-LSTM compostion function is usually better than CNN and add in different languages. 

If tested with morphological analyzer, character embedding shows better performance on language model task rather than morpheme representation. 

But, on arcle experiment the true morphological analysis is better than character representation in Czech and Russian. 

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Words can be represented by composing the representations of subword units such as word segments, characters, and/or character n-grams. While such representations are effective and may capture the morphological regularities of words, they have not been systematically compared, and it is not understood how they interact with different morphological typologies. On a language modeling task, we present experiments that systematically vary (1) the basic unit of representation, (2) the composition of these representations, and (3) the morphological typology of the language modeled. Their results extend previous findings that character representations are effective across typologies, and they find that a previously unstudied combination of character trigram representations composed with bi-LSTMs outperforms most others. But they also find room for improvement: none of the character-level models match the predictive accuracy of a model with access to true morphological analyses, even when learned from an order of magnitude more data.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P17-1184/">The paper: From Characters to Words to in Between: Do We Capture Morphology?. Vania and Lopez. 2017 ACL</a>
</div>

# Reference 

- Paper 
  - [arXiv Version: From Characters to Words to in Between: Do We Capture Morphology?  (Vania and Lopez., arXiv 2017)](https://arxiv.org/abs/1704.08352)
  - [ACL Version: From Characters to Words to in Between: Do We Capture Morphology? (Vania and Lopez., ACL 2017)](https://www.aclweb.org/anthology/P17-1184/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [How to use MathJax on stackoverflow](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)




























