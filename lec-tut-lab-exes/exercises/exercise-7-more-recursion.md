# Exercise 7 - More Recursion

## Problems

### 1. Fill

The troublesome part of this question is the creation and read of 3-D array. Also, understand this question is a bit hard.

### 2. Maze

The main take-away it to use another array which is the same size as the input 2-D char array to store the explored grids.

### 3. Walk

This is a classic dynamic programming problem. This one is just a easy version which only needs to build the table according to the "upper" and "left"

## Tips

1. When writing recursion in 2-D array, always think about how would you not enter an "infinite loop". This is usually down in your **condition to enter the recursion**. Some common methods are:
   1. mark the attendance of the "cell" you have updated.
   2. there is some initial "constant" that you can compare to
