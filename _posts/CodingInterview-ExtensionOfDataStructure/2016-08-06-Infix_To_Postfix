---
layout: post
title: Infix To Pofix
subtitle: How to switch Infix to postfix
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

I refer to coding interview book and [geeksforgeeks](http://quiz.geeksforgeeks.org/stack-set-2-infix-to-postfix/)

Infix expression : The expression of the form a op b. When an operator is in-between every pair of operands.

Postfix expression : Then expression of the form a b op. When an operator is followed for every pair of operands.

The compiler scans the expression either from left to right or from right to left.

Consider the below expression 

  : a op1 b op2 c op3 d
  
If op1 = +, op2=*, op3= +

The compiler first scans the expression to evaluate the expression b * c, then again scan the expression to add a to it. 

The result is then added to d after another scan. 

The repeated scanning makes it very in-efficient. it is btter to convert the expression to postfix(or prefix) form before 

evaluation. 

The corresponding expression of postfix form is abc*d++. The postfix expressions can be evaluated easily using a stack. 


# use of Stack for solution. 

## algorithm of [geeksforgeeks](http://quiz.geeksforgeeks.org/stack-set-2-infix-to-postfix/)

 1) Scan the infix expression from left to right.
 
 2) if the scanned character is an operand, output it. 
 
 3) Else, 
      
      3-1) if the precedence of the scanned operator is greater than precdence of the operator in the stack(or the stack is empty), push it. 
      
      3-2) else, Pop the operator from the stack until the precedence of the scanned operator is less-equal to the precedence of the operator residing  on the top of stack. Push the scanned operator to the stack. 
      
  4 ) If the scanned character is an '(', Push it to the stack. 
  
  5 ) If the Scanned character is an ')', pop and output frome the stack until meeting '('.
  
  6 ) Repeat steps 2 - 6 until infix expression is scanned.
  
  7 ) Pop and ouput from the stack until it is empty.
  
  let's see the code comprised of the above algorithm.
  
```c
  // Stack type
  struct Stack {
      int top; 
      unsigned int capacity;
      int * arrary;
  };
  
  // Stack operations
  struct Stack * createStack ( unsigned capacity ) {
          
        Stack* stack = (struct stack *)malloc(sizeof(struct Stack));
        
        if ( !stack)
              return NULL;
              
        stack -> top = -1; 
        stack -> capacity = capacity;
        
        stack -> array = (int *) malloc (stack->capacity * sizeof(int));
        
        if ( !stack -> array)
            return NULL;
            
        return stack;
  }
  
  int isEmpty(struct Stack *stack) {
          return stack -> top == -1; 
  }
  
  char peek (struct Stack *stack) {
  
      return stack -> array[stack -> top];
  }
  
  char pop(struct Stack * stack) {
      
      if (!isEmpty(stack))
        return stack -> array[(stack -> top)--];
      else 
          return '$';
  }
  
  char push(struct Stack * stack, char op) {
  
       // in geeksforgeeks, hers is no checcking whether stack is full. 
       
       stack -> array[++stack->top] = op;
  }
  
  // A utility function to check if the given character is operand. 
  int isOperand (char ch) {
  
      return (ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z');
  }
  
  // A utility function to return precdence of a given operator
  // Higher returned value means higher percedence
  int Prec(char ch) {
        
     switch (ch) {
      case '+' : 
      case '-' :
          return 1;
      case '*' :
      case '/' :
          return 2;
      case '^' : 
          return 3;
     }
    return -1;
  }
  
  int infixToPostfix(char * exp) {
      int i, k;
      
      // Create a stack of capacity equal to expression size
      Struct Stack* stack = createStack(strlen(exp));
      
      if (!stack)
          return -1;
        
      for ( i = 0, k = -1 ; exp[i]; i++) {
          
          // If the scanned charater is an operand, add it to output
          if ( isOperand(exp[i]))
              exp[++k]= exp[i];
              
          // If the scanned character is an '(', push it to stack. 
          else if (exp[i] == '(')
              push(stack, exp[i]);
              
          // If the scanned character is an ')', pop and output from the stack.
          // until an '(' is encountered. 
          else if (exp[i] ==')') {
              while (!isEmpty(stack) && peek(stack) != '(')
                  exp[++k] = pop(stack);
              if (!isEmpty(stack) && peek(stack) != '(' )
                        return -1; // invalid expression
                        
              else 
                  pop(stack);
          }
          
          // An operator is encountered 
          else {
              while ( !isEmpty(stack) && Prec(exp[i]) <= Prec(Peek(stack)))
                    exp[++k] = pop(stack);
                    
              push(stack, exp[i]);
          }
      }
      
      // after for statement, you have to pop all operator from stack.
      while (!isEmpty(stack))
          exp[++k] = pop(stack);
        
      exp[++k]= '\0';
      printf("%s\n", exp);
  }
  
```
  
  
  
## Algorithm of coding interviewing book.

  this book's algrotim also is the same from geeksforgeeks.
  
  the following is algorrithm of the coding interviewing book. 
  
  1 ) make the stack. 
  
  2 )
  
```c
  for ( get input from the string of infix ) {
      if ( whether t is operands or not)
            if t is operand, output it. 
            
      else if ( t == ')' )
            pop until meeting '(' and you have to print the popped stuff. but don't have to print ')'.
            
      else { // t == operator and '('
          pop operator from stack Until t is less and equal to the top of stack and stack is empty. 
          push t to stack.
      }
  }
  
  after the above process, you have to check the stack is empty.
```
  


## how to get minimum using stack. 

  if you want to know more information, just I recommend you this site, [geeksforgeeks](http://www.geeksforgeeks.org/design-and-implement-special-stack-data-structure/)

  you have to prepare for two stacks. one is just a usual stack. the other you will use is just for minimum. 
  
  if the stack for minimum is special stack. when you call getminimum function, time complexity should be O(1).
  
  sol > 
  
  Use two stacks : one to store actual stack elements and other as an auxiliary stack to store minimum values. The idea is to do push() and pop() operations in such a way that the top of auxiliary stack is always the minimum. 
  
### algorithm 

   1 ) one is to do push() and pop() continuously 
   
   2 ) the other one compares with item that will is push to another stack before updating stack, for example, pushing(now, there are only two stacks). 
   
   per functions for your information. I just explain to you each function. 
   
   push (int x ) // inserts an element x to special Stack. 
   
   1 ) push x to the first stack ( the stack with actual elements )
   
   2 ) compare x with the top element of the second stack( the auxiliary stack). Let the top element be y. 
   
        a ) If x is smaller than y then push x to the auxiliary stack. 
        
        b ) If x is greater than y then push y to the auxiliary stack. 
        
  int pop() // removes an element from Special Stack and return the removed element
  
    1 ) pop the top element from the auxiliary stack. 
    
    2 ) pop the top element from the actual stack and return it. 
    
  int getMin() returns the minimum element from special stack. 
  
  1 ) Return the top element of auxiliary stack. 


### Let's think of more space to save.

  The stack managing the minimum is not neccessary, i.e. it waste the space of stack. 
  
  So let's change the algorithm of stack. 
  
  when you push node to two stacks. 
  
  Especailly, you need to reduce a little times of push in minStack(Special stack invovled the getMin function).
  
  condition of pushing node to minStack.
  
  the original top is greater or the same than new node. then , you have to push the new node as well.  
  
  And when you remove the node from minStack. 
  
  peek of the other Stack is compared with peek of minStack. 
  
  when both of them is the same, minStack can also pop.
