# Final minified version

_Note: always keep the full version to add cases !_

# Minified version

```
>,[>++++[-<-------->]+<[-----[-----[-[--[--[>+++++[-<--->]+<[--[-[------------[--[-[>++++++[-<+++
++>]<<[->++++++++++<]>[-<+>]]>[-<<<[->+<]<[->+<]>>[-<<+>>]>]<]>[-<<<[->+<]<[->+<]<[->+<]>>>[-<<<+
>>>]>]<]>[-<<<[->+>+<<]>[-<+>]>[>>>>++++++++++<<<<[->+>>+>-[<-]<[->>+<<<<[->>>+<<<]>]<<]>+[-<+>]>
>>[-]>[-<<<<+>>>>]<<<<]<[>++++++[<++++++++>-]<-.[-]<]++++++++++.[-]>]<]>[-<<<[-]>]<]>[-<<<[->+>+<
<]>>[-<<+>>]>]<]>[-<<<.>>]<]>[-<<<[->>>+<<<]<[->+>>+>-[<-]<[->>+<<<<[->>>+<<<]>]<<]>[-]>>>[-]>[-<
<<<<+>>>>>]<<<]<]>[-<<<[-<->]>]<]>[-<<<[-<+>]>]<]>[-<<<[->>+<<]>>[-<<<[->+>+<<]>[-<+>]>>]<<<[-]>>
[-<<+>>]]<]>[-<<<[->>>+<<<]<[->+>>+>-[<-]<[->>+<<<<[->>>+<<<]>]<<]>[-<+>]>>>[-]>[-]<<<]<]>[->]<,]
```



Here is the same C# program, minified as well, but longer anyway. **BF rocks !!!**
```
using System;
using System.Collections.Generic;
class Calc{
static void Main(string[] args){
int a,b,c;
Stack<int> s=new Stack<int>();
foreach(String instr in Console.ReadLine().Split(' ')){
switch(instr){
case "P":Console.Out.WriteLine(s.Peek());break;
case "R":a=s.Pop();b=s.Pop();c=s.Pop();s.Push(a);s.Push(c);s.Push(b);break;
case "S":a=s.Pop();b=s.Pop();s.Push(a);s.Push(b);break;
case "A":Console.Out.WriteLine((char)s.Peek());break;
case "C":s.Push(s.Peek());break;
case "D":s.Pop();break;
case "+":s.Push(s.Pop()+s.Pop());break;
case "*":s.Push(s.Pop()*s.Pop());break;
case "-":a=s.Pop();b=s.Pop();s.Push(b-a);break;
case "/":a=s.Pop();b=s.Pop();s.Push(b/a);break;
case "%":a=s.Pop();b=s.Pop();s.Push(b%a);break;
default: s.Push(int.Parse(instr));break;}}}}
```
