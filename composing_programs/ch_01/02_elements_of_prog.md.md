## Elements of Programming
> Fun tings

When writing programs, it must be written for people to read 

Every powerful language has these three mechanisms:
- **primitive expressions and statements** - simple building blocks
- **means of combination** - compounding elements built from simpler ones
- **means of abstraction** - compound elements that can be named and manipulated

We deal with 2 elements `function` and `data`

## 1. Expressions

> [youtube - expressions](https://www.youtube.com/watch?v=vguCdBIHQmI)
> explaining computational expressions in the concept of maths
>
> *All expressions use function call notation*

> so more or less experiment on the interpreter

Lets begin with the simplest `Primitive expressions`, one of such is just a simple number. Type expression consists of the numeral represents number in base 10

These expressions can be combined with mathematical operators which the compiler will evaluate

## 2. Call Expressions
> [youtube - functions, objects and expression](https://www.youtube.com/watch?v=2SopsFYlGr4)
> General overview of what we went through the previous chapter
> 
> More or less a showcase of the power of python

> video seems swapped over but ok

basic of functions or Call expressions, it applies a function to some arguments

![call expressions](https://composingprograms.com/img/call_expression.png)

- Operator - specifies a function, on evaluation, we say the function `max` is called with arguments 7 and 9, returns a value of 9
- Order of arguments is very important
- Function notation has 3 advantages over mathematical convention of infix notation
	1. may take an arbitrary number of arguments
		- no ambiguity because of the function name
	2. can extend to nested expressions, where the elements can be compound expressions (other functions).
	3. these expressions are unified and easier to deduce via their name

## 3. Importing Library functions

Python defines a large number of functions but **NOT** all the names are available by default. 
Functions are organised into modules, creating the Python Library, and they need to be `import`ed to be used

```python
from math import sqrt
sqrt(256)
# 16.0
```

`import` designate a module name, and then list the named attribute of that module to import (`sqrt`) 

[Py3 Library docs](https://docs.python.org/3/library/index.html)

## 4. Names and the Environment

> [youtube - names, assignment, user defined function](https://www.youtube.com/watch?v=JinchX1Vn-I)
> 
> using built in library names
> assigning called expressions into user defined names
> using `def` to create user defined functions
>
> Types of expressions
> - primitive - numeral, name, string
> - call expressions

critical aspect of programming is how it use names to refer to computational objects

In Python, names can be assign values or via import

the `=` is called the assignment operator

> I think its generally ok to speed through this 

One different thing is you can reassign names form imported functions

```python
from math import max

max = 7
# this is legal wtf
# i guess its the same as import x as y
```

another strange thing is the single statement assignment

```python
a, b, c = 3, 2, 1

a+c 
# 4
```

## 5. Evaluating nested expressions

Goal of this section is to isolate issues about thinking procedurally 

So in nested expressions the interpreter is following a procedure:
1. evaluate the operator then operand subexpressions
2. I dont get the description here but generally evaluate the sunexpressions /operand to its simplest value


## 6. Non-Pure print

> [youtube - print and none](https://www.youtube.com/watch?v=jNYc5Gdwo3c)
>
> explaining what the python interpreter is doing
> interpreter have rules when evaluating a statement
>
> - `print(print(1), print(2))`
> - Pure function v non-pure function

Now we are comparing 2 Types of functions
- Pure 
- Non Pure

**Pure functions**  have some input and returning some output using the input. These have no side effect as a product of computing a value

**Non pure functions** in addition to returning a value, it can cause a side effect

Pure functions are restricted that they cannot have side effect or changed behaviour over time. These restrictions are extremely beneficial as 
- it can be reliably composed into compound call expressions (nested expressions)
- simpler to test, same arguments always returns same value
- essential `ch4`  

[1.3 defining new functions](03_new_functions.md)