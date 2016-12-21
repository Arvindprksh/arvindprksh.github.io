---
layout: post
title: Queue with LinkedList
subtitle: How can I make queue with LinkedList
category: Data Structure
tags: [queue, list]
permalink: /2016/03/22/Queue_Based_On_LinkedList/
---

이것은 윤성우의 열혈 자료구조를 참고했습니다. 
this refers to 윤성우의 열혈 자료구조.

1-1-1. queue based on LinkedList.

    - there is difference between stack and queue. it is how to remove a data.
    - when you make queue, use the stack. but removing a data is different from the original stack.
    - 배열기반 보다  연결 리스 트 기반이 더욱 쉽다. 
    - 스택과 큐의 차이점은 단지 데이터를 어떻게 제거하는 지가 다르다. 즉, 이전 스택에서 데이터를 제거하는 
    방식을 바꾸면 될거 같다. -> 연결 리스트 기반인 경우에만 
  
![](/img/Image/DataStructure/2016-03-22-Queue_Based_On_LinkedList/QueueLinkedList1.png)

1-1-2. intialization of queue based on LinkedList.

```c
void QueueInit(Queue * pq)
{
    pq -> front = NULL;
    pq -> rear = NULL;
}

int QIsEmpty(Queue * pq)
{
  if(pq -> front == NULL)
    return TRUE;
  else 
    return FALSE; 
}
```

![](/img/Image/DataStructure/2016-03-22-Queue_Based_On_LinkedList/QueueLinkedList2.png) 


```c
void Enqueue (Queue * pq, Data data)
{
    Node * newNode  = (Node * ) malloc(sizeof(Node));
    newNode -> next = NULL;
    newNode -> data = data;
    
    if(QIsEmpty(pa))
    {
        pq -> front = newNode;
        pq -> rear = newNode;
    }
    else
    { 
        pq -> rear -> next = newNode;
        pq -> rear = newNode;
    }
}
```


![](/img/Image/DataStructure/2016-03-22-Queue_Based_On_LinkedList/QueueLinkedList3.png) 


```c
void Dequeue (Queue * pq, Data data)
{
    Node * delNode;
    Data retData;
    
    if(QIsEmpty(pa))
    {
        printf("Queue is empty\n");
        exit(-1);
    }
    
    delNode = pq -> front;
    retData = delNode -> data;
    pq -> front = pq -> front -> next;
    
    frer (delNode);
    return retData;
    
}
```

![](/img/Image/DataStructure/2016-03-22-Queue_Based_On_LinkedList/QueueLinkedList4.png) 

![](/img/Image/DataStructure/2016-03-22-Queue_Based_On_LinkedList/QueueLinkedLis5.png)

```c
// example of main function

int main(void)
{
  // initialization queue
  Queue q;
  QueueInit(&q);
  
  // put data in the queue
  Enqueue(&q, 1);
  Enqueue(&q, 2);
  Enqueue(&q, 3);
  Enqueue(&q, 4);
  Enqueue(&q, 5);
  
  // remove data from queue
  
  while (!QIsEmpty(&q))
  {
      printf("%d ", Dequeue(&q));
  }
  return 0;
}


// the result of main function

->  1 2 3 4 5
```

