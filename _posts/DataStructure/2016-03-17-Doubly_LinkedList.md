---
layout: post
title: Summary of Duobly LinkedList
subtitle:
css:
tags:
date:
big-image:
share-image:
permalink:
comments:
show-share:
big-image:
meta-title:
meta-description:
---
윤성우의 열혈자료구조를 참고하여 만들었습니다. 

1-1. 양방향 연결리스트에도 여러가지 종류가 있다. 
    
    - 기본적인 양향연결리스트 
    - 더미노드양방향 연결리트스 
    - 원형 연결기반의 양향 연결리스

![](/img/Image/DataStructure/2016-03-17-Doubly_LinkedList/double_linked_list.png)

![](/img/Image/DataStructure/2016-03-17-Doubly_LinkedList/doubly LinkedList.png)

1-2. 양방향으로 연결을 하면 검색이 용이하다. 단방향 보다

아래는 양방향 연결 리스트의 탐색부분을 보여준다. 

위의 양방향 연결리스트의 그림을 보면 복잡하지만 코드를 보면 간단하다.

![](/img/Image/DataStructure/2016-03-17-Doubly_LinkedList/doubly LinkedList1.png)

아래의 그림은 앞으로 구현을 할 양방향 연결리스트의 모형이다. 

![](/img/Image/DataStructure/2016-03-17-Doubly_LinkedList/doubly LinkedList2.png)

이제 아래 함수를 보면 양방향 연결리스트의 ADT를 알 수 있을 것이다. 

![](/img/Image/DataStructure/2016-03-17-Doubly_LinkedList/doubly LinkedList3.png)


아래의 그림은 양방향 연결리스트의 활용한 예를 보여준다. 

![](/img/Image/DataStructure/2016-03-17-Doubly_LinkedList/doubly LinkedList4.png)


양방향 연결 리스트이 초기화 부분

![](/img/Image/DataStructure/2016-03-17-Doubly_LinkedList/doubly LinkedList5.png)

양방향 연결리스트이 노드 사입 부분

![](/img/Image/DataStructure/2016-03-17-Doubly_LinkedList/doubly LinkedList6.png)

양방향 연결리스트의 노드 첫번째 노드 삽입 부분

![](/img/Image/DataStructure/2016-03-17-Doubly_LinkedList/doubly LinkedList7.png)

양방향 연결리스트의 두번째 이후 노드 삽입 부분

여기서 양방향의 연결이 되도록 해준다. 그리고 노드는 head 앞으로 삽입을 한다. 

![](/img/Image/DataStructure/2016-03-17-Doubly_LinkedList/doubly LinkedList8.png)

양방향 연결리스트이 검색 부분 - 검색을 할때 before이 불필요하다. 거의 알아서 cur 하나로 

참조를 할 수 있기 때문이다.

![](/img/Image/DataStructure/2016-03-17-Doubly_LinkedList/doubly LinkedList9.png)
