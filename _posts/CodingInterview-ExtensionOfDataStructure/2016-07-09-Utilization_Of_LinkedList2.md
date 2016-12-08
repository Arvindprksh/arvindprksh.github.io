---
layout: post
title: Utilization Of LinkedList2
subtitle: how can I check that the LinkedList is rotation or not ?
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

do you think single linked list is Loop or not ????

what is way to indentify the Loop of List in single Linked List ???

### Brute-Force 
 
 무식하게 푸는 방법, 
 
 what variable of next points to is different, so you have to searching for the whole linked List.
 
 and then you have to check if a node is indicated from a two of node.
 
 -> 싱글 링크드 리스트에서는 next가 가리키는 노드가 하나이다. 그러므로 만약에 하나의 노드가 두개의 next를 얻는다면
 
 -> 이건 순환 구조라고 볼수 있다. 
 
 -> 가장 무식한 방법 현재 노드로 다시 돌아 오는지 확인을 하는 것인데 이것은 순환 구조에 현재 노드가 포함이 될때 가능한 방식이다. 
 
 -> 전체 탐색을 하면서 탐색한 노드인지 아닌 지를 확인을 해봐야 한다. ----> 이게 현재 합리적인 방식으로 생각을 한다. 
 
### way to use the hash table. 

  -> identify hash value, so if you find the same value of hash, then list is Loop
   
### finding Loop of list at O(n)  

 this is floyd cycle finding algorithm. 
 
 두 개의포인터를 가지고 하나는 빠른 속도로 달리고 그다음 하나는 느린 속도로 간다면 결국에는 만난다는 이야기 입니다. 
 
```c
 int IsLinkedListContainsLoop (struct ListNode * head) {
  
    struct ListNode * fastNode = head; two times than slow Node
    struct ListNode * slowNode = head;
 
    while(fastNode != NULL && slowNode != NULL) {
        
        fastNode = fastNode -> next;
        
        if (fastNode == slowNode)
            return true;
            
        fastNode = fastNode -> next;
        
        if (fastNode == NULL)   /// 이건 나도 미처 생각을 못한 부분이다. 
            return false;
            
        if (fastNode == slowNode)
            return true;    
            
        slowNode = slowNode -> next;
    }
    
    return false;
 
 }
```
 
### List contains Loop or not, if true, where is location to start Loop

  -> 리스트가 순환인지 아닌지 확인하고, 순환이라면 어디서 순환이 시작을 하는 지를 구하시요
  
  -> if you want to verify this algorithm, just click to [this site](http://makefortune2.tistory.com/7)
  
  m = 순환까지의 거리 (찾아야 할 값)

  n = 순환 루프의 길이

  k = 순환 시작점에서 토끼와 거북이가 만난 자리까지의 거리
  
  이것을 가지고 비교를 하면된다. 즉 순환까지의 거리와 K부터 순환 시작점까지 거리와 m이 같으면 된다. 
  
  If you are looking for verification about this theory, just click to [this site](https://nol2soft.wordpress.com/2013/07/13/linked-list-cycle-detection-explanation/)
  
  If you can make function of the above problem. as following 
  
``` c
 int FindBeginningOfLoop (struct ListNode * head) {
    struct ListNode * fastnNode = head, slowNode = head;
    int loopExits = 0
    
    while ( fastNode != NULL && slowNode != NULL) {
      
      fastNode = fastNode -> next;
      
      if (fastNode == slowNode) {
       loopExits = 1;
        break;
      }
      
      if (fastNode == NULL)
          break;
      fastNode = fastNode -> next;
      
      if (fastNode == slowNode) {
       loopExits = 1;
        break;
      }
      slowNode = slowNode -> next;
    }
    
    if (loopExits == 1) {
        int count =0;
        slowNode = head;
        
        while (slowNode == fastNode) {
           count++;
           slowNode = slowNode -> next;
           fastNode = fastNode -> next;
        }
        
        return slowNode;
    }
    
    return NULL;
 }
```

 think about when speed of fastNode and slowNode is that fastNode = 3 and slowNode = 2, then do floyd finding cycle algorithm work??
 
   -> It will work, of course
   
   
