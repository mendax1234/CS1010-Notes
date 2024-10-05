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

## Tips

1. As discussed in [#problem-11.1](../../lec-tut-lab/tutorial/tut-04.md#problem-11.1 "mention"). To prove a program is false, **one counter example** is enough. But to prove an algorithm is **true,** we may use **assertion** or some other proof techniques. Usually try to find counter example first!!!
2. If the variables are not too much, always try the **Truth Table** Method since it will make your life and analysis much easier!
3. "_Imprecisions using floating-point values might mean that certain conditions may be evaluated incorrectly_", this is occurred when you want to do the **equality test** between a floating number and an integer.
