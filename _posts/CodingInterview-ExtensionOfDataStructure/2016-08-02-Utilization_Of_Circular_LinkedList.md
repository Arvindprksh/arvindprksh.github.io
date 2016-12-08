---
layout: post
title: Utilization Of Circular LinkedList
subtitle: How to Split a Circular Linked List into two halves. 
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

# problem 

 - you have to split the circular Linked List with the same size of Divisions. 
 - Maybe if circular Linked List is odd, you have to change the number of node, it is even .
 - if I explain to you with drawings. Just refer to the following pictures.(The following pictures is refered to [geeksforgeeks](http://www.geeksforgeeks.org/split-a-circular-linked-list-into-two-halves/)
 
 ![](/img/Image/CodingInterview-ExtensionOfDataStructure/2016-08-02-Utilization_Of_Circular_LinkedList/Split_a_Circular_Linked_List_into_two_halves.png) 

### Algorithm

 1. First count the number of node in Circular Linked List // way to split the list is floyd algorithm, it is much better. 
 2. Second, I have to make the List even. 
 3. Third, I make the List half. the front is the same size like the rear. Finally, I have to make two circular Linked List.

```c
 struct node 
 {
   int data;
   struct node *next;
 };
 
 void SplitList (struct node * head, struct node **head1_ref, struct node **head2_ref) {
      struct node * fastNode = head;
      struct node * slowNode = head;
      
      if (head == NULL)
       return;
      
      while (fastNode -> next != head && fastNode -> next -> next != head) {
          fastNode = fastNode -> next -> next;
          slowNode = slowNode -> next;
      }
      
      if (fastNode -> next -> next == head)
           fastNode = fastNode -> next;
        
      *head1_ref = head;
      
      // be careful about this. 
      if (head -> next != head)
       *head2_ref = slowNode -> next;
      
      fastNode -> next = slowNode -> next;
    
      slowNode -> next = head;
 }
```
