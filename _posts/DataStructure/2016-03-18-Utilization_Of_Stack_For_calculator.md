---
layout: post
title: Calculator with Stack
subtitle: How can I make caculator with stack ?
category: Data Structure
tags: [stack]
permalink: /2016/03/18/Utilization_Of_Stack_For_calculator/
---

this refers to 윤성우의 열혈 잘료구조

then, calculate the following

(3 + 4) * (5 / 2) + (7 + (9 - 5))

to calculate the above,

  - you first calculate the round brackets. ( 소괄호 부터 계산)
  - you calculate operator along with operator's priority. (연산자 우선 순위에 맞추어 계산)
 
 
three expression of number 

  - infix notation(중위 표기법)    -----> 5 + 2 / 7
  - prefix notation(전위 표기법)   -----> + 5 / 2 7  : calculate from the back
  - postfix notation(후위 표기법)  -----> 5 2 7 / +  : calculate using stack
  
  postfix is more easy than infix to calculate.(프로그래밍으로 계산을 하는 것은 후위 표기법이 중위 표기법보다 쉽다.)
  
  the following is to present method transforming from infix to postfix.

  ![](/img/Image/DataStructure/2016-03-18-Utilization_Of_Stack_For_calculator/calculation1.png)
  
  
  ![](/img/Image/DataStructure/2016-03-18-Utilization_Of_Stack_For_calculator/calculation2.png)
  
  
  ![](/img/Image/DataStructure/2016-03-18-Utilization_Of_Stack_For_calculator/calculation3.png)
  
  
  ![](/img/Image/DataStructure/2016-03-18-Utilization_Of_Stack_For_calculator/calculation4.png)
  
  
  ![](/img/Image/DataStructure/2016-03-18-Utilization_Of_Stack_For_calculator/calculation5.png)
  
  this considers the round brackets. when you transform from infix to postfix.
  
  ![](/img/Image/DataStructure/2016-03-18-Utilization_Of_Stack_For_calculator/calculation6.png)
  
  
  ![](/img/Image/DataStructure/2016-03-18-Utilization_Of_Stack_For_calculator/calculation7.png)
  
  
  ![](/img/Image/DataStructure/2016-03-18-Utilization_Of_Stack_For_calculator/calculation8.png)
  

  after the above, you calculate posfix. the method is the following.
  
  ![](/img/Image/DataStructure/2016-03-18-Utilization_Of_Stack_For_calculator/calculation9.png)
  
  
  ![](/img/Image/DataStructure/2016-03-18-Utilization_Of_Stack_For_calculator/calculation10.png)
  
  
  code is the following.
  
```c
int calculation(char exp[])
{
    Stack stac;
    int expLen = strlen(exp);
    char tok, op1, op2;
    
    StackInit(&stack);
    
    for(int i = 0 ; i < expLen ; i++)
    {
        tok = exp[i];
        
        if(isdigit(tok))
            SPush(&stack, tok - '0');
        else
        {
            op2 = SPop(&stack);
            op1 = SPop(&stack);
            
            switch(tok)
            {
                case '+';
                  SPush(&stack, op1+op2);
                  break;
                case '-';
                  SPush(&stack, op1-op2);
                  break;
                case '*';
                  SPush(&stack, op1*op2);
                  break;
                case '/';
                  SPush(&stack, op1/op2);
                  break;
            }
        }
    }
    
    return SPop(&stack);
}
```
