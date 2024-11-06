# PE2 Review

## Important Functions

### Numbers

#### is\_prime()

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

#### count\_factors()

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

### Strings

#### is\_match()

`char *word` is your source string, `size_t i` is the position in `word` you want to start searching for. `char *search_for` is the string that you want to search for in `word`.

```c
bool is_match(char *word, size_t i, char *search_for)
{
    size_t word_len = strlen(word);
    size_t search_len = strlen(search_for);
    size_t j = 0;
    for (j = 0; j < search_len && i + j < word_len; j += 1) {
        if (word[i + j] != search_for[j] ) {
            return false;
        }
    }
    if (j == search_len) {
        return true;
    }
    return false;
}
```

The use of `i` here is awesome! We won't be afraid that our pointer to the string will be moved away!

#### substitute()

An intermediate function that takes in

1. the source string `word`
2. the current position `i`
3. the length of the target string (the string to be searched for) and&#x20;
4. the string to replace with

{% code title="Substitute.c" lineNumbers="true" %}
```c
void substitute(char *word, size_t i, size_t target_len, char *replace_with) {
    size_t replace_len = strlen(replace_with);
    size_t j = 0;
    while (j < replace_len) {
        word[i + j] = replace_with[j];
        j += 1;
    }
    while (j < target_len) {
        word[i + j] = ' ';
        j += 1;
    }
}
```
{% endcode %}

{% hint style="info" %}
Here it is assumed that the length of the target string is **longer than or equal to** the length of the replace string.
{% endhint %}

#### compact()

An intermediate function that takes in the source string `word` and reform the string by ignoring the white space in it.

{% code title="Compact.c" lineNumbers="true" %}
```c
void compact(char *word)
{
    // Use the same assumption above
    size_t src = 0;
    size_t dst = 0;
    size_t word_len = strlen(word);
    while (src < word_len) {
        if (word[src] != ' ') {
            word[dst] = word[src];
            dst += 1;
        }
        src += 1;
    }
    word[dst] = 0;
}
```
{% endcode %}

{% hint style="info" %}
Based on the same assumption above, our `dst` is always smaller than or equal to `src`
{% endhint %}

#### replace()

A complete function that uses [#is\_match](./#is\_match "mention"), [#substitute](./#substitute "mention") and [#compact](./#compact "mention") above to achieve that purpose that given:

1. A source string `word`
2. The substring to search for in the source string `search_for`
3. The string to replace `search_for` called `replace_with`

and after the execution of the function, all the `serach_for` substrings that have appeared in the source string will be replaced with the `replace_with` string.

{% code title="Replace.c" lineNumbers="true" %}
```c
void replace(char *word, char *search_for, char *replace_with)
{
    size_t word_len = strlen(word);
    size_t search_len = strlen(search_for);
    for (size_t i = 0; i < word_len; i += 1) {
        if (is_match(word, i, search_for)) {
            substitute(word, i, search_len, replace_with);
            // Form a new "string" Awesome!
            i += search_len -­ 1;
        }
    }
    compact(word);
}
```
{% endcode %}

## Tips

1. When doing string traversal, it is strongly recommended to use `strlen()` to get the length of the string, and then use a **for loop** to traverse through thes string, with the loop variable `i` indicating the current position of the character we have traversed!

