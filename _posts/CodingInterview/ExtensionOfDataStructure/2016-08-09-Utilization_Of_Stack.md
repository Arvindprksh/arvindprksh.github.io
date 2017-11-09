---
layout: post
title: How to reverse a stack, only using stack operations
subtitle: How can I reverse a stack, If you sould only use stack operations ?
category: Extenstion Of DataStructure
tags: [stack]
permalink: /2016/08/09/Utilization_Of_Stack/
---

you can see a solution of this problem in [geeksforgeeks](http://www.geeksforgeeks.org/reverse-a-stack-using-recursion/) and get hint.

### GeeksforGeeks' solution. 

  I quoted the following contents from [geeksforgeeks site](http://www.geeksforgeeks.org/reverse-a-stack-using-recursion/)

  sol > Reverse a stack using recursion. 
  
  You are not allowed to use loop statement like while, for.. etc. and you cna only use the following ADT functions on Stack s:
  
``` 
  IsEmpty(s)
  Push(s)
  Pop(s) 
```
  
  solution : 
  
  my thought 
  
  > above all, You remove the top of stack, and then again you push items removed from stack to stack. 

   Finally, the stack is reverse direction.
              
  let me see, next time we see the solution of the geeksForgeeks. 
  
  geeksforgeeks sol 
  
  > The idea of the solution is to hold all values in Function Call stack(systemp stack). until the stack becomes empty. 
  
  When the stack becomes empty. insert all held items one by one at the bottom of the stack. 
                      
  For example, let the input stack be :
  
``` 
  1 <-- top
  2
  3
  4
```

```
  First 4 is inserted at the bottom. 
   4 <-- top
  Then 3 is inserted at the bottom. 
   4 <-- top
   3
  Then 2 is inserted at the bottom.
   4 <-- top
   3
   2
  Then 1 is inserted at the bottom. 
   4 <-- top
   3
   2
   1
```
  
  So we need a function that inserts at the bottom of a stack using the above given basic stack function. 
  
  void InsertAtBottom() : First pops all stack items and stores the popped item in function call stack using recursion. 
  
  And when stack becomes empty, pushes new item and all items stored in call stack. 
  
  void reverse() : This function mainly uses insertAtBottom() to pop all items one by one and insert the popped items at the bottom. 
  
  let's see the code of geeksforgeeks. 
  
  as you can see, just here uses the linked list 

```c
  struct sNode {
      char data;
      struct sNode *next;
  };
  
  // Below is a recursive funtion that inserts an element 
  // at the Bottom of a stack. 
  void insertAtBottom(struct SNode ** top_ref, int item) {
      if (isEmpty(*top_ref))
          push(top_ref, item);         
      else {
            // Hold all items in Function call Stack until we reach end of the stack. When the stack becomes empty. 
            //the IsEmpty (*top_ref) becomes true, the above if part is executed and the item is inserted at the bottom. 
            int temp = pop(top_ref);
            insertAtBottom(top_ref, item);
            // Once the item is inserted at the bottom, push all the items held in Function Call stack
            push (top_ref, temp);
      }
  }
  // Below is the function that reverses the given stack using 
  // insertAtBottom()
  void reverse(struct sNode* top_ref) {
        if (!IsEmpty(*top_ref)){        
            // Hold all items in Function Call Stack until we reach end of the stack. 
            int temp = pop(top_ref);
            reverse(top_ref); 
            // Insert all the items (held in Function Call Stack) one by one from the bottom to top. Every item is inserted at the bottom
            insertAtBottom(top_ref, temp);
        }
  }
```  
  
  But I think using the array is much better. 
  
  We will see another way in coding interviewing book
  
  BUT totally, it's different. 
  
  just in coding interview book, it is important to search reversely.
  
  Now, let's see algorithm of coding interview book.
  
  First, pop a stack until the stac is empty. 
  
  Second, insert the popped items from stack, using function call stack 
  
  let's make pseudo code
  
```c
  void ReverseStack (struct Stack *s) {
      int data;
      if (IsEmptyStack(s) )
          return;
          
      data = pop(s);
      ReverseStack(s);
      InsertAtBottom(s, data);
  }
  
  void InsertAtBottom(Struct Stack *s, int data) {
      int temp;
      
      if(IsEmptyStack(s))
        push(s, data);
        return;
        
      temp = pop(s);
      InsertAtBottom(s, data);
      Push(s, data);
  }
```
  
  let's think of two satck in a array. 
  
  If you want to know more, I will let you know this site, [geeksForgeeks](http://www.geeksforgeeks.org/implement-two-stacks-in-an-array/).
