# Welcome!

Welcome to this new playground about the BF language. Make sure you already read 
* [Getting started with BrainFuck](https://tech.io/playgrounds/50426/getting-started-with-brainfuck/welcome)
* [BrainFuck part 2 - Working with arrays](https://tech.io/playgrounds/50443/brainfuck-part-2---working-with-arrays/welcome)
* [BrainFuck part 3 - Write a BF interpreter in BF](https://www.codingame.com/playgrounds/50446/brainfuck-part-3---write-a-bf-interpreter-in-bf/welcome)
* [BrainFuck part 4 - Advanced maths](https://www.codingame.com/playgrounds/50446/brainfuck-part-3---write-a-bf-interpreter-in-bf/welcome)
* [BrainFuck part 5 - Math sequences](https://www.codingame.com/playgrounds/50478/brainfuck-part-5---math-sequences/welcome)
* [BrainFuck part 6 - 16-bit integers](https://www.codingame.com/playgrounds/50482/brainfuck-part-6---16-bit-integers/be-smart)
* [BrainFuck part 7 - Quine (+ some non-BF quine theory)](https://www.codingame.com/playgrounds/50485/brainfuck-part-7---quine-some-non-bf-quine-theory/welcome)
* [BrainFuck part 8 - JS/C#/BF Multi quine](https://www.codingame.com/playgrounds/50499/brainfuck-part-8---jscbf-multi-quine/welcome)
* [BrainFuck part 9 - Sort arrays with Bubble and QuickSort](https://www.codingame.com/playgrounds/50516/brainfuck-part-9---sort-arrays-with-bubble-and-quicksort/quicksort)

playgrounds if you didn't already !

The goal of this playground is to implement a calc tool based on reverse polish notation (RPN), and to add extensions on our tool by iterations.

# What is RPN ?

If you owned a calculator manufactured by the Hewlett-Packard company since the 70s, then you can probably skip this section. 

The reverse polish notation is a mathematical notation where operators follows operands.

Let's consider operation `(6 + 2) x 3 - 1 x (5 x 4)`. Result is 4.
* Evaluation of block `6 + 2` with operands 6 and 2, and operator +
* Evaluation of block `5 x 4` with operands 5 and 4, and operator x 
* Evaluation of block `8 x 3`
* Evaluation of block `1 x 20` **prior to subtraction**
* Evaluation of block `24 - 20`
* The second block is `6 x 2`

The notation is easy to understand, but it's evaluation is less easy to implement : we need to find the priority between blocks, operators, ...

Then comes the **Polish notation (PN)**. The same operation becomes

```
- x + 2 6 3 x 1 x 5 4
```

Not so easy to read, right ? Let's try anyway
* minus applies on the next 2 operands
  * multiply applies on the next 2 operands
    * plus applies on the next 2 operands
      * 2
      * 6
    * 6+2 = 8
    * 3
  * 8x3 = 24
  * multiply applies on the next 2 operands
    * 1
    * multiply applies on the next 2 operands
      * 5
      * 4
    * 5x4 = 20
  * 1x20 = 20
* 24-20 = 4

This notations allows to get rid of parentheses, though it's not really easy to read.

And unfortunately, it's also not really easy to interpret : the subtraction was initiated a large number of steps before its computation.

Now, let's look at the **Reverse polish notation(RPN)**. The operator follows the operands

```
6 2 + 3 x 1 5 4 x x -
```

Implementation of an RPN evaluator is quite easy, using a stack-based automaton.

* _empty stack_
* Push 6 _[ 6 ]_
* Push 2 _[ 6 , 2 ]_
* **Add** _[ 8 ]_
* Push 3 _[ 8, 3 ]_
* **Mult** _[ 24 ]_
* Push 1 _[ 24, 1 ]_
* Push 4 _[ 24, 1, 4 ]_
* Push 5 _[ 24, 1, 4, 5 ]_
* **Mult** _[ 24, 1, 20 ]_
* **Mult** _[ 24, 20 ]_
* **Sub** _[ 24 ]_

In other words, an operand is pushed on the stack, and an operator pops operand 2 and operand 1 (in this order) from the stack.

Now, let's implement a BF stack-based RPN evaluator automaton.
