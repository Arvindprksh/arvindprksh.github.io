---
layout: post
title: Meta-Learning for Low-Resource Neural Machine Translation
subtitle: Title of paper - Meta-Learning for Low-Resource Neural Machine Translation
category: NLP papers - Translation
tags: [meta-learning, translation]
permalink: /2020/06/17/Meta-Learning_for_Low-Resource_Neural_Machine_Translation/
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

This is a brief summary of paper for me to note it, [Meta-Learning for Low-Resource Neural Machine Translation. Gu et al. EMNLP 2018](https://www.aclweb.org/anthology/D18-1398/)

{% include MathJax.html %}


They suggest application from model-agnostic meta-learning to neuarl machine tralsation as follows:

![Gu et al. EMNLP 2018](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2020-06-17-Meta-Learning_for_Low-Resource_Neural_Machine_Translation/Meta-Learning1.PNG)

In this paper, they follow up on these latest approaches based on multilingual NMT and propose a meta-learning algorithm for low-resource neural machine translation. We start by arguing that the recently proposed model-agnostic meta-learning algorithm could be applied to low-resource machine translation by viewing language pairs as separate tasks. This view enables us to use MAML to find the initialization of model parameters that facilitate fast adaptation for a new language pair with a minimal amount of training examples. 

Furthermore, the vanilla MAML however cannot handle tasks with mismatched input and output. They use the universal lexical representation and adapting it for the meta-learning scenario.

They extensively evaluate the effectiveness and generalizing ability of the proposed meta-learning algorithm on low-resource neural machine translation. We utilize 17 languages from Europarl and Russian from WMT as the source tasks and test the meta-learned parameter initialization against five target languages (Ro, Lv, Fi, Tr and Ko), in all cases translating to English. 

There is I/O mismatch across language pairs.

One major challenge that limits applying meta-learning for low resource machine translation is that the approach outlined above assumes the input and output spaces are shared across all the source and target tasks. 

This, however, does not apply to machine translation in general due to the vocabulary mismatch across different languages. 

In multilingual translation, this issue has been tackled by using a vocabulary of sub-words or characters shared across multiple languages. 

This surface-level sharing is however limited, as it cannot be applied to languages exhibiting distinct orthography (e.g., IndoEuroepan languages vs. Korean.)

![Gu et al. EMNLP 2018](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/Translation/2020-06-17-Meta-Learning_for_Low-Resource_Neural_Machine_Translation/Meta-Learning2.PNG)

Illustration In Fig. 2, they contrast transfer learning, multilingual learning and meta-learning using three source language pairs (Fr-En, Es-En and Pt-En) and two target pairs (Ro-En and Lv-En).

Transfer learning trains an NMT system specifically for a source language pair (Es-En) and fine-tunes the system for each target language pair (RoEn, Lv-En). Multilingual learning often trains a single NMT system that can handle many different language pairs (Fr-En, Pt-En, Es-En), which may or may not include the target pairs (Ro-En, LvEn). 

If not, it finetunes the system for each target pair, similarly to transfer learning. Both of these however aim at directly solving the source tasks.

On the other hand, meta-learning trains the NMT system to be useful for fine-tuning on various tasks including the source and target tasks. 

This is done by repeatedly simulating the learning process on low-resource languages using many high-resource language pairs (Fr-En, Pt-En, Es-En).

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
In this paper, they propose to extend the recently introduced model-agnostic meta-learning algorithm (MAML, Finn et al., 2017) for lowresource neural machine translation (NMT). They frame low-resource translation as a metalearning problem, and we learn to adapt to low-resource languages based on multilingual high-resource language tasks. We use the universal lexical representation (Gu et al., 2018b) to overcome the input-output mismatch across different languages. They evaluate the proposed meta-learning strategy using eighteen European languages (Bg, Cs, Da, De, El, Es, Et, Fr, Hu, It, Lt, Nl, Pl, Pt, Sk, Sl, Sv and Ru) as source tasks and five diverse languages (Ro, Lv, Fi, Tr and Ko) as target tasks. 
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/D18-1398">The paper: Meta-Learning for Low-Resource Neural Machine Translation. Gu et al. EMNLP 2018</a>
</div>

# Reference 

- Paper 
  - [ArXiv version: Meta-Learning for Low-Resource Neural Machine Translation. Gu et al. EMNLP 2018](https://arxiv.org/abs/1808.08437)
  - [EMNLP version: Meta-Learning for Low-Resource Neural Machine Translation. Gu et al. EMNLP 2018](https://www.aclweb.org/anthology/D18-1398/)
  
 
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)

- For your information
  - [Meta-Learning: Learning to Learn Fast on Lil'Log](https://lilianweng.github.io/lil-log/2018/11/30/meta-learning.html)
  - [Learning to learn on BAIR](https://bair.berkeley.edu/blog/2017/07/18/learning-to-learn/)
  - [How to use Latex with latex4technics.com](https://www.latex4technics.com/?note=gw021j)
  - [MathJax on Stackexchange](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)
