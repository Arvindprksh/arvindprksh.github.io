---
layout: post
title: Utilization Of LinkedList.
subtitle: Where is the middle of LinkedList ? and How do I have to do for printing in reverse order of LikedList
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

I refered to the book,"coding interview" and [geeksforgeeks](http://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/).

# where is the center of LinkedList ?

### First, brute-force

  1. get the total length of list, after that, get (the total length of list / 2)
  
  Let's make pseudo code 
  
  I think this is the simplest way I have ever experienced

```c
  struct ListNode * WhereIsMiddle ( struct ListNode * head ) {
            LinsNode * temp = head;
            int LenOfList = 0;
            int middlePosition = 0;
            
            // Just, firt get the length of list 
            while ( temp != NULL ) {
                LenOfList++;
                temp = temp -> next;
            }

            /// Second. the length of list / 2
            middlePosition = LenOfList / 2;
            
            temp = head;
            
            while ( middlePositio != 0 ) {
                temp = temp -> next;
            }
            
          return temp;
  
  }
```


### Another way 

  what about [geeksforgeeks](http://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/)
  
  I think just use how to check whether list is loop or not. 
  
  Use the two of point. Let's see pseudo code 
  
```c
    struct ListNode * WhereIsMiddle(struct ListNode * head) {
         struct ListNode * fastNode = head;
         srruct ListNode * slowNode = head;
         int count = 0  ; 
         
         while (slowNode != NULL) {
           
          count = 2;
          while ( count != 0 && fastNode != NULL){
                fastNode = fastNode -> next;
                count --; 
          }
          if ( fastNode == NULL)
             break;
             
             slowNode = slowNode -> next;
        }
        return slowNode;
    }
```
  
  The above is my way to find middle. 
  
  But the following is contents of the book "coding interview".
  
  While read this book. I feel really way to solve is differenct. Even though the algorithm is the same.
  
```c
  struct ListNode * FindMiddle (struct ListNode *head) {
    struct ListNode * moveX1 = NULL, * moveX2 = NULL;
    int i = 0;
    
    moveX1 = moveX2 = head;
    
    
    while (moveX2 != NULL) {
        if (i == 0) {
          moveX2 = moveX2 -> next;
          i = 1; 
        }
        else if (i == 1) {
          moveX2 = moveX2 -> next;
          moveX1 = moveX1 -> next;
          i = 0;
        }
    }
    return moveX1;
  }
```
 
# how to print the whole list from the end of the list. 

  I think the best way is stack.
  
  So if you are thinking about stack, You cand choose the type of stack, whether you ust system stack or not. 
  
  Or use stack you make.
  
  
### First, How to use stack. 

  let's pseudo code 
  
```c
  void PrintFromTheEndOfList (struct ListNode * head) {
    Stack A;
    struct ListNode * temp = head;
    
    // First. put the total ListNot in stack. 
    while (temp != NULL) {
        stack.push(temp);
        temp = temp -> next;
    }
    
    // Secode, print out from the top of Stack A.
    // If stack is empty, return NULL;
    // If Stack is not empty, return not NULL;
    while (stack.empty() != NULL ) {
      printf( stack.top);
      stack.pop();
    }
    
  }
```
  
  The Following shows you how to use recursive function with system stack. 
  
  In addition, the pseudo code is in contents of the book,"coding interview".
  
  i.e, recursive function !
  
  that function is useful, when you need to use dynamic programming. 
  
```c
  void PrintListFromEnd (struct ListNode * head) {
        
        if( head == NULL) 
            return ;
            
        PrintfListFromEnd ( head -> head );
        
        printf( head -> data );
  }
```
