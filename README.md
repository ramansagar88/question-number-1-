# Stack Implementation Using Array in C

Welcome! 👋

In this project, we will learn how to implement a **Stack using an Array in C**.

This project is designed for beginners, so let's understand the concept step by step.

---

## 📚 What is a Stack?

A Stack is a linear data structure that follows the:

**LIFO principle**

LIFO means:

> Last In, First Out

Think about a stack of plates.

If you put plates one above another, the plate you put last will be the first plate you remove.

Example:

```text
30  ← Top
20
10
```

If we perform `pop()`, `30` will be removed first.

---

## 🔑 Important Stack Operations

There are mainly two important operations:

### 1. Push

`push()` is used to **add an element** to the stack.

Example:

```text
Push 10

10
```

Then:

```text
Push 20

20  ← Top
10
```

Then:

```text
Push 30

30  ← Top
20
10
```

---

### 2. Pop

`pop()` is used to **remove the top element**.

Before pop:

```text
30  ← Top
20
10
```

After pop:

```text
20  ← Top
10
```

The element `30` is removed.

---

## 📌 What is `top`?

We use a variable called `top` to keep track of the top element.

Initially:

```c
int top = -1;
```

Why `-1`?

Because the stack is initially empty.

When we add the first element:

```text
top = 0
```

When we add the second element:

```text
top = 1
```

And so on.

---

## 🚨 Stack Overflow

Stack Overflow occurs when we try to add an element to a stack that is already full.

Our stack size is:

```c
#define MAX 5
```

So it can store a maximum of 5 elements.

We check:

```c
if (top == MAX - 1)
```

If this condition is true, the stack is full.

---

## 🚨 Stack Underflow

Stack Underflow occurs when we try to remove an element from an empty stack.

We check:

```c
if (top == -1)
```

If this condition is true, there is nothing to remove.

---

## 💻 Complete Program

The complete C program is available in:

`stack.c`

The program contains:

- `push()` function
- `pop()` function
- `display()` function
- Stack Overflow checking
- Stack Underflow checking

---

## ▶️ Example

If we execute:

```c
push(10);
push(20);
push(30);
```

The stack becomes:

```text
30 ← Top
20
10
```

After:

```c
pop();
```

The stack becomes:

```text
20 ← Top
10
```

---

## 🧠 How the Program Works

### Step 1 — Create an Array

```c
int stack[MAX];
```

This array stores the stack elements.

### Step 2 — Initialize `top`

```c
top = -1;
```

This means the stack is empty.

### Step 3 — Push an Element

When `push()` is called:

```c
top++;
stack[top] = value;
```

The top position increases and the new value is stored.

### Step 4 — Pop an Element

When `pop()` is called:

```c
top--;
```

The top position decreases, effectively removing the top element.

---

## ⏱️ Time Complexity

| Operation | Time Complexity |
|-----------|-----------------|
| Push      | O(1)            |
| Pop       | O(1)            |
| Display   | O(n)            |

---

## 🎯 What You Learn

After completing this project, you should understand:

- What a Stack is
- LIFO principle
- Push operation
- Pop operation
- Display operation
- Stack Overflow
- Stack Underflow
- `top` variable
- Array-based Stack implementation

---

## 👨‍💻 Author

Created as a beginner C programming learning project.
