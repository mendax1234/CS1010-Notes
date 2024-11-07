# Lab 09 - Backtracking

## Exercise 6

### 4. Marks

Construct a **cumulative frequency** table.

## Recursion & Backtracking

It seems (erroneously) that recursion is always about "going backwards". but it is not always the case.

A problem-solving paradigm (Usually used in AI):

* Suppose we have an **initial state** S.
* Our **goal** is to find all states where a **terminating condition** p holds.
* Upon entering each **current state X**, we first check if p is true. If it is, we **collect X** as a valid result.
* Else, we explore the **actions** that can be performed at state X to **transition** to a different state Y.
* For each new state Y generated this way, we enter it and repeat the process.
* After **exhausting** all possible actions, we **return** to the previous state.

And the steps can be summarized as:

1. Define goal(S)
2. Define condition for goal(S)
3. Define state representation
4. Define actions and transitions (Usually it is recursion)
5. Invoke function with initial state

Backtracking is **searching by brute force.**

{% hint style="info" %}
The difficult part is for us to find "initial state S, goal, terminating condition, actions that can be performed to transition, return to the previous state".
{% endhint %}

We can practice this kind of thinking using one of the past year PE questions [#id-5.-stone](../../past-year-exam/midterm-pe/pe1-ay21-22.md#id-5.-stone "mention").

1. We start our sequence $$s=\empty$$ and number of digits k = 0
2. (Add it after the lab)

(Missing code for Stone.c here)

### Graph Traversal

Taking the Depth-First-Search as an example. Given that two vertices v and u, we wish to determine whether they are connected by a path.

Identify the following"

1. **Current Stage:** The current vertex x (initially v)
2. **Terminating Condition**: x=u
3. (Missing notes)

## Exercise 7

### 3. walk

A genius way to solve this problem is to use combinatorics! Legit genius! But only implementing $$nCr$$ directly is not correct! (The factorial will easily exceed the space limit of `long`). Try the step-by-step solution.
