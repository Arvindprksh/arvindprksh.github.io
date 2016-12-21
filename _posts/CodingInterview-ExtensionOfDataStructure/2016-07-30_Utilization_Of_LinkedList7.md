---
layout: post
title:  Measuring the length of a LinkedList and merging both of sorted linkedLists
subtitle: How can I find out if the length of a linkedList is odd or even and merge two sorted linkedList ?
category: Extenstion Of DataStructure
tags: [list]
permalink: /2016/07/30_Utilization_Of_LinkedList7/
---

I refer to the book, cording interview.

# brute-force 

  First of all, get the total length of List, and then do the length of list % 2.
  
  let's make pseudo code
  
```c
  bool FindOddOrEven (struct ListNode * head) {
      struct ListNode * temp = head;
      int count = 0;
      
      while (temp != NULL) {
            count++;
            temp = temp -> next;
      }
      
      if (count % 2 == 0)
          return true; // IF the list is even, return true;
      else 
          return false ; // IF the list is odd, rerturn false;
  }
```
  
  I can make the above code on another way to use the floyd cycle algorithm. 
  
  let's make pseudo code!
  
```c
  bool IsLinkedListIsLenghtEven (struct ListNode * head) {
            struct ListNode * temp = head;
            
        while (temp != NULL && temp -> next != NULL) {
            temp = temp -> next -> next;
        }
        
        if( temp != NULL )
            return false; // this means the list is odd;
        else 
            return true ; // this means the list is even;
  }
```
  
  
## can you think you can search for list at one time, i.e O(1).

  I think the list can, if List has hash table.
  
  In other words, when you make list. you have to make hash table with the list. 
  
# how to make another List with two list sorted. 

 If you want to know more, let me know , and I recommend [this site](http://www.geeksforgeeks.org/merge-two-sorted-linked-lists/)

```c
 List A : 1 -> 2 -> 8 -> 9 -> 10  & List B : 3 -> 4 -> 5 -> 12 -> 15
 you have to make another List with the above two list. 
```

 내가 보기에는 merge sorting과 비슷해 보인다. 합치는 부분에서 
 I thinkg it's like the merge part of merge sorting. 
 
```c
 here the insertion function of List put Node in the end of List. 
 
 struct ListNode * MergeList (struct ListNode * A, struct ListNode * B) {
    struct ListNode * tempA = A;
    struct ListNode * tempB = B;
    struct ListNode * mergeList = NULL;
 
    /// comparable part 
    While (tempA != NULL && tempB != NULL ) {
      
      if ( tempA -> data > tempB -> data) {
          mergeList.insertion(tempB);
          tempB = tempB -> next;
      }
      else if( tempA -> data < tempB -> data) {
          mergeList.insertion(tempA);
          tempA = tempA -> next;
      }
      else { // there are the same Nodes.
        mergeList.insertion(tempA);
        ergeList.insertion(tempB);
        
        tempA = tempA -> next;
        tempB = tempB -> next;
      }
    }
    
    // the rest part of List
    // tempA Is empty
    if (tempA == NULL ){
      // you have to processes list B
      while (tempB != NULL) {
          mergeList.insertion(tempB);
          tempB = tempB -> next;
      }
    }
      
    // the opposite side of the above tempA. 
    if (tempB == NULL) {
    
      while (tempA != NULL) {
          mergeList.insertion(tempA);
          tempA = tempA -> next;
      }
    }
  
  return mergeList;
 }
```
 
 Let's see the sample code of the book,"coding interview"
 
 just this book uses the recursive function. 
 
```c
 struct ListNode* MergeList(struct ListNode * a, struct ListNode * b ) {
        struct ListNode * result = NULL;
        
        if ( a == NULL)
          return b;
        else ( b == NULL)
          return a;
          
        if (a -> data <= b -> data) {
          result = a; 
          result -> next = MergeList(a-> next, b);
        }
        else {
          result = b; 
          result -> next = MergeList(a, b->next);
        }
        
    return result;
 }
```
 
 내가 보기에는 재귀적 함수의 활용성이 높을 수도 있다. 
 
 think about the recursive function. if You iterate. i.e If you repeat with the same way.  
 
