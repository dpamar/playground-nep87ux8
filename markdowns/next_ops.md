# Next operators

Let's add the missing mathematical operators : mod (%) and divide (/)
* Modulus (code 37)
* Divide (code 47)

Note that this operator will not consumes the first stacked value : it will print it bu value remains unchanged

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
  * subtract **5** (total 42), if char is null : it's multiply
    * reset else flag, multiply the 2 operands
  * subtract 1 (total 43), if char is null : it's addition
    * reset else flag, sum the 2 operands
  * subtract 2 (total 45), if char is null : it's subtraction
    * reset else flag, subtract the 2 operands
  * subtract 2 (total 47), if char is null : it's division
    * reset else flag, divide the 2 operands
  * subtract **33** (total 80), if char is null : it's print
    * reset else flag, print first operand
  * otherwise
    * **add 32** (to get the digit value)
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
  print 80
  digit 48 to 57

  >++++[-<-------->]+<  subtract 32
  [-----                subtract 5
  [-----                subtract 5
  [-                    subtract 1
  [--                   subtract 2
  [--                   subtract 2
  [>++++++++++[-<--->]+< subtract 33
  [                     it's a digit
    >+++[-<++++++++>]<  add 32 to get digit value (and reset else flag)
    <[->++++++++++<]    add current number 10 times to current digit
    >[-<+>]             replace current number by current digit
  ]>[-                  now unwind cases: it's print
    <<<[->+>+<<]>[-<+>] copy number (to remain value unchanged after print)
    >[>>>>++++++++++<<< print copied value
    <[->+>>+>-[<-]<[->>   as a decimal number
    +<<<<[->>>+<<<]>]<<   ** part 3 **
    ]>+[-<+>]>>>[-]>[-<   ** part 4 **
    <<<+>>>>]<<<<]<[>++   ** part 5 **
    ++++[<++++++++>-]<-   ** part 6 **
    .[-]<]                ** part 7 **
    ++++++++++.[-]>     print newline (and reset newline char)
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

You can try with input `11 22 + 3 * P 6 P / P 5 P % P` for example. It should print 99, 6, 16 (integer part of 99/6), 5, 1 (result of 16 % 5)
