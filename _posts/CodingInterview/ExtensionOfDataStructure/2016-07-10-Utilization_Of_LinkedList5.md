---
layout: post
title: How can I find out intersection of two LinkedList ?
subtitle: Where is the intersection of two LinkedList
category: Extenstion Of DataStructure
tags: [list]
permalink: /2016/07/10/Utilization_Of_LinkedList5/
---

# intersection of two list 

 just I recommend you to refer to [geeksforgeeks](http://www.geeksforgeeks.org/write-a-function-to-get-the-intersection-point-of-two-linked-lists/)

 for example, 
 
```
  A:          a1 → a2   
                     ↘   
                      c1 → c2 → c3   
                     ↗               
  B:     b1 → b2 → b3   
```

in the above case, how can you find c1 without any information ??????

just in this case, you cas get just lits is only linked list and don't have Loop.

->즉 전제 조건은 리스트 들은 각각 링크드 리스트 그리고 순환 구조가 아니라고 해보자.


##   brute-force

 - 단순한게 만나는 점을 찾으면 되기 때문에, 이중 Loop를 이용하면 된다. 
 - just try to find intersection of List, so just using two of Loop is the simple solution.

 let's make psuedo code

```c
 void intersectionOfLinkedList (ListNode * A, ListNode *B){
     for( the length of List A ) {
        for ( the lengthn of List B ) {
               if( address of Node of List A == address of Node List B) {
                       printf("the same address : address of Node of list")
               }
        }
     }
  printf(" there is no the same address") // this means theres is no intersection.
 }
```

 If you want to improve more the above algorithm, just find out the shortest length of both of above them.
 
 let's say make pseudo code
 
```c
 void intersectionOfLinkedList (ListNode * A, ListNode *B){
  
   here is you have to calculate the length of the two lists after that, you find out the shortes length of the both.
   
   and the shortest length is List A in next for statement.
 
      // from first to end
     for( the length of List A ) {
        for ( the lengthn of List B ) {
               if( address of Node of List A == address of Node List B) {
                       printf("the same address : address of Node of list")
                       return;
               }
        }
     }
  printf(" there is no the same address") // this means theres is no intersection.
 }
```


## how to use hash table

  let's make psuedo code
  
```c
  void whereIsIntersectionInBothOfList (ListNode *A, ListNode *B) {
        
        // first 
        arrA[hash(each Node of List A)] = address of each Node of List A;
        
        // from first to end
        for ( the length of List B ) {
              if( arrA[hash(ech Node of List)] == address of each Node of List B) {
                        printf("there is intersection between List A and List B");
                        return ;
              }
        }
        
     printf("there is no intersection between List A and List B");
  }
```

## If you use the stack to solve this problem about intersection of the two lists.

 yes, you can use the stack to solve this problem. 
 
 1. 각 리스틑 스택에 집어 넣고 그 다음 top의 위치를 비교하여 다를 때가지 비교한다. 
 
 
 let's make pesudo code

```c
 struct ListNode * IsIntersectionOfLits (struct ListNode * A, struct ListNode *)
 {
      Stack A, B;
      struct ListNode * tempA = NULL, tempB = NULL;
      struct ListNode * intersection = NULL;
      
      // first,  get StacK the total Node of each listNode 
      while (tempA != NULL) {
           A.push(tempA->Node);
           tempA = tempA-> next;
      }
      
      while (tempB != NULL) {
           B.push(tempB -> Node);
           tempB = tempB-> next;
      }
      
      // Second, comare the tops from the Stacks. 
      while ( A.empty() != false && B.empty() != false ) {
           if ( A.top != B.top)
              break;
           else 
               intersection = A.top or intersection = B.top;
          A.pop();
          B.pop();
      }
      return intersection; 
 }
```

## Another way

  1. 두 리스트 중 작은 길이만큼만 비교 즉, 각 리스트 길이를 구하고 그 다음에 두리스트의 길이의 차를 구해서 
  
  2. 긴 리스트를 차이만큼 움직이고 나서 
  
  3. 각 리스트의 노드가 동인한지 비교를 해본다. 

```c
  struct ListNOde * findIntersectingNode( struct ListNode * A, struct ListNode * B)
  {
     ListNode tempA=A;
     ListNode tempB=B;
     int lenOfTempA = 0;
     int lneOfTempB = 0; 
     int differenceOfTwoLen = 0;
     ListNode * intersection = NULL; 
     // first, you have to calculate the length of two lists. 
     
     while (tempA != NULL) {
       lenOfTempA++;
       tempA = tempA -> next;
      }
  
     whil (tempB != NULL) {
       lenOfTempB++;
       tempB = tmepB -> next;
     }
     
     // Second, difference of length of two list 
     // here I allocate tempA the longer List/
     if ( lenOfTempA < lenOfTempB ) {
           tempA = tmpeB;
           tempB = TempA;
           differenceOfTwoLen = lenOfTempB - lenOfTempA;
      }
     else {
       tempA = tempA;
       tempB = tempB;
       differenceOfTwoLen = lenOfTempA - lenOfTempB;     
     }
     
     // now you have to move the longer list by differenceOfTwoLen 
     for(int i = 0 ; i < differenceOfTwoLen ; i++) {
          tempA = tempA->next;
     }
     
     // finally, you have to compare whether two list is indentical. 
     while (tempA != NULL && tempB != NULL) {
          if (tempA -> data == tempB ->  data) {
                 intersection = tempA or intersection = tempB
                 break;
          }
          else {
               tempA = tempA -> next;
               tempB = tempB -> next;
          }
     }
    return intersection; 
  }
```
