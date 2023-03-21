
## Key ideas 

- what makes a program functional
- general programming principals
	- DRY - dont repeat yourself
	- YAGNI - ya aint gonna need it
	- loose coupleing high cohesion
	- least suprise, single responsibility
- the point of all of these pricipals hold up in a functional setting
	- although only by coincidence to line up with the ultimate goal

## Brief encounter

> going through code sample

The main point to take a way 
- state and mutable values are hard to follow
try again with the functional approach
```js
const add = (x, y) => x+y;
const mult = (x, y) => x*y;

const flockA = 4;
const flockB = 2;
const flockC = 0;

add(multiply(flockB, add(flockA, flockC)), multiply(flockA, flockB));
// 16
```
ok so this is kind of still confusing to read because of the nesting
but it is some what better to follow 
essentially you could also simplify this using maths
```js
// original
add(multiply(flockB, add(flockA, flockC)), multiply(flockA, flockB));

// math view
//(b . (a + c(0))) + (a . b)
//(b.a) + (a.b)
// 2ab or b(a+a) / a(b+b)


// simplification
// a(b+b)
multiply(flockA, add(flockB, flockB))
```

## Takeaways
This will require some discipline but
We want to 
- represent the specific problem in terms of generic, composable parts 

---

next chapter [[magFP - 02 first class function]]



