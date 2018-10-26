---
layout: page
title: Projects
subtitle: collections of what I have worked on with challenging works I was interested in.
tag: personal 
comments: true
css : /css/ForYouTubeByHyun.css
---

  When I have carried out a variety of fileds like IOT, Kernel, Web, Windows, Natural Language processing, Deep learning and so on. Currently, I am interested in NLP technologies with Deep Learning and Machine Learning. This page would shows you my projects.

## IOT Project

<div id="tutorial-section">

  <div id="tutorial-title">Smart refrigerator for people who are visually impaired</div>

  <ul class="nav nav-pills">
    <li class="active"><a data-toggle="tab" href="#refrigerator">Project video</a></li>
    <li><a data-toggle="tab" href="#refrigerator_concept">Concept video of this project</a></li>
  </ul>

  <div class="tab-content">
    <div id="refrigerator" class="tab-pane fade in active">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/Cgth5cEyfYA" frameborder="0" allowfullscreen></iframe>
    </div>
    <div id="refrigerator_concept" class="tab-pane fade">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/Szy-ek9KsbE" frameborder="0" allowfullscreen></iframe> </div>
  </div>
</div>

  - **[Smart Refrigerator to tell the location of a food to a person who is visually impaired - 시각장애인에게 반찬 위치를 안내하는 스마트 냉장고](https://www.youtube.com/watch?v=Cgth5cEyfYA)**
  
    - **[concept video](https://www.youtube.com/watch?v=Szy-ek9KsbE)** : this video show you why I tried to make this project.  
    - Langugeses : C#, Java, MySQL
    - Platforms :  Android, Windows 7, Emgu CV, [Open Source(Clipper)](http://www.angusj.com/delphi/clipper.php)
    - Tools : Visual Studio 2010, Eclipse
    - My role : developed and designed DataBase, Windows(UI) and the dish-regonition algorithm for dividing the dishes piled up into the indivisual dish
    - Description : I implemented IOT project with SAMSUNG ELECTRONICS' Home Appliances Business Department. This project,"Smart Refrigerator told the location of a food to a person who is visually impaired", targets people who visually imparied using the TTS & STT, vision.
     * The First Award(1st Award), IOT Competition supported by Samsung Electronics' Home Appliances Business Department
    
      Korean Ver. 이 프로젝트는 삼성전자 생활가전사업부 함께 IOT를 주제로 진행한 프로젝트입니다. 이 프로젝트의 target은 시각장애인을 대상으로  TTS&STT와 영상처리를 이용하여 시각장애인에게 반찬 위치를 알려주는 스마트 냉장고 프로젝트 입니다. 
    * 삼성전자 생활가전사업부가 주관한 IOT 공모전 1등상 수상
   
   
## Windows Project

<div id="tutorial-section">

  <div id="tutorial-title">Monitor Calibration</div>

  <ul class="nav nav-pills">
    <li class="active"><a data-toggle="tab" href="#calibration">Project video</a></li>
  </ul>

  <div class="tab-content">
    <div id="calibration" class="tab-pane fade in active">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/VV-9Z3wccQs" frameborder="0" allowfullscreen></iframe>
    </div>
  </div>
</div>


  - **[Monitor Calibration using smart phone device - 모니터 캘리브레이션](https://www.youtube.com/watch?v=VV-9Z3wccQs)**

    - Langugeses : C#, Java
    - Platforms :  Android, Windows 7
    - Target Device : galaxy 5
    - Tools : Visual Studio 2010, Eclipse, ADB(Android Debug Bridge)
    - My role : developed windows(UI), USB communication module and graphic card’s algorithm adjusting monitor' brightness, contrast and gamma of Windows application
    - Description : 모니터 연식이나 제조사 별로 모니터의 색상은 실제 색상가 다르게 표현이 됩니다. 이를 자동으로 조절하는 전문적인 장비가 있지만 가격이 상대적으로 비싸 보급형 모니터 캘리브레이션을 만들고자 진행한 프로젝트입니다. 대중화된 스마트 폰의 카메라를 센서로 하여 그래픽 카드의 look-up-table를 조절하여 사용자에게 모니터의 색상을 실제 색상과 같게 출력하도록 진행한 프로젝트 입니다. 
<!-- 이 프로젝트 **[파검드레스](http://www.segye.com/content/html/2015/10/18/20151018000778.html?OutUrl=naver)**  문제도 해결 할 수 있을 거라고 생각합니다.-->
    - Award : 
    전문적인 장비 Spider 4 Express와 이 프로젝트의 프로그램 성능을 비교한 결과 Spider 4 Express와 이 프로그램을 2~3회 반복 수행 시 모니터의 색상 출력은 유사했습니다. 이때, 색상의 정확도를 측정하기 위한 장비로 비교한 결과 입니다. 
    * 제 27회 글로벌 SW 공모대전(2015) 전자신문 사장상 수상
    

## Kernel Project
  
<div id="tutorial-section">

  <div id="tutorial-title">big.LITTLE Architecture</div>

  <ul class="nav nav-pills">
    <li class="active"><a data-toggle="tab" href="#bigLITTLE">Project video</a></li>
  </ul>

  <div class="tab-content">
    <div id="bigLITTLE" class="tab-pane fade in active">
      <iframe width="560" height="315" src="https://www.youtube.com/embed/K1lXRJxumwQ" frameborder="0" allowfullscreen></iframe>
    </div>
  </div>
</div>  
  
  - **[Cutomizing Governor in big.LITTLE Architecture - KBG : Kangbuk Governor](https://www.youtube.com/watch?v=K1lXRJxumwQ)**
  
    - Langugeses : C/C++, Java
    - Platforms : Android, Linux, ORDROID-XU+E 
    - Tools : Eclipse, Windows 7, ADB(Android Debug Bridge)
    - My role : developed the Governor's algorithm using the DVFS(Dynamic Voltage frequency scaling) and analyzed the kernel source. and Tested my Governor alogrithm
    - Description : 
    현재 스마트 폰에서 배터리의 효율성이 가장 큰 화두입니다. 이를 위해 ARM big.LITTLE Architecture라는 저전력 Architectur를 개발했습니다. 이를 적용한 스마트 폰을 삼성전자, LG 전자에서 출시하고 있지만 실제 전력의 효율성은 좋지가 않습니다. 이는 소프트웨어가 하드웨어를 제대로 활용하도록 개발이 되지 않아서 입니다. 이러한 상태에서 "어플리케이션 별로 최적의 주파수를 설정하자"란 컨셉으로 스마트 폰의 배터리 효율성 개선을 위해 진행한 프로젝트입니다.
    - Result :
    이 프로젝트대로 설계한 Governor를 이용하여 소비전력은 30%이상 감소했습니다.
   <!-- * 제 12회 임베디드 소프트웨어 경진대회(2014) 본선 진출 -->

## Android & Web Application Project
   
  - **[Making Github Page - hyunyoung2.github.io : Currently, this web page](https://hyunyoung2.github.io)**
  
    - Langugeses : Javascript, html(css), ruby<!--, Markdown, liquid -->
    - Platforms :Jekyll, github, hugo
    - Tools : git, Xcode, Mac OS
    - My role : developed github page alone using Open-Source Static Site Generator(Jekyll) and I used hugo as addition to Jekyll which is another pen-source static site generators(Hugo).
    - Description :
    나만의 이력 및 프로젝트 관리의 위해 그리고 웹 프로래밍을 경험을 위해 진행한 프로젝트입니다.

  - User Customizing the wrong English note - User Cumstomizing 영어 오답노트

    - Langugeses : PHP, MySQL, Java, JavaScript, html(css)
    - Platforms : Android, Aphache, Web
    - Tools : Eclipse, Sublime text, Notepad++
    - My role : developed Sever for communicating server with Android & web applications and Database stored the parsing data from PDF file tranformed into HTML file 
    - Description :
    현재 오답노트 어플리케이션은 사용자들이 사용하기가 많이 불편한 상태로 되어있습니다. 예를 들어 사진촬영을 해서 저장을 하거나 모의고사의 문제를 완변하게 제공하지 않는 형태로 제공되고 있습니다. 이 프로젝트는 스마트 폰과 웹으로 어디서나 사용자가 영어 문제 오답노트를 작성할 수 있도록 제공하는 프로젝트입니다. 스마트 폰은 오답노트 작성만 제공하고, 웹에서는 오답노트를 작성하고 이를 출력하는 형태 제공합니다.


## Natural Language Processing Project

  - **Korean Dependency Parsing by using Transition-based Deep Learning Techonology**

    - Langugeses : python
    - Platforms : Ubuntu16.04, Tensorflow
    - Tools : vim, jupyter notebook
    - My role : developed the parsing algorithm based on Neural network(Bi-LSTM), the whole methodology of how to parse Korean Sentence to dependency structure(arc-eager and backward based on Head-final rule of Korean Language of transition base).
    - Publication & Award: 
     1. 0000 [\[Paper\]](), [\[Slide\]]()

  - **Compound Noun Decomposition by using Bi-LSTM and Linear-chain CRF**

    - Langugeses : python
    - Platforms : Ubuntu16.04, Tensorflow
    - Tools : vim
    - My role(alone) : In order to separate the compoun noun to unit nouns, used BI-LSTM encoder and Linear-chain CRF model.
    - Publication & Award: 
     1. The KIPS(Korea Information Proceeding Society) FALL CONFERENCE(11/02/2018) 
        Title - Compound Noun Decomposition by using Bi-LSTM and Linear-chain CRF. [\[Paper\]](), [\[Slide\]]()
     2. Excellence Award in "Automatic Spacing and Compound Noun Decoposition : 2018 Korean Natural Language Processing Contest"
     - Reference of the performance & result When comparing to other models : Jin-Hyuk Choi, Pum-Mo Ryu, Hyo-Jung Oh, "[Overview of Automatic Spacing and Compound Noun Decomposition: 2018 Korean Natural Language Processing Contest](), " Proceedings of the 30th Annual Conference on Human and Cognitive Language Technology, pp. 193-196, 2017.


  - **Bi-LSTM-CRF and Syllable Embedding for Automatic Spacing of Korean Sentences**

    - Langugeses : python
    - Platforms : Ubuntu16.04, Tensorflow
    - Tools : vim
    - My role(alone) : used Neural Network methodology calle BI-LSTM-CRF for automatic spacing of Korean sentences
    - Publication & Award: 
     1. The 30th Anuual Conference on Human & Cognitive Language Technology(10/13/2018) 
        Title - Bi-LSTM-CRF and Syllable Embedding for Automatic Spacing of Korean Sentences. [\[Paper\]](), [\[Slide\]]()
    - Reference of the performance & result comparing to another model : Jin-Hyuk Choi, Pum-Mo Ryu, Hyo-Jung Oh, "[Overview of Automatic Spacing and Compound Noun Decomposition: 2018 Korean Natural Language Processing Contes](), " Proceedings of the 30th Annual Conference on Human and Cognitive Language Technology, pp. 193-196, 2017. 
     
  - **Open source project : Konlp(Korean Natural Language toolkit)**
  
    - Langugeses : python
    - Platforms : Ubuntu16.04, Tensorflow
    - Tools : vim, jupyter notebook
    - My role : designed and developed the structure of the open source call KoNLP such as how to contribute and test with test module, automatic build system, code checking, and documentation using [SPHINX](http://www.sphinx-doc.org/en/master/) with readthedoce as tech leader in NLP lab of Kookmin university. [\[Github\]](https://github.com/konltk/konlp), [\[Web page\]](https://www.konltk.org/)
    - Publication & Award: 
     1. The 30th Anuual Conference on Human & Cognitive Language Technology(10/13/2018) 
        Title - KoNLTK: Korean Natural Language Toolkit. [\[Paper\]](), [\[Slide\]]() 

  - **Deep Learning Method of keyword generation by using Doc2Vec and Word2Vec**

    - Langugeses : python, C 
    - Platforms : Ubuntu16.04, Tensorflow
    - Tools : vim, jupyter notebook
    - My role(alone) : this projecto is for goal which is the generation of the keyword of document using word2vec and doc2vec, I construct the doc2vec as adding the word2vec of words in the document and then generated the representative keyword of the document comparing doc2vec and word2vec.
    - Publication & Award:
     1. 2nd prize in Poster Presentation(IC-LYCS2018) by Asia Pacific Society for Computing and Information Technology(02/11/2018). [\[Poster\]]()
 

  - **spam text messagg filtering by using Sen2Vec and Feedforward Neural Network**
    
    - Langugeses : python, C 
    - Platforms : Ubuntu16.04, Tensorflow
    - Tools : vim, jupyter notebook
    - My role(alone) : developed and researched all of things related to "Spam Text Filtering by Using Sen2Vec and FeedForward Neural Nework". the project is classify whether the text message is the spam or not using neural network.
(Kor ver): 문장 벡터와 전방향 신경망을 이용한 스팸 문자 필터링 연구를 진행하였다.
    - Publication & Award: 
      1. The 29th Anuual Conference on Human & Cognitive Language Technology(10/14/2017) 
        Title - Spam Text Filtering by Using Sen2Vec and Feedforward Neural Network. [\[Paper\]](http://ocean.kisti.re.kr/IS_mvpopo213L.do?ResultTotalCNT=72&pageNo=6&pageSize=10&method=view&acnCn1=&poid=sighlt&kojic=OOGHAK&sVnc=y2017m10a&id=0&setId=&iTableId=&iDocId=&sFree=&pQuery=%28kojic%3AOOGHAK%29+AND+%28voliss_ctrl_no%3Ay2017m10a%29), [\[Slide\]](https://www.slideshare.net/HyunYoungLee3/spam-text-message-filtering-by-using-sen2-vec-and-feedforward-neural-network-119298956)
      2. The 4th Annual conf. on Computational Science & Computational Intelligence(CSCI 2017)-(12/16/2017)
        Title - Spam Message Filtering by Using Sen2Vec and Feedforward Neural Network

  - **Recommending Word in text which is A B x C D**
    
    - Langugeses : python(3.6)
    - Platforms : Window10 
    - Tools : spyder 3.1.2
    - My role(alone) : this project is toy project, which recommend the best X word, if You have the text which is "A B x C D". I used statistics of n-gram frequency. <a href="https://github.com/hyunyoung2/Hyunyoung2_Recommending_System/tree/master/Python/3.6">[github]</a>.

 
  - **[COPYDET : Plagiarism Detected Source Retrieval and Text Alignment - 원본 문서 추출 및 표절 위치 탐색 기법 ](https://www.youtube.com/watch?v=prBhnX2CQbM&feature=youtu.be)**
    
    - Langugeses : Python
    - Platforms : Windows 7
    - Tools : Python GUI
    - My role : developed & designed this project's algorithm and done this project as leader 
    - Description :
    영어 문서간의 표절검사를 진행하는 프로젝트입니다. 먼저 Database에서 의심 문서와 가장 유사한 원본 문서 후보군을 추출에 TF-IDF를 이용합니다. 이후 추출된 원본문서와 의심문서 쌍의 후보 문서들을 정밀 비교하여 의심 구간을 찾는 알고리즘을 연구 개발을 합니다. 정밀 비교 부분에서는 단어기반 문서간의 유사도와 코사인 유사도 등 다양한 알고리즘을 적용해 보며 선택한 것은 단어 기반의 매칭 알고리즘으로 이를 가지고 정밀 비교를 진행했습니다. 
    - Publication & Award :
    이 프로젝트는 제 26회 한글 및 한국어 학술대회(2014.10)와 국회도서관(2015.06)이라는 학술지에 논문을 게재했습니다.
   <!-- PAN 2014 conpetition 출전 -->


## Term Project

  - Making Mini C-compiler
   
    - Langugeses : C.
    - Platforms : Lex, Yacc, cygwin. 
    - Tools : Visual Studio, Notepad++.
    - My role(alone) : developed Mini-C complier alone.
    - Description :
    현존하는 컴파일러와 같이 나만의 C언어를 설계하고, 이 언어로 생성된 코드를 syntax를 검사하여 파스 트리를 출력하는 프로젝입니다. 

  - BigData Visualization
  
    - Langugeses : C/C++, Javascript.
    - Platforms : windows 7. 
    - Tools : Visual studio, Notepad++.
    - My role : developed javascript program visualizing bigdata from the Tweeter using sigma library.
    - Description :
    정보검색과 데이터 마이닝 수업에서 term project로 빅데이터 시각화 프로젝트를 진행했습니다. 단순히 트위터에서 생성된 데이터 중 텍스트를 기준으로 연관성을 표시하는 빅데이터 시각화 프로그램을 작성했습니다. 

  - And on so. I have carried out different field's project more than term projects above during undergraduate. 
