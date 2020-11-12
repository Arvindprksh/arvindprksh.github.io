---
layout: post
title: Attention-Guided Answer Distillation for Machine Reading Comprehension
subtitle: Title of paper - Attention-Guided Answer Distillation for Machine Reading Comprehension
category: NLP papers - Question Answering
tags: [neural network, machine reading comprehension, question answering]
permalink: /2020/09/08/Attention-Guided_Answer_Distillation_for_Machine_Reading_Comprehension/
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

This is a brief summary of paper for me to study and organize it, [Attention-Guided Answer Distillation for Machine Reading Comprehension. Hu et al. EMNLP 2018](https://www.aclweb.org/anthology/D18-1232/) I read and studied. 
{% include MathJax.html %}

This paper proposed a simple way to distill knowledge from teacher to student. 

The teacher model is large model, an anesmble model which is comprised of 12 single models with the indentical architecture but different initial parameter to obtain the ensemble.

Their model is robust to adversarial attack on Machine Reading Comprehension task. 

They suggest three ways to distill knowlege (i.e. Vanilla Knowledge Distillation, Answer Distillation, and Attention Distillation)

The vanilla knowledge distillation denote that instead of ground truths it uses out distribution from teacher. i.e. Vanilla knowledge distillation allows the student to learn knowledge from teacher. 

Answer distillation is used to prevent the student from make an over-confidence to confusing answer. 

Attention distillation is similar to distill intermediate representations to provide additional supervised signal for training the student network, However it used attention information in place of the intermediate representation. 

The following is overview of their appproach:

![Hu et al. EMNLP 2018](/img/Image/NaturalLanguageProcessing/NLPLabs/Paper_Investigation/MRC/2020-09-08-Attention-Guided_Answer_Distillation_for_Machine_Reading_Comprehension/Guided_attention_to_distill_knowledge.PNG)

<div class="alert alert-info" role="alert"><i class="fa fa-info-circle"></i> <b>Note(Abstract): </b>
Despite that current reading comprehension systems have achieved significant advancements, their promising performances are often obtained at the cost of making an ensemble of numerous models. Besides, existing approaches are also vulnerable to adversarial attacks. This paper tackles these problems by leveraging knowledge distillation, which aims to transfer knowledge from an ensemble model to a single model. They first demonstrate that vanilla knowledge distillation applied to answer span prediction is effective for reading comprehension systems. They then propose two novel approaches that not only penalize the prediction on confusing answers but also guide the training with alignment information distilled from the ensemble. Experiments show that their best student model has only a slight drop of 0.4% F1 on the SQuAD test set compared to the ensemble teacher, while running 12× faster during inference. It even outperforms the teacher on adversarial SQuAD datasets and NarrativeQA benchmark.
</div>
    
<div class="alert alert-success" role="alert"><i class="fa fa-paperclip fa-lg"></i> <b>Download URL: </b><br>
  <a href="https://www.aclweb.org/anthology/D18-1232/">The paper: Attention-Guided Answer Distillation for Machine Reading Comprehension. Hu et al. EMNLP 2018</a>
</div>

# Reference 

- Paper 
  - [arXiv version: Attention-Guided Answer Distillation for Machine Reading Comprehension. Hu et al. arXiv 2018](https://arxiv.org/abs/1808.07644)
  - [EMNLP version: Attention-Guided Answer Distillation for Machine Reading Comprehension. Hu et al. EMNLP 2018](https://www.aclweb.org/anthology/D18-1232/)
  
- How to use html for alert
  - [how to use icon](http://idratherbewriting.com/documentation-theme-jekyll/mydoc_icons.html)
    


