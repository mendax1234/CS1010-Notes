# Lab 03

## Exercise 1 Further Discussion

### odd.c

A solution that uses no condition is that `m = n + (n % 2) * (n % 2) + 1`, where m is the smallest odd number that is bigger than `n`.

### multiple.c

It is not defined when we divide a non-zero number by 0.

### date.c

There is a method not using conditions. Map each `(m.d)` date to the integer `100m+d`.

### power.c

Remove the useless work, when the base is 0, -1 or 1.

```c
if (x == 0)
{
    return 0;
}
if (x == 1)
{
    return 1;
}
if (x == -1)
{
    return y % 2 == 0 ? 1 : -1;
}
```

Half the calculation

```c
if (y % 2 == 0)
{
    return compute_power(x * x, y / 2);
}
return x * compute_power(x * x, (y - 1) / 2);
```

### taxi.c

An interesting method to optimize the `ceil()` function in C.&#x20;
