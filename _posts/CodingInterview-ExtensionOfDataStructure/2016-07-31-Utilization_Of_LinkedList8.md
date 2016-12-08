---
layout: post
title: Utilization Of LinkedList 8
subtitle: How to change the singly LinkedList pairwise
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

I refer to [geeksforgeeks](http://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list/)

# First Problem

```
  List A : 1 -> 2 -> 3 -> 4 -> X
              | after some function 
  List A : 2 -> 1 -> 3 -> 4 -> X
```
  
  In other words, you have to reverse Node of the list in two units
  
  How can you solve the above problem. 
  
  my first algorithm, 
  
  1. First Of all, calculate the length of List 
  2. current node exchange the next node
  3. move second step
  
  but The above algorithm is too slow, 

  So I will change the algorithm a little bit. 
  
  1. when moving head pointer, you have to move two times at once.
  2. any time you move the pointer of head, just chang two of nodes.
  3. during this operation, you have to continue until head is NULL or head -> next is null 

  let's make psuedo code
  
```c
struct ListNode * ReversePairsInterative (struct ListNode * head){
  struct ListNode * temp = head;
  struct ListNode * beforeTwoNode=NULL;

  while(temp != NULL && temp -> next != NULL){
    
    struct ListNod * exch = temp -> next;
    
    temp -> next = temp -> next -> next;
    exch -> next = temp;
    
    if (beforeTwoNode != NULL) {
        beforeTwoNode -> next = exch;
    }
    
    beforeTwoNode = temp;
    temp = temp -> next;
  }
  return head;
  }
```
  
  If you want to understand with pictures, please refer to the following. 
  
```
  List A : 1 -> 2 -> 3 -> 4 -> X
              | for one cycle.
              
          temp   exch
            |     |  
  List A :  2 ->  1 ->  3 ->  4 ->  X
  
          exch   temp
            |     |  
  List A :  1 ->  2 ->  3 ->  4 ->  X  
  
              beforeTwoNode
          exch    |    temp
            |     |     |
  List A :  1 ->  2 ->  3 ->  4 ->  X  
```
  
## Another way to solve this problem in coding interview.
 
  I refer to coding interview book. 

### First, you can use the recursive function. 

```c
  void ReversePairRecursive(struct ListNode * head) {
  
    struct ListNode * temp;
    if ( head == NULL || head -> next == NULL) 
          return;
          
    else {
        temp = head -> next;
        head -> next = temp -> next;
        temp -> next = head;
        ReversePairRecursive(head -> next);
    }
  }
```

 following is explaining about the above source code. 

```
  List A : 1 -> 2 -> 3 -> 4 -> X
              | for one cycle.
          head   temp
            |     |  
  List A :  2 ->  1 ->  3 ->  4 ->  X
          temp   head
            |     |  
  List A :  1 ->  2 ->  3 ->  4 ->  X  
  // here is end of on cycle 
  // below is another cycle
                       head  temp
                        |     |
  List A :  1 ->  2 ->  3 ->  4 ->  X  
                       head  
                        |    
  List A :  1 ->  2 ->  3 ->  X  
                     /
                  4             
```
  
  I think this code is strage, needless to say, frame of linked list break. 
  
  So I think just my above algoritm is much better, first algorithm. 
  
### Second, the entire frame is same, the difference is usint iteration for recusive function.

```c
// iteration version 
void ReversePairIterative(struct ListNode *head) {
  struct ListNode *temp, temp2, *current = head;
  while(current != NULL && current -> next != NULL) {
      temp = current -> next;
      temp2 = temp -> next;
      temp -> next = current;
      current -> next = temp2;
      if (current != NULL)
          current = current -> NULL;
  }
}
```
  
maybe if I expresss the above algorithm with drawing. 

```
  List A : 1 -> 2 -> 3 -> 4 -> X
              | for one cycle.
              
         current temp temp2
            |     |     |
  List A :  2 ->  1 ->  3 ->  4 ->  X
  
          temp  current temp2
            |     |     |
  List A :  1 ->  2 ->  3 ->  4 ->  X  
  // here is end of on cycle 
  // below is another cycle
                    current  temp  temp2
                        |     |     | 
  List A :  1 ->  2 ->  3 ->  4 ->  X  
                      current temp2 
                        |     |
  List A :  1 ->  2 ->  3 ->  X  
                     /
                  4 
                  |
                 temp
```
  
 As you can see the above result, I think this function also is different from the orginal opinion of author.
 
 Just If you only change the data of node. the above algorithm is perfect. 
 
 IF you want to know why it is correct. please refer to [this site](http://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list/)


###  The best way I think 

 get rid of the thought of changing nodes, Just you have to change just data of node. 

```c
 void ReverseLinkList(struct ListNode *head) { 
   struct ListNode * temp= head;
   
   while (temp != NULL && temp -> next != NULL) {
    
      swap (temp, temp->next);; // this function only switch the data in node.  
   
      temp = temp -> next -> next;
   }
 }
```
