---
layout: post
title: Extension of Douubly Linked List 
subtitle: How can I make doubly LinkedList efficiently ?
category: Extenstion Of DataStructure
tags: [list]
permalink: /2016/07/07/Extension_Of_Double_Linked_List/
---

- Before  you start the this course, I recommend [geeksforgeeks site](http://www.geeksforgeeks.org/union-and-intersection-of-two-linked-lists/)

 - I refered to [geeksforgeeks site](http://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/) ande coding interview

## conventional definition of doubly Linked - XOR Linked List (메모리 효율적인 양방향 링크드 리스트)

### base structure (기본 구조)

![](/img/Image/CodingInterview-ExtensionOfDataStructure/2016-07-07-Extension_Of_Double_Linked_List/double_linked_list.png)

```c
  typedef struct node {
      int data;
      struct node * before;
      struct node * next;
  } Node;
```
  but If you use XOR operation, You utilize one variable for direction. the structure is the following 
  
```c
  typedef struct node {
      int data;
      struct node * ptrDifference;
    } Node
```
 
let me think about it in detail.

in the case of ordinary double Linked List, let's say 

characteristic of XOR operation

X XOR X = 0

X XOR 0 = X

X XOR Y = Y XOR X

(X XOR Y) XOR Z = X XOR ( Y XOR Z) 

the following is the brief representation of double Linked List 

Node A :
  - prev = NULL, next = address of Node B 
  
Node B : 
  - prev = address of Node A, next = address of Node C 

Node C :
  - prev = address of Node B, next = address of Node D
  
Node D :
 - prev = address of Node C, next = NULL
 
I will transform the above double linked list into XOR double linked List 

asterisk(*) : XOR List's address variable is npx that in XOR between pre and next variable (i.e pre XOR next). 


Node A:
  - npx = NULL XOR address of B // bitwise XOR zero and address of B
  
Node B:
  - npx = address of A XOR address of C // bitwise XOR address of A and address of C
  
Node C:
  - npx = address of B XOR address of D // bitwise XOR address of B and address of D
  
Node D :
  - npx = address of C XOR NULL // bitwise XOR address of c and NULL

##### Traversal of XOR List

you can traverse the XOR list in both forward and reverse direction. while traversing the double Linked list that memory is efficient

you have to remember the previously accessed node's address in order to calculate the next node's address. 

let me try with the above npx 

for head ---> Node A, 

Node B 
  (NULL XOR Node A)
  
Node C
  (NULL XOR npx of Node A) XOR npx of Node B
  
Node D 
 ((NULL XOR npx of Node A) XOR npx of Node B) XOR npx of Node C
