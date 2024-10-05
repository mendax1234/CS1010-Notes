# Midterm (AY20/21)

## Problems

### 6. Logical Expression

> This question assesses whether students can form a **logical expression** given **a set of conditions.**

<figure><img src="../../.gitbook/assets/Midterm-2021-Q6.png" alt=""><figcaption><p>Q6</p></figcaption></figure>

For this kind of question about forming a logical expression given a set of conditions, if the conditions are not too many, we should try the **Truth Table** Method. That is list all the possible conditions and see the output's relationship between the different set of possibilities.

The columns of the table are the **bool** variables given in the table, the output is **bool.** Since we have three variables, so the total possibilities will be $$2^3=8$$, which means we will have 8 rows in total.

| is\_with\_gf | is\_with\_mom | is\_raining | umbrella? |
| ------------ | ------------- | ----------- | --------- |
| Y            | Y             | Y           | Y         |
| Y            | Y             | N           | Y         |
| Y            | N             | Y           | Y         |
| Y            | N             | N           | Y         |
| N            | Y             | Y           | N         |
| N            | Y             | N           | N         |
| N            | N             | Y           | Y         |
| N            | N             | N           | N         |

Then, what we need to do is to find all the **rows** that make the output **True/Y**. We will find that when `is_with_gf == true`, output is always `true`. When `!is_with_mom && is_raining`, the output will be `true`. Otherwise, the output will be `false`. So, we can form our **final logical expression** as:

```
is_with_gf || (!is_with_mom && is_raining)
```

### 11. Recursion

<figure><img src="../../.gitbook/assets/Midterm-2021-Q11.png" alt=""><figcaption><p>Q11</p></figcaption></figure>

This is a recursion question, but it wants to test **how to convert the** `if-else` **structure recursion to a single** `return` **statement including logical expressions only**. But the basic idea is to write the `if-else` structure recursion **first!!!**

So, for this question, the normal `are_coprime_upto_c()` should be

```c
// returns true if a and b share no common factors from 2 to c
bool are_coprime_upto_c(long a, long b, long c) {
    if (c == 1)
    {
        return true;
    }
    if (a % c == 0 && b % c == 0)
    {
        return false;
    }
    return are_coprime_upto_c(a, b ,c - 1);
}
```

First thing first, to make our thinking easier, let's consider when we will `return true`.

1. When `c==1` or
2. when `!(a % c == 0 && b % c == 0) && are_coprime_upto_c(a, b ,c - 1)`, assuming that `are_coprime_upto_c()` will return as expected.

Knowing this, we can form our single `return` statement with the logical expression only easily. That's

```c
return ( c == 1 || (!(a % c == 0 && b % c == 0) && are_coprime_upto_c(a, b, c - 1))
```

## Tips

1. As discussed in [#problem-11.1](../../lec-tut-lab/tutorial/tut-04.md#problem-11.1 "mention"). To prove a program is false, **one counterexample** is enough. But to prove an algorithm is **true,** we may use **assertion** or some other proof techniques. Usually try to find counterexample first!!!
2. If the variables are not too much, always try the **Truth Table** Method since it will make your life and analysis much easier!
3. "_Imprecisions using floating-point values might mean that certain conditions may be evaluated incorrectly_", this is occurred when you want to do the **equality test** between a floating number and an integer.
4. When you want to form a single `return` statement in recursion, write out the normal `if-else` recursion first, then consider under whcih cases we will get `true` output.
