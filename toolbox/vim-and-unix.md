# Vim & Unix

## Vim

### Reformatting

To indent **all the code**, use `gg=G`. Then all lines will be indented according to a specific style.

### Commenting Multiple Lines of Code

* Press `CTRL + Q` (on Windows) or `CTRL + V` (On Linux) to enter the `VISUAL BLOCK` Mode.
* Type `SHIFT-I` to insert in `VISUAL BLOCK` Mode. To comment, type `//` and then `ESC` to go back to Normal Mode . Then the text `//` will be inserted in front of each line selected.
* To uncomment, select `//` on each line that you wish to uncomment, and `x` to delete them.

### Changing Names

#### Changing the name of one type/variable/method call

Occasionally, we mix up our variable or our method name, and we need to fix it before the code runs correctly or compiles. Suppose we have

```
double perimeter = get_area();
```

and we realize that we should be calling `get_perimeter` instead. Instead of using backspace or delete to delete the characters one by one, we can use `cw` to change the word `get_area` into `get_perimeter`.

To do so, (i) place the cursor at the beginning of `get_area`. Remember to avoid using arrow keys or `h` or `l` to move letter-by-letter. You can use `w` or `b` for faster word-by-word navigation. (ii) type `cw` to remove the word `get_area` and enter INSERT mode. Now type `get_perimeter` to replace the method name and ESC to return back to NORMAL mode.

> Basically, the command we should memorize here is using `cw` to change one word.

#### Changing multiple names on the same line

> Notice that this method applies to the words **in one line** only.

Sometimes we have multiple occurrences that we wish to change on the same line. Let's say:

```
int area = get_area();
```

and we realize that we should be calculating `perimeter` instead of `area`.\
One option is to use `cw` twice. But we could also use the substitute command, like so.\
Place the cursor on this line, and type `:s/area/perimeter/gc`, and then ENTER. Here is what it does:

* `:`allows us to issue a command to Vim
* `s/<what to substitute>/<substitute with this>/` tells Vim what we want to replace and replace with what.
* `g` stands for `global` and it says that we want to substitute all occurrences (in this line only)
* `c` is optional, and it tells Vim to confirm every replacement with us.

#### Changing multiple occurrences in a block

If there are only a few lines and you can count the size of the scope within which you want to search and replace, you place your cursor at the beginning of the method and issue the command `:.,+4s/<what to substitue>/<substitue with this>`. Here `.` refers to the current line; `,` is a separator, `+4` refers to the next four lines.

Suppose your cursor is far away and you have the line number turned on. Let say the method above appears at Lines 125 to 131. You can issue the command `:125,131s/<what to substitute>/<substitute with this>`.

Alternatively, you can use VISUAL-LINE mode. Place the cursor at the beginning of the method, and press SHIFT-V. This enters the VISUAL-LINE mode. Now, navigate to select the scope within which you want to search and replace (5j or } works in this case), and press :. You will see that the command prompt is pre-filled with `:'<,'>` to signify the selected range. Continue typing `s/<what to substitute>/<substitute with this>` and ENTER.

#### Changing all occurrences in a file

Let's say that you have a typo in a file, where you have named all variables `angel` instead of `angle`, and you want to fix all occurrences of this in the file. You can use `%` to signify that the range of substitution is the entire file.

The command `:%s/angle/angle/g` should replace all occurances for you.

### Typing Long Variable/Function Names

#### Auto-completion

You can type CTRL-P or CTRL-N in INSERT mode to auto-complete a word. So you only need to type the long name the first time. Subsequently, type the prefix and auto-complete.

#### Abbreviation

You can set up a temporary abbreviation in your `~/.vimrc`. Example

```
ab noc num_of_customers
```

After the configuration is read, you only need to type noc in your code and it will be automatically expanded to `num_of_customers`.

This is useful for functions from the CS1010 library, such as `cs1010_println_long`, as well.

### Fixing Mistakes

#### Undo and Redo

`u` undoes the last action. `CTRL+R` redoes the action.

## Unix

### Terminal Control Sequence

* `CTRL` + `D`: signal the end of input to a program.
* `CTRL` + `Z`: suspend the current running program.
* `CTRL` + `C`: terminate the current running program.
* `CTRL` + `S`: freeze the terminal.
* `CTRL` + `Q`: resume the terminal.

> Note that often hitting `CTRL` + `Z` will causing the resources not freed in time. So, try to use `CTRL` + `C` instead.

### Unix Directory

For the home directory, sometimes we add the username behind `~` to indicate the home directory of the other user. E.g., `~bob` means the home directory of a user named `bob`.

### Directory-related Commands

* In Unix, a file or directory with a name that starts with `.` is hidden from `ls`. To show these files, we need to run `ls` with `-a` flag.
* Entering `cd` alone brings you back to your **home directory**.
* `rmdir`: ReMove a subDIRectory\
  `rmdir` removes a subDIRectory in the current directory -- note that a directory must be **empty** before it can be removed.

### File Management

* To copy a directory, we use `cp -r`, where `-r` stands for copying recursively.
* The `cp` command takes in two arguments, the first is the **source**, the second is the **destination**.
* Same as the `cp` command, the `mv` command takes in two arguments also. THe first one is **source** and the second one is **destination**.
* `rm -rf`, `-r` means recursively, `-f` means force.
* `cat`: CATenate file content to screen\
  This command is used to take a look at the content of the file. If the file is too long, we can use the variant of `cat`, called `less`. In `less`, we use `<space>` to move down one page, `b` to move Back up one page and `q` to quit. And if not argument is specified, `cat` will use the standard input (keyboard) as its input. And in this case, remember to use `CTRL` + `D` to signal the end of the input.
* `man`: MANual\
  Just use `man <name of command>` to see the manual of that command.

### File Permission Management

#### The _What_ of File Permissions

`r` is read, `w` is write, `x` is execute. And the permissions on a file can be expressed in two ways:

1. using symbolic notation. For instance, `rwx`, `r-x`, `-wx`, where a `-` means that the corresponding permission is not given (in the order of `r`, `w`, `x`)
2. using a numerical notation. This notation uses a digit between 0 to 7, which is computed as a sum of individual digit representing the permissions: `r` is represented with 4, `w` is represented with 2, and `x` is represented with 1. For instance, `r-x` has a numerical representation of 5(4+1), and `-wx` has a numerical representation of 3(2+1). And the max is 7(4+2+1).

#### The _Who_ of File Permissions

Unix divides the users into **three** classes: `u` is the **u**ser who owns the file; `g` refers to the users in the same **g**roup as the user; and `o` are all the **o**ther users.\
The permission can be controlled separately for these classes of users. The permission notation simply concatenates the file permissions of each class of users together, in the order of `u`, `g` and `o`.\
For instance, the permission of 644, or `rw-r--r--`, on a file means that:

* the owner can read and write
* the group users can only read
* all the other users can only read Sometimes you may see `d` in front of the permission, that means it is a **directory**.

### Standard Input/Output

#### Output Redirection

The operators `>` and `>>` are used to redirect the standard output to a file. The difference is that `>` will overwrite the given file, while `>>` will concatenate into the given file.

#### Input Redirection

The operatros `<` is used to redirect a file into the standard input. So, instead of reading from the keyboard, we can now read from a file. For example, `wc test.txt` is the same with `wc < test.txt`. A slight difference is that the second one will have no file name.

> In most CS programming assignments, however, to keep things simple, you will be asked to read from the standard input only, so the `<` is a great-time-saver -- you do not have to repeatedly type in the same input data over and over from the keyboard. You can just save the input data in a file, then redirect it to standard input with the `<` operator.

### Advanced

#### Composing Programs with `|`

The `|` operator takes the standard output from one program and redirects it as the standard input of another program. For example

```bash
$ cat test.txt | wc
    1   11  64
```

and this command is just the same as

```bash
$ wc < test.txt
```

Another example that shows the power of `|` is that suppose we have three files and we want to count the total number of lines, words and characters in these three files. We can use one line of command to achieve this,

```bash
cat test.txt foo.txt bar.txt | wc
    3   33  192
```

#### Some other commands

* `echo` simply prints out the command-line argument to the standard output (terminal)

```bash
$ echo "hello world!"
hello world!
```

* `sort` rearrange the input lines in alphabetical order.
* `uniq` remove any two consecutive lines that are the same.
* `grep` returns the lines of text from the given file (or the standard input) that matches the given string. For instance, run

```bash
grep abc
```

and start typing in some lines of text, some containing `abc`, some do not. `grep` will spew out into the standard output all the lines that contain the text `abc` somewhere. As usual, hit `CTRL` + `D` when you are done.\
To `grep` a pattern in a directory, use `grep -r <pattern> <directory>`

See the famous [pipe example](https://nus-cs1010.github.io/2425-s1/guides/unix-advanced.html) example from CS1010.

> Notice that the `wc -l` means we only want to print the number of lines to our standard output.

### Pattern matching in `bash`

| Pattern    | Matches                                                                                |
| ---------- | -------------------------------------------------------------------------------------- |
| `*`        | 0 or more characters                                                                   |
| `?`        | One character                                                                          |
| `[..]`     | One character, coming from the given set between `[` and `]`, `-` to indicate a range. |
| `{.., ..}` | Either one of the names, separated by `,`.                                             |

Example 1,\
`ls [f-t]*t` matches all file names that start with the alphabet `f`, `g`, etc, until `t`, followed by zero or more characters, followed by `t`.

Example 2,\
`ls {fo,ba}??txt` matches any file names that start with either `fo` or `ba`, followed by two characters, followed by `txt`.

## Credit

1. [CS1010 Handbook - Vim Common Operations](https://nus-cs1010.github.io/2425-s1/guides/vim-operations.html)
2. [CS1010 Handbook - Unix Background](https://nus-cs1010.github.io/2425-s1/guides/unix-background.html)
3. [CS1010 Handbook - Unix Essentials](https://nus-cs1010.github.io/2425-s1/guides/unix-essentials.html)
4. [CS1010 Handbook - Unix Advanced](https://nus-cs1010.github.io/2425-s1/guides/unix-advanced.html)
