In most powerful programming languages, they must consist these elements
1. Numbers and Arithmetic operations are `primitive` built-in data values and functions
2. Nested functions provides a mean of `combining` operations
3. binding names to values is a limited form of `abstraction`

On _function definitions_, this is a powerful `abstraction` technique where a `name` can be bound to a compound operation
```python
def <name>(<parameters>):
return <return expression>
```
`python` functions consist of the keywork `def` that initiate a `<name>` and a list of named `<parameters>`.
then a `return` statement in the function body, whis is an expression to be evaluated

> [youtube - functions](https://www.youtube.com/embed/j3uTRrPBrKk)
> - although seem overly convoluted, it may be extremely useful when starting out to understand the order of execution in things

understanding how to properlly format your functions is ideal, as each and every function can be used as building blocks of your application

## 1.3.1 Environments

**what if a formal parameter has the same name as a built-in function?** can 2 functions share same names without confusion

> [youtube - environment diagrams](https://www.youtube.com/embed/gyk0Qutui1s)
> - `scope` introduced as `frames`
> - straight forward demo of `scope` and named function reassignment

The `Environment` where your `expression` is evaluated consist of a `sequence of frames` (or boxes) 
- each `frame` contains `bindings`
- each associates a `name` with its corresponding value
- there is a `global frame`
- `import` and `assignment` add entries to the frame of the current environment

> This is such a convoluted way of describing scope
> But I guess it is difficult to describe the concept of scope in general, I learned it via trial and error

## 1.3.2 Calling User-Defined functions

A function evaluation follows a computational process:
It evaluates the operator and operands expressions, then applied the named function to the to the resulting arguments.

A `user-defined function` introduces a second `local frame` - only accessible to the function
Its arguments are 
1. bind to `names` only available in the new `local frame`
2. executes the body of the functions

> - **local** to the function's frame (scope) where the arguments are only accessible to that function
> - this `local` frame has access to other `bindings` of the local frame

`NameEvaluation` a name evaluate to the value bound to that name in the earliest frame of the current environment in which that name is found

## 1.3.3 Local names

> This principle - the meaning of a function should be independent of the parameter names chosen by its author
> The parameter names of the function is `local` to the body of the function

The scope of the local name (parameter) is limited to the body of the user-defined function which defined it

When the name is no longer accessible, its `out of scope`

## 1.3.4 choosing names

Well chosen names are `essential` for the human interpret-ability of the code.

The following are "guidelines" from [Style guide for python code](https://peps.python.org/pep-0008/), not necessarily enforced but a set of conventions

1. functions are `lowercase`, seperated by underscores
2. functions names typically reflect the operations of the arguements or the name of the quantity of the result
3. parameter names should reflect the role of the parameter in the function
4. single letter parameters are ok if their role are oblivious

## 1.3.5 Function as abstractions

- This shows how powerful user-defined functions are as we can write functions that are depending on other functions without needing to know how it is defined
	- as there are many ways to do a certain thing
- Function definition should be able to suppress details
> You dont need to know how a car engine is built to understand it is driving the car

Programmers should `not` need to know how the function is used in order to use it

`Aspects of a functional abstraction` To master the use of a functional abstraction, its often useful to consider its 3 core attributes
- The domain - set of arguments it can take
- the range - set of value it can return
- the intent - relationship it computes between I/O (and any side effects it might generate)
> These attributes do not specify how the intent is carried out, that information is `abstracted`

## 1.3.6 operators

> Misc operators
> > [Operators](https://www.youtube.com/embed/gDsdcF1bpBs?rel=0&showinfo=0&enablejsapi=1)
>
> seems simple enough skip this for now

[[composing-1.4 Designing Functions]]
back to [[Composing Programs Index]]
