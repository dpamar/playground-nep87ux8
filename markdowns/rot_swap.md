# Rotate and swap

Let's now add some other stack manipulation functions. Namely, Rot (R) that transform the stack A,B,C (from top to bottom) into B,C,A; and Swap (S) that transforms stack A,B into B,A
* Rot (code 82)
* Swap (code 83)

Note that these operatoris will not consume the stacked values

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
  * subtract 5 (total 37), if char is null : it's modulus
    * reset else flag, compute A mod B
  * subtract 5 (total 42), if char is null : it's multiply
    * reset else flag, multiply the 2 operands
  * subtract 1 (total 43), if char is null : it's addition
    * reset else flag, sum the 2 operands
  * subtract 2 (total 45), if char is null : it's subtraction
    * reset else flag, subtract the 2 operands
  * subtract 2 (total 47), if char is null : it's division
    * reset else flag, divide the 2 operands
  * subtract 20 (total 67), if char is null : it's copy
    * reset else flag, copy first operand
  * subtract 1 (total 68), if char is null : it's drop
    * reset else flag, drop first operand
  * subtract 12 (total 80), if char is null : it's print
    * reset else flag, print first operand
  * subtract 2 (total 82), if char is null : it's rot
    * reset else flag, rotate stack's head
  * subtract 1 (total 83), if char is null : it's swap
    * reset else flag, swap first 2 operands
  * otherwise
    * add **35** (to get the digit value)
    * add current number 10 times to current digit to get new current number
* loop

# Code
```
>,[                     leave empty space and read char
  let's track our target values here
  space 32
  modulus 37
  multiply 42
  add 43
  subtract 45
  divide 47
  copy 67
  drop 68
  print 80
  rot 82
  swap 83
  digit 48 to 57

  >++++[-<-------->]+<  subtract 32
  [-----                subtract 5
  [-----                subtract 5
  [-                    subtract 1
  [--                   subtract 2
  [--                   subtract 2
  [>++++[-<---->]+<     subtract 20
  [-                    subtract 1
  [------------         subtract 12
  [--                   subtract 2
  [-                    subtract 1
  [                     it's a digit
    >++++++[-<+++++>]<  add 35 to get digit value (and reset else flag)
    <[->++++++++++<]    add current number 10 times to current digit
    >[-<+>]             replace current number by current digit
  ]>[-                  now unwind cases: it's swap
    <<<[->+<]           move A to the right
    <[->+<]             move B at A initial location
    >>[-<<+>>]>         move A where B was initially
  ]<]>[-                next case: it's rot
    <<<[->+<]<[->+<]<[- move A and B and C to the right
    >+<]>>>[-<<<+>>>]>    and move A where C was initially
  ]<]>[-                next case: it's print
    <<<[->+>+<<]>[-<+>] copy number (to remain value unchanged after print)
    >[>>>>++++++++++<<< print copied value
    <[->+>>+>-[<-]<[->>   as a decimal number
    +<<<<[->>>+<<<]>]<<   ** part 3 **
    ]>+[-<+>]>>>[-]>[-<   ** part 4 **
    <<<+>>>>]<<<<]<[>++   ** part 5 **
    ++++[<++++++++>-]<-   ** part 6 **
    .[-]<]                ** part 7 **
    ++++++++++.[-]>     print newline (and reset newline char)
  ]<]>[-                next case: it's drop
    <<<[-]>             remove stack first value
  ]<]>[-                next case: it's copy
    <<<[->+>+<<]        duplicate stack first value
    >>[-<<+>>]>         move duplicate back to original location
  ]<]>[-                next case: it's division
    <<<[->>>+<<<]<      move 2nd operand
    [->+>>+>-[<-]<[->>+ divide
    <<<<[->>>+<<<]>]<<]   ** part 2 **
    >[-]>>>[-]>[-<<<<   move result
    <+>>>>>]<<<           ** part 2**
  ]<]>[-                next case: it's subtraction
    <<<[-<->]>          do the subtraction
  ]<]>[-                next case : it's add
    <<<[-<+>]>          do the addition
  ]<]>[-                next case : it's multiply
    <<<[->>+<<]>>[-<<<  do the multiplication
    [->+>+<<]>[-<+>]>>    ** part 2 **
    ]<<<[-]>>[-<<+>>]     ** part 3 **
  ]<]>[-                next case : it's modulo
    <<<[->>>+<<<]<      move 2nd operand
    [->+>>+>-[<-]<[->>+ divide
    <<<<[->>>+<<<]>]<<]   ** part 2 **
    >[-<+>]>>>[-]       move result
    >[-]<<<               ** part 2 **
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

# Test program

The program can be tested on its own.

You can try with input `6 8 * C 1 + S C 2 + S R P D P D P` for example. It should
* computes 48
* copy 48 and add 1 to compute 49 (stack: 49, 48)
* swap and copy (stack: 48, 48, 49)
* add 2 to compute 50 (stack: 50, 48, 49)
* swap (stack: 48, 50, 49)
* rotate (stack: 50, 49, 48)
* and finally print and rotate 3 times: this prints 50, 49 and 48
