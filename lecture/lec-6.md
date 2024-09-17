---
description: Thanks for today's lecturer Eldon Chung!
---

# Lec 6

## Unit 13 Call Stack

### Stack Frame

We can think of the **frame** as a portion of **stack**. The latter is a portion of the memory in our computer.

## Unit 14 Fixed-Length Array

### Pointer

```c
long *a;
```

Using this  way to declare a pointer, its type `long` means that this pointer (variable) stores **the address of a variable of type `long`.**&#x20;

### **Array Name Decay**

```c
long a[2] = {0, 1};
long *array_ptr = a;
```

**Array Name Dacay** means that after you define an array, and then you want to use the array nam, the array name will decay into just a **memory address, not a pointer variable!!!**
