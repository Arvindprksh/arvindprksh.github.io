---
layout: post
title: Utilization Of LinkedList 9
subtitle: How Can I check if the singly LinkedList is plindorme ?
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

I refer to coding interview book and [geeksforgeeks](http://www.geeksforgeeks.org/function-to-check-if-a-singly-linked-list-is-palindrome/)

# Problem 

If you are given a singly Linked List of character. if the given list is palindrome, You have to return TRUE.

![palindrome](/img/Image/CodingInterview-ExtensionOfDataStructure/2016-08-03-Utilization_Of_LinkedList9/palindrome.png)

## algorithm

  1) let's us use the stack 
    - First put list in a stack. 
    - Second, You have to compare top of the stack with node of List.
    
  let's us make pseudo code
  
```c
  bool WhetherToBePalindrome(struct ListNode * head) {
      structure ListNode * temp = head;
      Stack sample;
      
      if (temp == NULL)
        return false;
      
      while (temp != NULL) {
        
        sample.push(temp->data);
      
        temp -> next;
      }
      
      // after the above
      // here you have to compare stack with list
      
      while( head != NULL ){
        
         if ( head -> data == stack.top ) {
                  head = head -> next;
                  stack.pop();
         }
         else {
              printf("here found this list is not palindrome");
              retrun false;
         }
      }
      return true;
  }
```
  
  this algorithm is same from the geeksforgeeks. And GeeksforGeeks introduce the another alorithm.
  
### Second, Algorithm of GeeksForGeeks.

  this algorithm is similar to coding interview book. 
  
  the following is algorithm 
  
  1) Get the middle of linked list.   
  2) Reserve the Second half of the linked list  
  3) Check if the first half and second half is identical.   
  4) Construct the original linked List by reversing the secondf half again and attaching it back to the first half.   
  
  let's make pseudo code

```c
  struct node {
    char data;
    struct node* next;
  };
  
  void reverse(struct node **);
  bool compaeLists(struct node *, node *);
  
  bool isPalindrome(struct node *head){
      struct node * fastNode = head, *slowNode = head;
      struct node * prev_of_slow_ptr = head;
      struct node * second_half;
      struct node * midNode = NULL;
      bool rc=true;
      
      
      if ( head == NULL )
          return false;
      
      while(fastNode != NULL && fastNode -> next != NULL) {
            fastNode = fastNode -> next -> next;
            prev_of_slow_ptr = slowNode;
            slowNode = slowNode -> next;
      }
      
      // if the list is odd, just move one
      if ( fastNode != NULL ) {
          midnode = slowNode;
          slowNode = slowNode -> next;
      }
      second_half = slow; 
      prev_of_slow_ptr -> next = NULL;
      reverse(&second_half);
      rc=compareLists(head, second_half);
      
      reverse(&second_half);
      
      if (midNode != NULL) {
          prev_of_slow_ptr -> next = midnode;
          midnode-> next = second_half;
      }
      else 
        prev_of_slow_ptr -> next = second_half;
        
        return rc;
      
  }
```
