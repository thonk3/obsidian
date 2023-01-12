As of until now the abilities of functions are fairly limited as we have not introduced
- ways to make comparison
- perform different operations depending on the result of comparisons

`Control statements` controls the flow of program's execution based on the result of logical comparisons

## 1.5.1 statements

`statements` differes with everything we know so far
Instead of computing, `statements` dertermines what the interpreter should do next

So far we've seen three kind of statements 
- assignment
- `def`
- `return`
These are not expressions although they contain expressions as components

Rather being evaluated, `statements` are executed.
Each statement describes some change to the interpreter state, and executing a statement applies that change.
Hence, executing a **statement** can involve evaluating sub-expressions contained within them

## 1.5.2 Compound statements

Simply its a statement composed of other statements

> but the description makes it seems more than that

The definition exposes the essential structure of a recursively defined `sequence`
A sequence can be decomposed into its first element and the rest of its elemnt.
The rest of a sequence of statements it self is also a statement.
Thus we can apply this rule recursively

Its important to remember that statements are executed in order.
but some may never be reached becaused of `redirected control`

## 1.5.3 Functions - Local Assignments

- variable assignment within the scope of functions
- `return` statement redirects controll
	- process funtion `terminates` when the first `return` statement is executed
	- value of the `return` expression is the returned value of the function being applied
- effect of `assignment` statement is to bind a name to a value to the first scope of the current environment
	- assignment statements within `function` body cannot affect the `global` scope
	- function can only manipulate the local environment `pure functions`

## 1.5.4 Conditional statements

> the `if` , `elif` and `else` statement is self explanatory
> you know this, no need to rewrite

> Explains boolean logic

`python` uses `short circuting`, determining value without evaluating all of its subexpressions

for `<left> and <right>`
1. eval `<left>`
2. if the result is `false` then the expression evaluates to `false`
3. otherwise, the expression evaluates fo the value of the subexpression `<right>`
for `<left> or <right>`
1. eval `<left>`
2. if the result is `true` then the expression evaluates to `true`
3. otherwise, the expression evaluates fo the value of the subexpression `<right>`
for `not <expression>`
1. reverse the value after evaluating `<expression>`

## 1.5.5 Iterations

`Itterations` are control statements used to express repetition
> So far only `while` loops

To execute a `while` loop
1. evaluate the header expresion 
2. if it is true, execute the suite, then return to step 1
> Talk about `infinite loops`

## 1.5.6 Testing

`Testing` a function is the act of verifyng that the function behaviour matches expectations.o

`Test` is a mechanism for systematically performing this verification.
This takes the form of another `function` that contains one or more sample call to the function being tested.
The returned value is then `verified` against an expected result.
`Tests` are ment to be general, it involves vaidating calls with specific argument values.
But this could also serve as a form of `documentation` (how to call a `function` and what arguments are apropriate)

#### `Assertions`
- `assert` statements are to verify expressions
	- e.g output of a function being tested
- `assert` statement has an expression in a `bool` context followed by a string to display if the expression evaluated to false

#### `Doctests`
- library to provide ways to place tests directly in the docstring of a function

> ...

The key to effective testing is to write (and run)tests immediately after implementng the new function
Its also good practice is to write tests **before** implementation to have some example i/o
A test that applies a single function is called a `unit test`

> Exhaustive `unit testing` is a hallmark of good program design

---

[[composing-1.6 Higher-order functions]]
back to [[Composing Programs Index]]