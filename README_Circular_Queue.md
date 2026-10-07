# Circular Queue Implementation Using Array in C

Welcome! 👋

In this project, we will learn how to implement a **Circular Queue using an Array in C**.

This project is designed for beginners, so let's understand the concept step by step.

---

## 📚 What is a Queue?

A Queue is a linear data structure that follows the:

**FIFO principle**

FIFO means:

> First In, First Out

Think about people standing in a line.

The person who enters the line first will be served first.

Example:

```text
Front                         Rear
  ↓                             ↓
[10] → [20] → [30] → [40]
```

If we perform `dequeue()`, `10` will be removed first.

---

## 🔄 What is a Circular Queue?

A normal queue can waste empty spaces after elements are removed.

A **Circular Queue** solves this problem by connecting the last position of the array back to the first position.

Think of the array as a circle:

```text
[0] → [1] → [2] → [3] → [4]
 ↑                         ↓
 └─────────────────────────┘
```

When `rear` reaches the last position, it can move back to index `0` if there is an empty space.

This is done using **modulo arithmetic**.

```c
(rear + 1) % MAX
```

and

```c
(front + 1) % MAX
```

---

## 🔑 Important Operations

A Circular Queue mainly uses two operations:

### 1. Enqueue

`enqueue()` is used to **add an element** to the rear of the queue.

Example:

```text
Enqueue 10

[10]
```

Then:

```text
Enqueue 20

[10] → [20]
```

Then:

```text
Enqueue 30

[10] → [20] → [30]
```

---

### 2. Dequeue

`dequeue()` is used to **remove an element** from the front.

Before dequeue:

```text
Front              Rear
  ↓                  ↓
[10] → [20] → [30]
```

After dequeue:

```text
        Front       Rear
          ↓           ↓
[empty] → [20] → [30]
```

The element `10` is removed.

---

## 📌 What are `front` and `rear`?

We use two variables to keep track of the queue.

### `front`

`front` points to the element that will be removed next.

### `rear`

`rear` points to the position where the next element will be inserted.

Initially:

```c
int front = -1;
int rear = -1;
```

This means the queue is empty.

---

## 🔁 Why do we use `%`?

The modulo operator `%` allows the indexes to wrap around.

Suppose:

```c
MAX = 5
rear = 4
```

Then:

```c
(rear + 1) % MAX
```

becomes:

```text
(4 + 1) % 5
= 5 % 5
= 0
```

So `rear` moves back to index `0`.

This is the main idea behind a Circular Queue.

---

## 🚨 Circular Queue Overflow

Overflow occurs when the queue is completely full.

The condition is:

```c
(rear + 1) % MAX == front
```

If this condition is true, there is no empty position available.

---

## 🚨 Circular Queue Underflow

Underflow occurs when we try to remove an element from an empty queue.

We check:

```c
front == -1
```

If this condition is true, the queue is empty.

---

## 💻 Complete Program

Create a file named:

`circular_queue.c`

Use the following program:

```c
#include <stdio.h>

#define MAX 5

int queue[MAX];
int front = -1;
int rear = -1;

// Function to add an element
void enqueue(int value)
{
    // Check if queue is full
    if ((rear + 1) % MAX == front)
    {
        printf("Circular Queue Overflow!\n");
        return;
    }

    // If queue is empty
    if (front == -1)
    {
        front = 0;
        rear = 0;
    }
    else
    {
        rear = (rear + 1) % MAX;
    }

    queue[rear] = value;

    printf("%d inserted into the queue.\n", value);
}

// Function to remove an element
void dequeue()
{
    // Check if queue is empty
    if (front == -1)
    {
        printf("Circular Queue Underflow!\n");
        return;
    }

    printf("%d removed from the queue.\n", queue[front]);

    // If there is only one element
    if (front == rear)
    {
        front = -1;
        rear = -1;
    }
    else
    {
        front = (front + 1) % MAX;
    }
}

// Function to display the queue
void display()
{
    if (front == -1)
    {
        printf("Circular Queue is empty.\n");
        return;
    }

    printf("\nCircular Queue elements:\n");

    int i = front;

    while (1)
    {
        printf("%d ", queue[i]);

        if (i == rear)
        {
            break;
        }

        i = (i + 1) % MAX;
    }

    printf("\n");
}

int main()
{
    // Insert elements
    enqueue(10);
    enqueue(20);
    enqueue(30);
    enqueue(40);

    display();

    // Remove two elements
    dequeue();
    dequeue();

    display();

    // Add elements again
    enqueue(50);
    enqueue(60);

    display();

    return 0;
}
```

---

## ▶️ Example Execution

First, we insert:

```c
enqueue(10);
enqueue(20);
enqueue(30);
enqueue(40);
```

The queue becomes:

```text
Front                    Rear
  ↓                        ↓
[10] [20] [30] [40] [ ]
```

Now we remove two elements:

```c
dequeue();
dequeue();
```

The queue logically becomes:

```text
[ ] [ ] [30] [40] [ ]
          ↑       ↑
        Front    Rear
```

Now we insert:

```c
enqueue(50);
enqueue(60);
```

The circular queue can reuse the empty positions at the beginning:

```text
[60] [ ] [30] [40] [50]
 ↑                    ↑
Rear                 Front
```

The important point is that the array positions can be reused because the queue is circular.

---

## 🧠 How the Program Works

### Step 1 — Create the Array

```c
int queue[MAX];
```

This array stores the queue elements.

### Step 2 — Initialize `front` and `rear`

```c
int front = -1;
int rear = -1;
```

Both are `-1` because the queue is initially empty.

### Step 3 — Enqueue

When the first element is inserted:

```c
front = 0;
rear = 0;
```

For the next elements:

```c
rear = (rear + 1) % MAX;
```

This allows `rear` to wrap around to the beginning.

### Step 4 — Dequeue

After removing an element:

```c
front = (front + 1) % MAX;
```

This moves `front` to the next element and also allows it to wrap around.

### Step 5 — Queue Becomes Empty

If:

```c
front == rear
```

before removing the element, there was only one element.

So we reset:

```c
front = -1;
rear = -1;
```

---

## 🔄 Circular Movement Example

Suppose:

```text
MAX = 5
```

The indexes are:

```text
0 → 1 → 2 → 3 → 4
↑               ↓
└───────────────┘
```

If `rear = 4`:

```c
rear = (rear + 1) % MAX;
```

Then:

```text
rear = (4 + 1) % 5
rear = 0
```

So the rear moves from index `4` back to index `0`.

---

## ⏱️ Time Complexity

| Operation | Time Complexity |
|-----------|-----------------|
| Enqueue   | O(1)            |
| Dequeue   | O(1)            |
| Display   | O(n)            |

---

## 🎯 What You Learn

After completing this project, you should understand:

- What a Queue is
- FIFO principle
- Circular Queue
- Enqueue operation
- Dequeue operation
- Front pointer
- Rear pointer
- Circular movement
- Modulo operator `%`
- Queue Overflow
- Queue Underflow
- Array-based Circular Queue implementation

---

## 👨‍💻 Author

Created as a beginner C programming learning project.
