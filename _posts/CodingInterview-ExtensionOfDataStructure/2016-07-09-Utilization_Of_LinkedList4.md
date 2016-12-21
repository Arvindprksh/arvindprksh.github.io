---
layout: post
title: How can I reverse the LinkedList ?
subtitle: How can I reverse LinkedList and Putt a node in sorted LinkedList
category: Extenstion Of DataStructure
tags: [list]
permalink: /2016/07/09/Utilization_Of_LinkedList4/
---

# In the case of putting node in sorted Linked list

 right away make code.
 
 for example, head -> 2 -> 4 -> 5 -> 6 -> null 
 
 if I have to put 3 Node, where do I have to put it ????
 
```c
 struct ListNode * InsertInSortedList (struct ListNode * head, struct ListNode * newNode) {
  
 struct ListNode * current = head, temp;
 
 if ( current == NULL) 
    return head -> next = newNode;
 
 while ( current -> data < (newNode-> data && current != NULL)) {
    // key point
    temp = current;
    current = current -> next;
 }
 
       newNode -> next = temp -> next;
       temp -> next = newNode;
       
       return head;
 
 }
```

# Reverse of singly linked List

  if you want to know about reversing the list. click please [this site](http://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/)


  input :  
 head -> 1 -> 2 -> 3 -> 4 ->  5 -> NULL 
 
 output :
 I have to change this to 
 
 head -> 5 - > 4 -> 3 -> 2 -> 1 -> NULL

 just the way below is my thought. 

```c
 struct ListNode * reverseList(struct ListNode * head)
 {
   struct ListNode * temp = NULL;
   struct ListNode * nextNode  = NULL; 
   
   while (head != NULL) {
       temp = head;
       head = head-> next;
       temp -> next = nextNode;
       nextNode = temp;
   }
   return temp;
 }
```

 I just wanted to think simply, So It is easy 
 
 but the following show you another way to reverse
 
```c
 struct ListNode* ReverseOfLinkedList(struct ListNode * head) {
   struct ListNode * temp = NULL;
   struct ListNode * nextNode = NULL;
   
   while(head != NULL) {
      nextNode = head->next;
      head -> next = temp;
      temp = head;
      head = nextNode;
   }
  
   return temp;
 }
```
 two ways is different a littl bit, but if you are thinking about tow way, almost similar.
