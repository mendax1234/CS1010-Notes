---
description: Thanks for today's lecturer Eldon Chung!
---

# Lec 06 - Call Stacks, Arrays

## Unit 13 Call Stack

### Stack Frame

We can think of the **frame** as a portion of **stack**. The latter is a portion of the memory in our computer. The memory allocated to each function call is called a _stack frame_. When a function returns, the stack frame is deallocated and freed up for other uses.

Now, we introduce how to draw the stack fram using the following example

{% code lineNumbers="true" %}
```c
long add(long a, long b) {
  long sum;
  sum = a + b;
  return sum;
}

int main()
{
  long x = 1;
  long y;
  y = add(x, 10);
}
```
{% endcode %}

Below is the stack frame diagram when the stack frame for `add()` is created.&#x20;

<figure><img src="../../../.gitbook/assets/stack-frame.png" alt=""><figcaption><p>Stack Frame</p></figcaption></figure>

{% hint style="info" %}
This kind of diagram will be useful in future analysis about recursion and pointer. It may also come out in the exam paper.
{% endhint %}

## Unit 14 Fixed-Length Array

### Array Declaration

{% code lineNumbers="true" %}
```c
long list[10];
```
{% endcode %}

We use the square bracket `[` and `]` to indicate that the variable `list` is an array. The number `10` indicates that `marks` holds 10 `long` values. The size of the array must be an integer value, not a variable.

{% hint style="info" %}
Remeber this because it will help you in later units which may contain its variants.
{% endhint %}

### Pointer

```c
long *a;
```

Using this  way to declare a pointer, its type `long` means that this pointer (variable) stores **the address of a variable of type `long`.**&#x20;

Also, it is important for us to know how to draw the stack-frame diagram containing pointers. Below is an example,

<figure><img src="../../../.gitbook/assets/stack-frame-with-pointer.png" alt=""><figcaption><p>Stack Frame with Pointer</p></figcaption></figure>

### **Array Name Decay**

```c
long a[2] = {0, 1};
long *array_ptr = a;
```

**Array Name Dacay** means that after you define an array, and then you want to use the array name, the array name will decay into just a **memory address, not a pointer variable!!!**

{% hint style="info" %}
If you really want to let the array name become a pointer, see [#pointer-to-a-fixed-size-array](../lec-08-multi-d-array-efficiency/#pointer-to-a-fixed-size-array "mention")
{% endhint %}
