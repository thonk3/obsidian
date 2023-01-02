Functions are essential building blocks of a programs
So far, its discussed the formal properties of a functions and how they are applied

> now we learn what makes a great functions.

> **Fundamentally, the qualities of a good function reinforce the idea that functions are abstraction**

- **Each function should have exactly one job**
	- Jobs should be identifiable with a short name, characterized with a single line of text
	- function performing multiple jobs in sequence should be devided into multiple functions
- **Dont repeat yourself**
	- multiple fragments of code shouldnt describe redundant logic
	- if you find yourself repeating - it may be an opportunity for functional abstraction
- **Functions should be defined generally** 

> These guidelines improve the readability of code, reduce errors and often minimize the code written.
> Decomposing a complex task is a skill that takes time to master

## 1.4.1 Documentation

Funciton definition often include documentation describing the function.
`docstring` are conventionally triple quoted in the code

when you call `help` with the name of the function as an arg, you can see its `docstring`

```python
help(add)
```

`docstring` [guidelines](https://peps.python.org/pep-0257/)

## 1.4.2 Default Argument Values

An outcome of defining general functions is the introduction of additional args, which could be difficult to read.

[[composing-1.5 Control]]
back to [[Composing Programs Index]]
