---
layout: post
title: What is the MVC Pattern ?
subtitle: Summary of What MVC Pattern with my curiosity
category: Web Programming
tags: [pattern]
permalink: /2016/01/03/MVC_Pattern/
bigimg: 
  - "/img/Image/BigImages/carmel.jpg" : "Carmel-by-the-Sea, CA (2016)"
---

학습을 위해 <a href = "https://opentutorials.org/course/697/3828">생활코딩</a>을 참조하여 정리했습니다. 

- MVC란
 
 Model View Controller의 약자로 애플리케이션을 세가지의역활로 구분한 개발 방법론이다. 아래의 그림처럼 사용자가 Controller를 조작하면 Controller는 Model를 통해서 통해서 데이터를 가져오고 그 정보를 바탕으로 시각적인 표현을 담당하는 View를 제어해서 사용자에게 전달하게 된다. 
![](/img/Image/WebProgramming/2016-01-03-MVC_Pattern/MVC.png)

- Web에서 MVC 패턴을 사용하는 것을 보자 
  1. 사용자가 웹사이트에 접속한다. (Uses)
  2. Controller는 사용자가 요청한 웹페이지를 서비스하기 위해서 모델을 호출한다.(Manipulates)
  3. 모델은 데이터베이스나 파일과 같은 데이터 소스를 제어한 후 에 그 결과를 리턴한다.
  4. Controller는 Model이 리턴한 결과를 View에 반영한다. (Updates)
  5. 데이터가 반영된 View는 사용자에게 보여진다. (Sees)


즉, 요약을 해보자면 

 - Controller 
   사용자가 접근 한 URL에 따라서 사용자의 요청사항을 파악한 후에 그 요청에 맞는 데이터를  Model에 의뢰하고, 데이터를 View에 반영해서 사용자에게 알려준다. 

 - Model 
    일반적으로 데이터베이스 테이블에 대응된다. 데이버베이스를 통하여 데이터를 생성한다. 또는 페이지를 생성하기도 한다. 

 - View
    View는 클라이언트 측 기술인 html/css/javasript들을 모아둔 컨테이너이다. 


아래의 그림은 생활 코딩의 MVC 예제에 대한 설명을 그림으로 나타 낸것이다. 

![](/img/Image/WebProgramming/2016-01-03-MVC_Pattern/MVC_Example.gif)
