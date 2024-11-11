# PE2 Review

## Important Functions

### Array

#### Define a Fixed length 2-D array

{% code overflow="wrap" lineNumbers="true" %}
```c
long dir[8][2] = {{1, -1}, {1, 1}, {-1, 1}, {-1, -1}, {0, -1}, {0, 1}, {1, 0}, {-1, 0}};
```
{% endcode %}

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

<pre class="language-c"><code class="lang-c">/*
 * @param word       the word (can be a line) you want to search for
 * @param i          the position in the word to start searching
 * @param search_for the string you want to search for
 *
 * @output return true if search_for is in word. Otherwise return false
<strong> */
</strong>bool is_match(char *word, size_t i, char *search_for)
{
    size_t word_len = strlen(word);
    size_t search_len = strlen(search_for);
    size_t j = 0;
    for (j = 0; j &#x3C; search_len &#x26;&#x26; i + j &#x3C; word_len; j += 1) {
        if (word[i + j] != search_for[j] ) {
            return false;
        }
    }
    if (j == search_len) {
        return true;
    }
    return false;
}
</code></pre>

{% hint style="info" %}
The use of `i` here is awesome! We won't be afraid that our pointer to the string will be moved away!
{% endhint %}

#### substitute()

An intermediate function that replace the target string with the replace string plus white spaces.

{% code title="Substitute.c" overflow="wrap" lineNumbers="true" %}
```c
/*
 * @param word the source word (can be a line)
 * @param i    the current position
 * @param target_len the length of the target string (the string to be searched for)
 * @param replace_with the string to replace with
*/
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

A complete function that uses [#is\_match](./#is\_match "mention"), [#substitute](./#substitute "mention") and [#compact](./#compact "mention") above to achieve the purpose that after the execution of the function, all the `serach_for` substrings that have appeared in the source string will be replaced with the `replace_with` string.

{% code title="Replace.c" lineNumbers="true" %}
```c
/*
 * @param word the source string word (can be a line)
 * @param search_for the substring to be searched for (or target string)
 * @param replace_with the string used to replace the search_for/target string
*/
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

#### My Solution for [#id-5.-substring](pe2-ay20-21.md#id-5.-substring "mention")

{% code lineNumbers="true" %}
```c
/**
 * @param src  The source string
 * @param len  The length of source string
 * @param k    The length of the remaining characters
 * @param curr The position / Number of characters we have appended
 * @param sub  The substring
 */
void print_sub(char *src, size_t len, size_t k, size_t curr, char *sub)
{
  // No more remaining characters
  if (k == 0)
  {
    sub[curr] = '\0';
    cs1010_println_string(sub);
    return;
  }
  // Iterate through all the possible characters we can choose
  for (size_t i = 0; i <= len - k; i += 1)
  {
    sub[curr] = src[i];
    print_sub(src + i + 1, len - i - 1, k - 1, curr + 1, sub);
  }
}
```
{% endcode %}

### Binary Search

#### Binary Search in a Rotated Sorted List

> Appeared in [#id-3.-rotate](pe2-ay18-19.md#id-3.-rotate "mention")

{% code lineNumbers="true" %}
```c
/* 
 * @param a   the rotated sorted list
 * @param i   start position in the list (inclusive)
 * @param j   end position in the list (inclusive)
 * @param q   the number to search for
 * @param len the length of the list
 *
 * @output the position of q in the rotated sorted list
*/
long search(long *a, long i, long j, long q, size_t len)
{
  if (i > j)
  {
    return -1;
  }
  // Get how many bits have been right rotated
  long rotate = rotate_pos(a, len);
  long mid = (i + j) / 2;
  // Calculate the updated index
  long mid_rotated_pos = within_range(mid, rotate, len);
  if (a[mid_rotated_pos] == q)
  {
    return mid_rotated_pos;
  }
  if (a[mid_rotated_pos] > q)
  {
    return search(a, i, mid - 1, q, len);
  }
  return search(a, mid + 1, j, q, len);
}
```
{% endcode %}

Where, `within_range()` is implemented as follows;

{% code lineNumbers="true" %}
```c
long within_range(long index, long rotate, size_t len)
{
  if ((index + rotate) >= (long)len)
  {
    return index + rotate - (long)len;
  }
  return index + rotate;
}
```
{% endcode %}

#### Binary Search to get the length of "#"

> Appear in [#id-4.-box](pe2-ay21-22.md#id-4.-box "mention") (AY21/22) and [#id-4.-mode](pe2-ay23-24.md#id-4.-mode "mention")(AY23/24)

1. Recursive Method

{% code lineNumbers="true" %}
```c
/*
 * @param histogram The input board
 * @param start     The start searching position (inclusive)
 * @param end       The end searching position (inclusive)
 * @param row       The specific row to search for
 *
 * @output the number of '#' in the row
*/
size_t search_row(char **histogram, size_t start, size_t end, size_t row)
{
  if (end == start)
  {
    return start;
  }
  size_t mid = (start + end) / 2;
  if (histogram[row][mid] == '#')
  {
    return search_row(histogram, mid + 1, end, row);
  }
  return search_row(histogram, start, mid, row);
}
```
{% endcode %}

2. Iterative Method

{% code lineNumbers="true" %}
```c
/*
 * @param histogram The input board
 * @param r         The specific row to search for
 * @param m         The length of the row (exclusive)
*/
size_t score(char **histogram, size_t r, size_t m)
{
  size_t i = 0;
  size_t j = m - 1;
  while (i < j)
  {
    size_t mid = (i + j) / 2;
    if (histogram[r][mid] == '#' && histogram[r][mid+1] == '#')
    {
      i = mid+1;
    }
    else
    {
      j = mid;
    }
  }
  return i+1;
}
```
{% endcode %}

## Standard C Libaray

### ctype.h

1.

## Tips

1. When doing string traversal, it is strongly recommended to use `strlen()` to get the length of the string, and then use a **for loop** to traverse through thes string, with the loop variable `i` indicating the current position of the character we have traversed!
2. Refer back to [Lab 09 - Backtracking](https://wenbo-notes.gitbook.io/cs1010-notes/lec-tut-lab-exes/lab/lab-09-backtracking) when doing the backtracking problems! Usually, an easier way to help you understand is to **draw a "tree"**.
3. When doing Backtracking/Recursion problems, always think about the three statements, they will help you form the solution: a)**Current Stage,** b)**Terminating Condition,** c)**State Transitions**
4. Somtimes changing the **loop condition** will change the obvious time complexity, pay attention to the "hidden" time complexity and sometimes this kind of change can be utilised to make your code more effificient. See [#id-2.-sun](pe2-ay20-21.md#id-2.-sun "mention")
5. When you want to improve the complexity of **searching/sorting** problems, try thinking about how to **narrow your "searching area"**. This will be very useful!
6. The `strlen()` from C standard lib `<string.h>` will return **the number of characters in a string** (excluding the terminating `'\0'`).
7. Whenever you see the Time complexity is $$O(logN)O(logN)$$, try to think of **binary search**.
