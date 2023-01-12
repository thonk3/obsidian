> [Higher order function](https://www.youtube.com/embed/UlXvz-34Me0?rel=0&showinfo=0&enablejsapi=1)

The main thing we see from powerful programming language is the 
`ability to build abstractions by assigning names to common patterns, then to work in terms of the names directly`
Function provide this ability as we will see later on.

To express certain general patterns as named concepts, we will need to `construct functions that accepts other functions as arguments` or `return functions as values`.

> Function that manipulates other functions are called higher-order functions. `Higher order functions` can serve as powerful abstraction mechanisim, vastly increasing the expressive power of our language

## 1.6.1 Functions as Args

Shows the concept of passing a function via function arguments using the example of `sum_naturals` computing a sum of natural numbers up to `n` 
```python
def sum_naturals(n):
	total, k = 0, 1
	while k <= n:
		total = total + k
		k = k + 1
	return total
```
`sum_cubes`, compute the sum of the cubes of natural up to `n`
```python
def sum_cubes(n):
	total, k = 0, 1
	while k <= n:
		total = total + k*k*k
		k = k + 1
	return total
```
These 2 functions clearly share a common underlying pattern and for the most part identical. Differes only in name and the function of `k` used to compute the term to be added. 
The presnse of the common pattern is a strong sign that it could be abstracted.
```python
def sum(n, term):
	total, k = 0, 1
	while k <= n:
		total = total + term(k)
		k = k+1
	return total

def natural(x):
	return x

def cube(x):
	return x*x*x

def sum_natural(n):
	return sum(n, natural)

def sum_cube(n):
	return sum(n, cube)
```

## 1.6.2 Functions as General Methods
> [video](https://www.youtube.com/embed/71Vp90zsSds?rel=0&showinfo=0&enablejsapi=1)

## 1.6.3 Functions - Nested Definitions

## 1.6.4 Functions as Returned Values
> [video](https://www.youtube.com/embed/Q9ztlG4ezVs?rel=0&showinfo=0&enablejsapi=1)

## 1.6.5 Newton's Method
> [video](https://www.youtube.com/embed/zJlcbEOw1VU?rel=0&showinfo=0&enablejsapi=1)

> [video2](https://www.youtube.com/embed/OtNBPOKpB30?rel=0&showinfo=0&enablejsapi=1)

## 1.6.6 Currying
> [video](https://www.youtube.com/embed/6HMa5hfhRVc?rel=0&showinfo=0&enablejsapi=1)

## 1.6.7 Lambda Expressions
> [video](https://www.youtube.com/embed/vCeNq_P3akI?rel=0&showinfo=0&enablejsapi=1)

## 1.6.8 Abstractions and First-class functions
> [video](https://www.youtube.com/embed/bi_2gAetCiI?rel=0&showinfo=0&enablejsapi=1)

## 1.6.9 Function Decorators
> [video](https://www.youtube.com/embed/th_SlHfhlBo?rel=0&showinfo=0&enablejsapi=1)

[[composing-1.7 Recursive Functions]]
back to [[Composing Programs Index]]