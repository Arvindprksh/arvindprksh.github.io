---
layout: post
title: a test set of syntactic and semantic question for word embedding performance
subtitle: Translating the syntactic and semantic question to Korean
category: Natural Language Processing Labs
tags: [nlp, word2vec]
permalink: /2018/04/07/Syntactic_and_Semantic_set/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/monterey.jpg" : "Monterey, CA (2016)"
  - "/img/Image/BigImages/stanford_dish.jpg" : "Stanford Dish, CA (2016)"
  - "/img/Image/BigImages/marian_beach_in_sanfran.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/carmel2.jpg" : "Carmel-by-the-Sea, CA (2016)"
  - "/img/Image/BigImages/marina.jpg" : "MRINA of San Francisco, CA (2016)"
  - "/img/Image/BigImages/sanfrancisco.jpg" : "San Francisco, CA (2016)"
---

After I read the paper, Efficient Estimation of Word Representations in Vector Space titled.

I think I need to make the test set of syntactic and semantic qeustion into another language.

In particular, I want to translate the test set into Korean language. Becuase I am researcher of Korean language NLP. 

But If you guys use this respository I store with work I did. you can translate the test set into another language including language set the module, googletrans is providing. 


First, git clone the Hyunyoung2 [Korean test set v1](https://github.com/hyunyoung2/Hyunyoung2_Korean_test_set_v1)

and then run **Download_test_set.sh** under Efficient_Estimation_of_Word_Representations_in_Vector_Space dir in English dir. 

you will get the text file, word-test.v1.txt like this:

> ./Download_test_set.sh

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2018-04-07-Syntactic_and_Semantic_set/word-test-v1.png)

Second, run the python script, **google_trans.py**.

before running **google_trans.py**, After enter the paper directory, run the script as follows:

> python3 google_trans.py

The directory is Efficient_Estimation_of_Word_Representations_in_Vector_Space.

In my case, I normally use python3, so I run the python script above with python3. 

If you want to see the code, You could check [my repository](https://github.com/hyunyoung2/Hyunyoung2_Korean_test_set_v1)

just I did programming on **google_trans.py**, I verified the python script with [pylint](https://www.pylint.org/)

The following is just information about using pylint. 

- with pip3 install pylint, i.e. python package for python3 

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2018-04-07-Syntactic_and_Semantic_set/pip3_pylint.png)

- with apt-get install pylint i.e. ubuntu package

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2018-04-07-Syntactic_and_Semantic_set/ubuntu_apt_pylint.png)

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2018-04-07-Syntactic_and_Semantic_set/ubuntu_apt_pylint2.png)

Finally, after running the python script, **google_trans.py**, the result is as follows:

![](/img/Image/NaturalLanguageProcessing/NLPLabs/2018-04-07-Syntactic_and_Semantic_set/Korean_word_test_v1.png)

After I finished this job, I think that has error on syntactic qeustions, Later I have to fix this data of syntactic question to Korean Language.

Another problem is unigram in english is tuned into bigram or trigram in Korean after tranlating as follows:

Georgetown -> ?????? ??????

Later I will resolve it. 

# Reference 

 - [Python package googletrans 2.2.0](https://pypi.python.org/pypi/googletrans)
 
 - [googletrans's official site](http://py-googletrans.readthedocs.io/en/latest/)

 - [Efficient Estimation of Word Representations in Vector Space](https://arxiv.org/abs/1301.3781v3)

 - [The test set in the paper above](http://www.fit.vutbr.cz/~imikolov/rnnlm/word-test.v1.txt) 
  
 - [My Explanation of the paper, Efficient Estimation of Word Representations in Vector Space](https://hyunyoung2.github.io/2018/04/06/Efficient_Estimation_of_Word_Representations_in_Vector_Space/)
 
 - [The my github repository I stored for this job](https://github.com/hyunyoung2/Hyunyoung2_Korean_test_set_v1)
 
 - [pylint](https://www.pylint.org/)
