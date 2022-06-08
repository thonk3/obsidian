# Defining new functions
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

### Examples

## 3. Local names

## 4. choosing names

## 5. Function as abstractions

## 6. operators

[1.4 Designing functions](./04_designing_functions.md)

---
