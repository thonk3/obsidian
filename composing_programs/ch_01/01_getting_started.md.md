# Intro

All computing begins with 
- Representing information
- specifying the logic to process it
- designing abstractions that manage the complexity of that logic

To master these fundamentals, it will require
- understanding how computer interpret programs
- carry out computational process

## 1.1.4 General Information

> So I need interactive session or na
> Maybe not lets just use ide

As Introduction, several language features will be used as a sneak peak preview

```python
from urllib.request import urlopen
```

`import` loads logic from external data. In this case it loads `urlopen` to access content in an URL

Python code consist of **Statements** and **Expressions**, it
- compute some value
- carry out some actions

Some things
- **Statement** describe action(assignment statement), it carry out the corresponding action
- **Expression** describe computation, computing values
- **Functions** encapsulates logic that manipulates data (use data to carry out a set of instructions) `primary focus of chapter` 
- **Objects** example a `set`, it supports a set of functionalities. Object *bundles* data and logic that manipulates that data
- **Interpreters** `ch3 topic` program that interprets code in a predictable way

> At the end, all these core concepts are closely related


## 1.1.5 Errors

> FUK ITS VERY SIMPLE
> EXPERIMENT
> MAKE MISTAKE
> LEARN

One of the most important skill as a dev would be **interpreting and diagnosing errors** (debugging). This includes:
1. **Test incrementally**: well written code are composed of small, modular components that can be tested separately. Try out everything so you can gain confidence in the components
2. **Isolate Errors**: an output error generally caused by one small part of the component. Trace the error to the smallest fragment of code to be able to fix it
3. **Check your assumptions**: Interpreters always carry out the action correctly. When code behaviour does not match your assumptions, focus on verifying if that assumption is correct.
4. **Consult Others**: ASK FOR HELP YOU DUM DUM

[1.2 elements of programming](02_elements_of_prog.md)


--- 