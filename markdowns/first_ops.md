# First operators

Let's add 3 operators to our system now :
* addition (code 43)
* subtraction (code 45)
* multiplication (code 42)

# Let's start

* Memory: empty
* Cursor: first cell
* Input: space separated integers and operators

# Process

* Leave an empty space (current number on stack is null)
* While there is a char to read
  * subtract 32 and set else flag
  * if char is null : it's space
    * reset else flag, move to the right
  * subtract 10 (total 42), if char is null : it's multiply
    * reset else flag, multiply the 2 operands
  * subtract 1 (total 43), if char is null : it's addition
    * reset else flag, sum the 2 operands
  * subtract 2 (total 45), if char is null : it's subtraction
    * reset else flag, subtract the 2 operands
  * otherwise
    * subtract 3 (to get the digit value), and not 16 anymore (target total is 48, so 45+3 and not 32+16)
    * add current number 10 times to current digit to get new current number
* loop

# Code
```
>,[                     leave empty space and read char
  let's track our target values here
  space 32
  multiply 42
  add 43
  subtract 45
  digit 48 to 57

  >++++[-<-------->]+<  subtract 32
  [----------           subtract 10
  [-                    subtract 1
  [--                   subtract 2
  [                     it's a digit
    --->-<              subtract 3 to get digit value (and reset else flag)
    <[->++++++++++<]    add current number 10 times to current digit
    >[-<+>]             replace current number by current digit
  ]>[-                  now unwind cases: it's subtraction
    <<<[-<->]>          do the subtraction
  ]<]>[-                next case : it's add
    <<<[-<+>]>          do the addition
  ]<]>[-                next case : it's multiply
    <<<[->>+<<]>>[-<<<  do the multiplication
    [->+>+<<]>[-<+>]>>    ** part 2 **
    ]<<<[-]>>[-<<+>>]     ** part 3 **
  ]<]>[-                next case : it's space
    >                   move to next stack entry
  ]                     end of switch/case
<,]                     read char and loop
```

# Final state

* Memory: stack of integers
* Cursor: after stack
* Input: empty (read)
* Output: unchanged

_Note_: We can see how to add cases now:
* get the target code
* put somewhere in cases switch the code to match
* add implementation when we unwind the cases stack

_Note 2_: as all the digits are processed the same way, we will continue to process them as the default case (avoids 10 different implementations for 10 codes)

# Test program

This programs reads integers and the 3 operands, all space-separated, and then prints values on the stack as chars
```
>                                                           add empty cell
>,[>++++[-<-------->]+<[----------[-[--[--->-<<[->+++++++   calc tool
+++<]>[-<+>]]>[-<<<[-<->]>]<]>[-<<<[-<+>]>]<]>[-<<<[->>+<     ** part 2 **
<]>>[-<<<[->+>+<<]>[-<+>]>>]<<<[-]>>[-<<+>>]]<]>[->]<,]       ** part 3 **
<[<]>[.>]                                                   print stack as chars
```

You can try with input `6 8 * 7 7 * 1 7 7 * +` for example. 6x8 = 48, char 0; then 7x7=49, char 1; and finally 1+(7x7)=50, char 2; so it prints 012
