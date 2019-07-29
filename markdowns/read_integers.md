# Read integers

Let's define what we want to read first
* Digits (0 to 9, codes from 48 to 57)
* Space (separator, code 32)

Our program will read numbers, space separated, and push them onto the stack

# Let's start

* Memory: empty
* Cursor: first cell
* Input: space separated integers

# Process

* Leave an empty space (current number on stack is null)
* While there is a char to read
  * subtract 32 and set else flag
  * if char is null : it's space
    * reset else flag, move to the right
  * otherwise
    * subtract 16 (to get the digit value)
    * add current number 10 times to current digit to get new current number
* loop

# Code
```
>,[                     leave empty space and read char
  let's track our target values here
  space 32
  digit 48 to 57

  >++++[-<-------->]+<  subtract 32
  [                     it's a digit
    >+++[-<---->]<      subtract 16 (total 48)
    <[->++++++++++<]    add current number 10 times to current digit
    >[-<+>]             replace current number by current digit
  ]>[-                  it's space
    >                   move to next stack entry
  ]                     end of switch/case
<,]                     read char and loop
```

# Final state

* Memory: stack of integers
* Cursor: after stack
* Input: empty (read)
* Output: unchanged

# Test program

This program reads space-separated integers and then print them all as chars

```
>                         leave an empty cell (to go back to stack start)
>,[>++++[-<-------->]+<[  calc tool code
>+++[-<---->]<<[->++++++    ** part 2 **
++++<]>[-<+>]]>[->]<,]      ** part 3 **
<[<]>[.>]                 go back to the stack first cell and print whole stack as char
```
