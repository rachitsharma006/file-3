#include <stdio.h>
#include <stdlib.h>

#define MAX 5  // Maximum size of the queue

// Queue structure
struct Queue {
    int items[MAX];
    int front, rear;
};

// Function to initialize the queue
void initQueue(struct Queue* q) {
    q->front = -1;
    q->rear = -1;
}

// Function to check if the queue is full
int isFull(struct Queue* q) {
    return q->rear == MAX - 1;
}

// Function to check if the queue is empty
int isEmpty(struct Queue* q) {
    return q->front == -1;
}

// Function to enqueue an element
void enqueue(struct Queue* q, int value) {
    if (isFull(q)) {
        printf("Queue is full!\n");
        return;
    }
    if (q->front == -1) {  // If queue is empty
        q->front = 0;
    }
    q->rear++;
    q->items[q->rear] = value;
    printf("%d enqueued to queue\n", value);
}

// Function to dequeue an element
int dequeue(struct Queue* q) {
    if (isEmpty(q)) {
        printf("Queue is empty!\n");
        return -1;  // Indicating the queue is empty
    }
    int dequeuedValue = q->items[q->front];
    q->front++;
    if (q->front > q->rear) {  // Reset the queue if it's empty
        q->front = q->rear = -1;
    }
    return dequeuedValue;
}

// Function to display the front of the queue
int front(struct Queue* q) {
    if (isEmpty(q)) {
        printf("Queue is empty!\n");
        return -1;
    }
    return q->items[q->front];
}

int main() {
    struct Queue q;
    initQueue(&q);
    
    enqueue(&q, 10);
    enqueue(&q, 20);
    enqueue(&q, 30);
    
    printf("Dequeued element: %d\n", dequeue(&q));
    printf("Front element is: %d\n", front(&q));

    return 0;
}
