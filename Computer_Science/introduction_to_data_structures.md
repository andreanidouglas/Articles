---
title: Introduction to Data Structures (Queues)
published: false
description: Data structures are a foundamental piece in computer science and programming
tags: computer science, begginer, data structures
---

# Introduction to data structures (Queues)

One of the most overlooked concepts within computer science is data structures. Have a good understand of it's concepts, design and application can transform you from a simple coder to a more capable and resourceful professional.

One can brief summarize a generic data structure as a mean to store data in memory as an organized fashion. And for that, there are several types of structures, each one with it's specific use case and scenario.

## Queues

![Queue of people!](http://www.dailyexcelsior.com/wp-content/uploads/2014/05/page1-19.jpg)

Imagine you are excited to ride in this new attraction at the park. You arrive, there is a hundred people waiting in line for the same ride.

Queues can be very useful when you want to process data in the order. **First in, First out** or (FIFO). Every data element must be inserted at the end and removed from the top.

```c
struct element {
    int data;
    struct element *next;
};

typedef struct {
    struct element *start;
    struct element *end;
}queue;


queue* q;


void newqueue(queue* q){
    q->start = NULL;
    q->end = NULL;
}

/// Add element to the queue. O(1)
void enqueue(struct element* e){
    
    if(q->start == NULL){
        q->start = e;
        q->end = e;
    } else {
        struct element* aux;
        q->end->next = e;
        q->end = e;
        e->next = NULL;
    }
}

/// Remove element from the queue O(1)
void dequeue(struct element* e){
    e = q->start;
    q->start = e->next;
}

/// Get size of the queue. O(n)
int size(){
    int s = 0;
    struct element* curr;
    curr=q->start;
    while(curr->next != NULL){
        curr = curr->next;
        s++;
    }
    return ++s;
}

/// Peek at the nth element of the queue. O(n)
void peek(int n, struct element* e){
    int s = 0;
    struct element* curr;
    curr=q->start;
    e = NULL;
    while(curr->next != NULL){
        if (n==s) e = curr;

        curr = curr->next;
        s++;
    }
}

```

The form presented above, is the most standard implementation. You can implement queues only shifting elements on an dinamic array, but this would cause the queue/enqueue operations to drop their efficiency to O(n).

## Examples where queues can be useful

Now that you understand a queue and it's implemenation. Let's discuss where to implement them.

The most common case for a queue implementation is inside the producer/consumer scenario. The producer will generate data to be consumed and it can be faster than the consumer. For that reason, a queue at the consumer will organize the data income allowing it to be consume in order of oldest to newest data.