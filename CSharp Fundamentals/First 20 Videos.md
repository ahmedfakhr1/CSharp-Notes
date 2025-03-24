[https://www.youtube.com/watch?v=ohkeYczD1LY&ab_channel=EdAndersen](https://www.youtube.com/watch?v=ohkeYczD1LY&ab_channel=EdAndersen)

  
> [!information] TIP
> Explore specific features of C# like LINQ, delegates, events, and properties
# Study Plan
- Explore specific features of C# like LINQ, delegates, events, and properties
- Write small programs like calculator/todolist app or a basic game using unity
- Use it in problem solving
- Learn .Net Core
- Note that ASP.Net Core is a web framework built on .Net Core
# General
- Enter - New Line - White spaces don't matter between for the compier
- Comenting in visual studio -> ctrl+k , c
- Ctrl+d => duplicating the line
- 
# Console
- Attributes : ForegroundColor, BackgroundColor, Title
# Variables

- naming ⇒
    - can’t use keywords of the language
    - you can start with a ==letter== of an ==underscore==
    - Pascal - camel case - snake
    - should be representable to what it means
- variable declaration and variable assignment
- variables ==must be initialized== for less bugs : )
- If i want the variable name to be one of the reserved ones, I have to start it with @ example: @static or @class
- 
- 

# Boolean

- the difference between & and && , | and || is that the double ones are called ==“short circut operator”== which means that it doesn’t continute tha trails of evaluations from left to right if it doesn’t need to.
    - both get us the same results though

  

# Char DataType (note that “Char” is a class):

- Read () returns _**the Ascii code for the character**_
- ReadLine() returns _**a string**_
- “Enter” is represented by TWO characters and in some systems it is represented in 1 character.
```c#
char.IsLetter()
char.IsDigit()
```

> [!important]  
> Notice that the data types in c# are considered classes with static methods that you can use.  

# String

- array of characters.
- Special characters ⇒ “\n” and “\t” (tab=4 spaces)
- Escape character ⇒ “\”, is put before any special char in order to make it not special.
- concatincation ⇒ +
- ==@ character before a string== makes c# igonore all special characters and you can write your string on a a lot of lines ==like a paragraph==
- ## String Templates/Interpolation :
  ** ==$ character before the string== allows you to use **your** ==**variables**== ==**or a code**== inside the string, for example
    
    ![[/Untitled 83.png|Untitled 83.png]]
    

---

![[/Untitled 1 31.png|Untitled 1 31.png]]

- Methods : StartsWith , EndsWith ,Contains,IndexOf, LastIndexOf, ToUpper , ToLower, Replace, Substring, splitting, join, trimstart, trimend, IsNullOrEmpty
- Properties : Length
# Numeric Data Types

```C#
sizeof(int)
int.MinValue
int.MaxValu
int.parse("1980") //numerical integer in the form of string
```

- int
    - Memory size ⇒ 4 bytes
    - MinValue ⇒ -2147483648
    - MaxValue ⇒2147483648
- uint
    - no negatives
    - Memory size ⇒ 4 bytes
    - MinValue ⇒ 0
    - MaxValue ⇒ 4,294,967,296
- long (8 bytes)
- ulong
- short (2 bytes)
- ushort

---

- float (4 bytes)
- double (8 bytes)
- ==NOTE ⇒ float and double don’t have an unsigned version==
- 
```c#
float a = 1.4f;
```

# Arithmetic operators

- int/int=int
- double/int=double =< it returs the larger data type
- ==takeaway ⇒ the output of the operation is of the larger type of both original operands, so if both are integer and you expect the output to be say double, you need to case one of the operands to be double or float for example.==
- % ⇒ باقي القسمة

## ==Var data type==

- the compiler sets the data type implicitly without you specifying it.

## Operator precedence 

- we use brackets in order to specify our priority.

## Assignment operators

- +=, -= 
```c#
x = y = z = 4; // multiple assignments

```

## pre/post increment/decrement ++,- -

- post increment ⇒ increment but just after implementing this line of code with the old value.
- pre increment → it will increment the value before reading the variable
```c#
Console.writeLine(5 * ++x); 
// in this line,x will be incremented first then the line of code will be implemented normally
```

## comparison operators

![[/image 2.png|image 2.png]]

# String Parsing

- Converting string ⇒ other data types
```c#
int.parse(year) //year is a string
int.TryParse(year) //is better to avoid exception thrown in case the "year" is not convertable.
```

# Control Flow

# debugger basics

- bug ⇒ anything that causes the program to behave unlike what it is intended for.
- The systems does not behave as intended
    - step by step execution
    - breakpoints
	    - F9 adds a breakpoint
	    - F10 stepOver
    - Locals window ⇒ shows all local variables 
    - Watch Window ⇒ to watch a certain variable only, to activate it, right click on the variable and select 'add watch'
    - ==Edit and continue== ⇒ you can edit the code on the go while the debugging is ON, how ? just change the code and ==move the yellow arrow (Execution arrow)== to the code you just changed to start there without the need to restart.

# Arrays

- ==Syntax ⇒ int[] x = {1,4,5,3,2,1} ;==
- ==Syntax ⇒ int[] x = new int[7] ;==
```c#
Array.Sort()
Array.Copy()
```
- sorting in place⇒ ==Array.Sort(x)==;
- Array copying ⇒ ==Array.Copy(source array, destination array, number of elements to copy);==
