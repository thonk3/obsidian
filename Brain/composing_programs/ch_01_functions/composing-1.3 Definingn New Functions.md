We have identified that programming languages consist of
1. primitive number and arithmetic values and functions
2. nested functions
3. binding names to values **gives a form of** `abstraction`

**Defining functions**

python functions consist of the keywork `def` that inidates a `<name>` and a list of named `<parameters>`, 
then a `return` statement in the function body, specifying the `<return expression>` of the function

```
def <name>(<parameters>):
	return <return expression>
```

> weird they did not elaborate in python indentation
> Im just gonna do dot points now as these are pretty standard
> 
> > [youtube - functions](https://www.youtube.com/embed/j3uTRrPBrKk)
> - although seem overly convoluted, it may be extremely useful when starting out to understand the order of execution in things'
> - fairly wordy and hard to catch but it is very well described

- possible to use functions ass building blocks in other functions
```python
def add(a ,b):
	return a + b

def square(a):
	return a*a

def sum_square(x, y):
	return add(square(x), square(y))
```


## 1. Environments

so now **what if a formal parameter has the same name as a built-ion function?** can 2 functions share same names without confusion

> ah so now they are introducing scope as frames
>
> > [youtube - environment diagrams](https://www.youtube.com/embed/gyk0Qutui1s)
 straight forward demo of scope and named function reassignment
 >
 > everything is relatively fine, but they are bringing some unfamiliar terms in congusing me

- more of an explanation of the Python Tutor page explaining global frames, local frames
- brief talk on **function signature** that is explaining the above function where multiple func with the same name can exist because of different number of parameters

## 2. Calling User-Defined functions

with any function call (user defined or built in) the interpreter follows a computational process.
It evaluates the operator and operands expressions, then applied the named function to the to the resulting arguments.

> ok this introduces the local frame
> - **local** to the function's frame (scope) where the arguments are only accessible to that function
> - this function local are evaluated and consist of 2 frames - the local and globall

\***NameEvaluation** a name evaluate to the value bound to that name in the earliest frame of the current environment in which that name is found

> Examples section goes through the function calling process step by step

## 3. Local names

This context, Local names points to the parameter names

> This principle - the meaning of a function should be independent of the parameter names chosen by its author
> The parameter names of the function is **local** to the body of the function

The scope of the local name (parameter) is limited to the body of the user-defined function which defined it

When the name is no longer accessible, its out of scope

## 4. choosing names

Well chosen names are **essential** for the human interpret-ability of the code.

The following are "guidelines" from [Style guide for python code](https://peps.python.org/pep-0008/), not necessarily enforced but a set of conventions

1. functions are lowercase, seperated by underscores
2. functions names typically reflect the operations of the arguements or the name of the quantity of the result
3. parameter names should reflect the role of the parameter in the function
4. single letter parameters are ok if their role are oblivious

## 5. Function as abstractions

- This shows how powerful user-defined functions are as we can write functions that are depending on other functions without needing to know how it is defined
	- as there are many ways to do a certain thing
- function definition should be able suppress detail

> You dont need to know how a car engine is built to understand it is driving the car

- Programmers should now need to know how the function is used in order to use it
> **Aspects of a functional abstraction** To master the use of a functional abstraction, its often useful to consider its 3 core attributes
> - The domain - set of arguments it can take
> - the range - set of value it can return
> - the intent - relationship it computes between I/O (and any side effects it might generate)

## 6. operators

> Misc operators
> > [Operators](https://www.youtube.com/embed/gDsdcF1bpBs?rel=0&showinfo=0&enablejsapi=1)
>
> seems simple enough skip this for now

[[composing-1.4 Designing Functions]]
back to [[Composing Programs Index]]
