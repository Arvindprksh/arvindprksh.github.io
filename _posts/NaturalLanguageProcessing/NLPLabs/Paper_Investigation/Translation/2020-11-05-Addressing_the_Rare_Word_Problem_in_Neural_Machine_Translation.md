---
layout: post
title: On Using Very Large Target Vocabulary for Neural Machine Translation
subtitle: Title of paper - On Using Very Large Target Vocabulary for Neural Machine Translation
category: NLP papers - Translation
tags: [translation]
permalink: /2020/11/02/On_Using_Very_Large_Target_Vocabulary_for_Neural_Machine_Translation/
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

This is a brief summary of paper for me to study and organize it, [Addressing the Rare Word Problem in Neural Machine Translation. Luong et al. ACL and IJCNLP 2015](https://www.aclweb.org/anthology/P15-1002/) that I read and studied. 
{% include MathJax.html %}

They resoved the problem to handling OOV word on neural machine translation which is a conceptually simple large neural network that reads the etire source sentence and produces an output translation one word at a time.

Example of the rare word problem:

![Luong et al. ACL and IJCNLP 2015](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2020-11-05-Addressing_the_Rare_Word_Problem_in_Neural_Machine_Translation/problem_1_of_the_rare_word.PNG)

The minimum of domain knowledge is used in neural machine translation since neural machine translation archtecture can be formulated to make it to any problem such as mapping input sequence to output sequence. 

In addition, the natural ability of neural networks to gnenralize implies that nueral machine translation systems will also generalize to novel word phrases and sentences that do not occur in the training set.

Furthermore, the neural machine translation potentially remove the need to store explicit pharase tables and language models which are used in conventional translation system.

Despite these advantages, conventional neural mchine translation systems is incapable of translating rare words because they hvae a fixed modest-sized vocabulary which forces them to use **UNK** symbol to represent the large number of out-of-vocabulary (OOV) words. 

The reason for the conventional neural machine translation system to have modest-size vocabulary is due to computationally intensive nature of the softmax, so the neural machine translation systems often limit their vocabualry size to be 30K-80K most frequent words in each language. 

This paper proposed and impolemented a novel approach to address the rare word problem of nueral machine translation. 

Their approach annotates the training corpus with explicit alignment information that enables the NMT system to emit.

For each OOV word, a "pointer" to its corresponding words in the source stentnece. 

The information is utilized in a post-processing step that ranslates the OOV words using a dictionary  or with the identity translation, if no the translation is found.

In other words, They propose to address the rare word problem by training the NMT systems to track the origins of the unknow words in the target sentences. 

If the neural machine translation system knew the soruce word responsible for each unknown target word, in the post-processing step they propose to replace each **UNK** in the system output with a translation of its source word, using either a dictionary or the identity translation.

For example, in Figure 1, if the model knows that the second unknown token in the NMT (line nn) originates from the source word **ecotax**, it can perform a word dictionary lookup to replace that unknown token by **ecotaxe**. Similarly, an identity translation of the source word **Pont-de-Buis** can be applied to the third unknown token.

Therefore, they present three annotation strategies that can easily be applied to any neural machine translation systems. 

They treat the neural machine translation system as a black box and train it on a corpus annotated by one of the models below. 

First, the alignments are produced with an unsupervised aligner ([Liang et al., ACL 2006](https://www.aclweb.org/anthology/N06-1014/)).

Nest, they use the alignment links to construct a word dictionary that will be used for the word translation in the post-processing step.

When constructing the dictionary from these alignment links, they add a word pair to the dictionary only if its alignment count exceeds 100

If a word does not appear in their dictionary, then they the identity translation.

1. Copyable Model

In this approach, they use mutiple tokens to represent the various unknow words in the source and in the target language, as opposed to using nonly one **UNK** token.

They annotate the OOV words in the source sentence with \\(UNK_1, UNK_2, UNK_3\\) in order, while assigning repeating unkown words identical tokens.

The annotation of the unknown words in the target language is slightly more elaborate: (a) each unknown target word that is aligned to an unknown source word is assigned the same unknown token. It is why they call their model copy model.

and (b) an unknow target word that has no alignment or that aligned with a known word uses the speical null token \\(UNK_{\O}\\).

See the Figure 2 below for an example. This annotation enables us to translate every non-null unknown token.

![Luong et al. ACL and IJCNLP 2015](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2020-11-05-Addressing_the_Rare_Word_Problem_in_Neural_Machine_Translation/Annotation_1.PNG)

2. Positional All Model (PosAll)

The model above, copyable model, is limited by its inability to translate unknown target words that are aligned to known words in the source sentence.

So they propose anonther annotatio model that include the complete alignments between model that includes the complete alignments between the source and the target sentence.

Specifically, they return to using only a single universl **UNK** token. But, on the targe side, they insert a positional token \\(p-d\\) after every word.

where \\(d\\) indicates a relative position (\((d = -7, ..., -1, 0, 1, ..., +7 \\)) to denote that a trage words at position \\(j\\) is aligned to a soruce word as position \\(i = j - d\\). 

Aligned words that are too far apart are condiered unaligned, and unaligned words reannotated with a null token \\(p_{\0}\\)

their annotation is illustrated in Figure 3 below.

![Luong et al. ACL and IJCNLP 2015](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2020-11-05-Addressing_the_Rare_Word_Problem_in_Neural_Machine_Translation/Annotation2.PNG)

3. Positional Unknown Model (PosUnk)

The weakness of the PosAll model is that it doubles the length of the target sentence.

This makes learning more difficult ant slow s the speed of parameter updates by a factor of two. 

Their post-processing step is concerned only with the alignment of the unkwnown words, so it is more sensible to only annotate the unknown words. 

Based on it, they create the poistional Unknown model (PosUnk) which uses \\(unkpos_d\\)) tokens (for \\(d\\) in -7, ..., 7 or \\(\0\\)) to simultaneously denote (a) the fact that a word is unknown and (b) its relative position \\(d\\) with respect to its aligned source word.

They also use the symbol \\(unkpos_{\0}\\) for unknown target words that do not have an alignment.

They use the universal **UNK** for all unknown tokens in the source language.

See Figure 4 below for an annotated example.

![Luong et al. ACL and IJCNLP 2015](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2020-11-05-Addressing_the_Rare_Word_Problem_in_Neural_Machine_Translation/Annotation_3.PNG)

For training, they used the same neural network structure such as [Sutskever et al. NIPS 2014](https://arxiv.org/abs/1409.3215) which uses a deep LSTM ot encode the input sequence and a separate deep LSTM to output the translation.

For detailed experiment analysis, you can found in [Addressing the Rare Word Problem in Neural Machine Translation. Luong et al. ACL and IJCNLP 2015](https://www.aclweb.org/anthology/P15-1002/)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Neural Machine Translation (NMT) is a new approach to machine translation that has shown promising results that are comparable to traditional approaches. A significant weakness in conventional NMT systems is their inability to correctly translate very rare words: end-to-end NMTs tend to have relatively small vocabularies with a single unk symbol that represents every possible out-of-vocabulary (OOV) word. In this paper, they propose and implement an effective technique to address this problem. They train an NMT system on data that is augmented by the output of a word alignment algorithm, allowing the NMT system to emit, for each OOV word in the target sentence, the position of its corresponding word in the source sentence. This information is later utilized in a post-processing step that translates every OOV word using a dictionary. Their experiments on the WMT’14 English to French translation task show that this method provides a substantial improvement of up to 2.8 BLEU points over an equivalent NMT system that does not use this technique. With 37.5 BLEU points, their NMT system is the first to surpass the best result achieved on a WMT’14 contest task.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/P15-1002/">The paper: Addressing the Rare Word Problem in Neural Machine Translation. Luong et al. ACL and IJCNLP 2015</a>
</div>

# Reference 

- Paper 
  - [Arxiv version: Addressing the Rare Word Problem in Neural Machine Translation. Luong et al. arXiv 2014](https://arxiv.org/abs/1410.8206)
  - [ACL and IJCNLP 2015 version: Addressing the Rare Word Problem in Neural Machine Translation. Luong et al. ACL and IJCNLP 2015](https://www.aclweb.org/anthology/P15-1002/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


