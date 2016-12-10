---
layout: post
title: Utilization Of LinkedList 10
subtitle: how Can I reverse the part of LinkedList with the size periodically, when I get a specific size 
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

 I just refer to [geeksforgeeks](http://www.geeksforgeeks.org/reverse-a-list-in-groups-of-given-size/)

# problem

  | Example :  
  | input : 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 and K = 3  
  | outPut : 3 -> 2 -> 1 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9  
  |   
  | input : 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 and K = 5  
  | output : 5 -> 4 -> 3 -> 2 -> 1 -> 6 -> 7 -> 8 -> 9  
  
  
# Algorithm

 1 ) you look for kth node. then reverse them.  
 2 ) reverse group  
 
```c
 struct noded * reverseList(struct ListNode * head) {
      struct ListNode * moveTemp = head;
      struct ListNode * newHead = NULL;
      struct ListNode * temp = NULL;
      
      while (moveTemp != NULL) {
        
        temp = moveTemp -> next;
        temp -> next = newHead;
        newHead = temp;
        moveTemp = moveTemp -> next;
      }
      
   return newHead;
 }
 
 struct ListNode * ReverseListNodeKth(struct ListNode * head, int k) {
    struct ListNode * temp = head;
    struct ListNode * restOfNodes = NULL;
    struct ListNode * firstHead = head; 
    
    // searching for kth node.
    while ( k != 1 ) {
         temp = temp -> next; 
         k--;
    }
    
    // split the list into two part. 
   restOfNodes =  temp -> next ;
   temp -> next = NULL;
   
   firstHead = reverseList(firstHead);
   
   head -> next = restOfNodes;
    
    
   return firstHead; 
 }
```
 
 after finishing the above process, just print the list. 
 

 
## geeksforgeeks' solution 

 this introduce the different thing a little. 

  | Example :   
  | input : 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 and K = 3   
  | outPut : 3 -> 2 -> 1 -> 6 -> 5 -> 4 -> 9 -> 8 -> 7   
  |   
  | input : 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 and K = 5   
  | output : 5 -> 4 -> 3 -> 2 -> 1 -> 9 -> 8 -> 7 -> 6   
 

## geeksforgeeks' solution 

 1) Reverse the first sub-list of size K. While reversing keep track of the next node and previous node.   
 Let the point to the next be __next__ and point to the previous node be __prev__.  
 2 ) head -> next = reverse(next, k) // recursively call for the rest of the List after that, link the two sub-lists.  
 3 ) return prev.  // prev becomes the new head of the list.   

```c
 /* Link List node */
 struct node {
      int data;
      struct node * next;
 };
 
 /* reverses the linked List in groups of size k and returns the pointer to the new head node. */
 struct node * reverse (struct node * head, int k) {
     struct node * current = head;
     struct node * next = NULL;
     struct node * prev = NULL;
     int count = 0; 
     
     
    /* reverse first K nodes of the linked List */
     While (current != NULL && count < k) {
      
          next = current -> next;
          current -> next = prev;
          prev = current;
          current = next;
          count++;
     }
     
     /* next is now a pointer to (k+1)th node Recursively call for the list starting from current And
     make rest of the list as next of first node
     */
     if (next != NULL)
       head -> next = reverse(next, k);
       
      /* prev is nes head of the input list */
      return prev;
 
 }
```
