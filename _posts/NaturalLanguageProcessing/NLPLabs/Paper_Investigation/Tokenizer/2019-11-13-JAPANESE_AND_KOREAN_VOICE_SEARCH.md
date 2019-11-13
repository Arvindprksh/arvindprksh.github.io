---
layout: post
title: Japanese and Korean voice search
subtitle: Title of paper - Japanese and Korean voice search
category: NLP papers - Tokenizer
tags: [neural_network, Tokenizer]
permalink: /2019/11/13/JAPANESE_AND_KOREAN_VOICE_SEARCH/
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

This is a brief summary of paper for me to study and organize it, [Japanese and Korean Voice Search (Mike Schuster and Kaisuke Nakajima. 2012)](https://ieeexplore.ieee.org/document/6289079) I read and studied. 
{% include MathJax.html %}

I was interested in WordPiece model. The reason is When I read the paper published by Google they used **WordPiece** model.

For example, when I read [BERT](https://arxiv.org/abs/1810.04805) and [translation](https://arxiv.org/abs/1609.08144) papers, They use input tokens with **WordPiece** model. 

So I found the paper about WordPiece model from voice search reseach. 

In this paper, when they tokenized word to word unit, they doesn't consider the semantic information.

So they wanted to make tokenizer not dependent on language and solving the out-of-vocabulary problem. 

The model, called **WordPieceModel** learns word units form large amounts of text automatically and incremetally by running a greedy algorithm as follows:

They said : 

>>1. Initialize the word unit inventory with the basic Unicode  characters (Kanji, Hiragana, Katakana for Japanese, Hangul for Korean) and including all ASCII, ending up with about 22,000 for Japanese total and 11,000 for Korean.  
>>2. Build a language model on the training data using the inventory from 1.   
>>3. Generate a new word unit by combinning two units out of the current word inventory to increment the word unit inventory by one. Choose  the new word unit out of all possible ones that increase the likelihood on the training data the most when added to the model.  
>>4. Goto 2 until a predefined limit of word units is reached or the likelihood increase falls below a certain threshold.

Based on the **WordPieceModel**, its algorithm give deterministic segmentations.

In order to be able to learn where where to put spaces from the data and make it part of the decoding strategy they used the following:

>>1. The orignal language dmoel data is used **as written**, meaning some datat with, some without spaces.
>>2. when segmenting the LM data with **WordPieceModel** attach a space marker (they used an underscore or a tilde) before and after each unit when you see a space, otherwise don't attach. Each word unit can hence appear in four different forms, with underscore on both sides (there was a space originally on both sides in the data), with a space marker only on the left or only the right, and without space markers at all. The word inventory si now larger, possibly up to four times the original size if every combination exists.  
>>3. Biuld LM and dictionary based on this new inventory.  
>>4. During decodding the best path according to the model will be chosen, which preserves where to put spaces and where not. The attached space markers obviously have to be filtered out from the decoding output for correct display Assuming. The common scenario where the decoder puts automatically a space between each unit in the output string this procedure the is :  
>>    (a) Remove all spaces (" " -> "")    
>>    (b) Remove double space marker by space ("\_\_" -> " ")   
>>    (c) Remove remaining single space markers ("\_" -> "")     
>>This last step could potentially be also a replacement by space as this is the rare case when the decoder hypothesize a word unit with space followed by one without space or vice versa.

Let's see an exmaple explained in their paper:

They showed an example of the segmentation and gluing proceduer-note that the original and final texts contain where there is a space.

>>(1) Janpanese original unsegmented text   
>>(2) After segementation   
>>(3) the addition of underscores to retain location of spaces   
>>(4) a possible raw decoder result    
>>(5) with the final result after removing underscores     

![(Mike Schuster and Kaisuke Nakajima. 2012)](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Tokenizer/2019-11-13-JAPANESE_AND_KOREAN_VOICE_SEARCH/WordPieceModel_example.PNG)

Also, they said:
>>this techniques are successfully used for some Asian languages (Japanese, Korean, Mandarin) across multiple applications, Voice Search, dictation as well as YouTube caption generation.  

And Google release the extension of **WordPieceModel**, it is called [**SentencePiece**](https://github.com/google/sentencepiece).

If you want to know about **SentencePiece** in detail, visit [here](https://github.com/google/sentencepiece).

If you can also use the version of python, type in as follows: 

>>For installation of pythone module,  
>>SentencePiece provides Python wrapper that supports both SentencePiece training and segmentation.   
>>You can install Python binary package of SentencePiece with.  
>> % pip install sentencepiece


<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
This paper describe the techniques used to handle an infinite vocabulary and how to build dictionaries and so on. However, I focused on how to tokenize the Asian language making the OOV(out-of-vocabulary) problem less happen and using independent-language tokenizing techniques.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://ieeexplore.ieee.org/document/6289079">The paper: Japanese and Korean Voice Search (Mike Schuster and Kaisuke Nakajima. 2012)</a>
</div>

# Reference 

- Paper 
  - [Google AI Research: Japanese and Korean Voice Search (Mike Schuster and Kaisuke Nakajima. 2012)](https://ai.google/research/pubs/pub37842/)
  - [ICASSP 2012: Japanese and Korean Voice Search (Mike Schuster and Kaisuke Nakajima. 2012)](https://ieeexplore.ieee.org/document/6289079)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    
- For your information
  - [Google Sentence Piece gitub](https://github.com/google/sentencepiece)
  
  - Korean ver.
    - [Word Piece Model (a.k.a sentencepiece) on lovit blog](https://lovit.github.io/nlp/2018/04/02/wpm/)
    - [word segmentation about NLP on WHAT IS NATURAL LANGUAGE PROCESSING? wikidocs](https://wikidocs.net/22592)
    - [Unsupervised tokenizers in soynlp project on lovit blog](https://lovit.github.io/nlp/2018/04/09/three_tokenizers_soynlp/)
    - [SoyNLP github](https://github.com/lovit/soynlp)

Below is youtube about Korean tokenizing for your information

<div id="tutorial-section">

  <div id="tutorial-title">GloVe Youtube</div>

  <ul class="nav nav-pills">
    <li class="active"><a data-toggle="tab" href="#refrigerator">Korean Tokenizing with soynlp</a></li>
  </ul>

  <div class="tab-content">
    <div id="refrigerator" class="tab-pane fade in active">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/Vj55zaDvn4Q" frameborder="0" allowfullscreen></iframe>
    </div>
  </div>
</div>



























