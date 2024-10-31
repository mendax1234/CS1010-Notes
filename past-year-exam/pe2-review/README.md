# PE2 Review

## Important Functions

### is\_prime()

Return whether a number is a prime or not. Time complexity is $$O(\sqrt{N})$$.

{% code lineNumbers="true" %}
```c
bool is_prime(long num)
{
  for (long i = 2; i * i <= num; i += 1)
  {
    if (num % i == 0)
    {
      return false;
    }
  }
  return true;
}
```
{% endcode %}

### count\_factors()

Return the number of prime factors of a num. Time complexity is $$O(\sqrt{N})$$

{% code lineNumbers="true" %}
```c
long is_semiprime(long num)
{
  long all = 0;
  long curr = num;
  for (long factor = 2; factor * factor <= curr && curr != 1; factor += 1) {
    long count = 0;
    while (curr % factor == 0) {
      curr = curr / factor;
      count += 1;
    }
    if (count != 0) {
      all += count;
    }
  }
  if (curr != 1) {
    all += 1;
  }
  return all;
}
```
{% endcode %}

