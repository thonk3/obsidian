
> [!NOTE] How to use this chapter
> This is a tour of Angular DI systems and concepts
> Find more of the code in [DI-r73 demo](https://github.com/AshayKing/ng-book2-book-angular-7-r73.git)
> The code is heavily deprecated
> Just read through it 
> Code is dead 

When your app will eventually grow bigger and bigger.
Different parts of the app will need to communicate with other modules.

When module `A` requires `B` to run. `B` is a dependency of `A`
		The most common way to get access to dependencies is to import a file.

Sometimes, we may need more ==sophisticated== ways to provide dependencies:
- Substitute out the implementation of `B` for `mockB` during testing
- share a single `instance` of `B` class across the whole app ([[Singleton Design Pattern]])
- create a `new` instance of `B` class everytime its used ([[Factory Design Pattern]])

> [!INFO]
> Dependency Injection(DI) is a system to make parts of our program accessible to other parts of the program, and we have controll of how it happens

> [!hint]
> one way to think about the `injector` is as a replacement for the `new` operator.
> Instead of using the language-provided `new` operatorm DI lets us configured how objects are created

Main benefit of DI is the client component does not need to know of how to create the dependencies.
All it needs to do is know how to interact with those dependencies.

## Injection Examples

> Looking at the demp app

Imagine we have a store that has `Products` and we need to calculate the final price of that product *after sales tax*.
To do this we use a `PriceService` to that takes as args
- *base price* of the `Product`
- the *state* it is sold to
Then return the final `Product` price + tax

> See `price.service.1.ts`
> for the above function `calculateTotalPrice()`

say we want to use this service on `Product`

> See product.model.1.ts

If we would write a test for this it may look like
```ts
import { Product } from './product'

describe('Product', () => {
	let prod;
	beforeEach(() => {
		prod = new Product(11);
	})

	describe('price', () => {
		it('is calculated based on base price and state', () => {
			expect(prod.totalPrice('Fl')).toBe(11.66);
		})
	})
})
```

The problem with this is we cant/set the tax value in `FL` to unit test.
Even if `PriceService` was implemented the realway, calling an api, there is still the issue of
- API needs to be available (db needs to be running)
- We need to know the exact florida tax at the time the test is ran

So to effectively test the `price` method of `Product` without external resource.
One way is to mock the `PriceService`

If there exist an interface of `PriceService` we can write `MockPriceService` to always give a predictale calculation

```ts
// price-service.interface.ts
export interface IPriceService {
	calculateTotalPrice(base: number, state: string): number;
}
```
now to write the mock service to test
> see price.service.mock.ts

Then modify the product class to use the service
> see product.model.1.ts
> to product.model.ts
> change to implement the interface instead

So now, the client using `Product` becomes ==responsible for deciding which concrete implementatin of PriceService is going to be given to the new instance==

With this, we can tweak the test to get rid of the unpredictability previously

```ts
import { Product } from './product'
import { MockPriceService } from './price.service.mock'

describe('Product', () => {
	let prod;
	beforeEach(() => {
		const service = new MockPriceService()
		prod = new Product(service, 11);
	})

	describe('price', () => {
		it('is calculated based on base price and state', () => {
			expect(prod.totalPrice('Fl')).toBe(11.66);
		})
	})
})
```
> check `product.model.ts

At the moment, its still abit laborious to pass an istance of the service for every `Product` instance

Ang DI can aveliate this, instead of a new instance of the class, it can
- register the `dependency`
- describe how the `dependency` is `injected`
==> DI

> [!INFO] a benefit of this
> is the dependency implementation can be swapped at run-time
> We can freely configured how the ==dependecy is created==

This is often the case of ==application wide services==
it may only need one instance - [[Singleton Design Pattern]]

Another case for DI is to for configs/ env specific variables.
- we might define a const `API_URL`, but then injenct a different value in prod vs dev

Lets learn how to create services and different method of injections

---
## DI components
To register a dependency, it needs to ==be binded== to something that will ==identify its dependency==.
The Identification is called the ==dependency token==.

> [!NOTE] Example
> to register an API URL, can use the string `API_URL` as the token.
> similarly, if we're registering a class, we can use the class itself as its `token`  which will be shown below

DI in angular consist of 3 parts
- `Provider` - (or binding) maps a `token` (string or class) to a list of dependencies, it tells Ang how to create the object / give a token
- `Injector` - holds a set of bindings, responsible for resolving dependencies, injecting dependencies when creating objects
- `Dependency` - what is being injected

![[Pasted image 20230208200916.png]]

A way for thinking about this is
When we configured DI, we specify what is being injected and how its being resolved

---
## Playing with an Injector

#todo p222

## Providing dependencies

## Providers are the key

## Providers

### using a class

### Using a value

### Configurable Services

### Using a factory

### factory dependencies

---
# DI in apps

# More Resources

---

Up next [[ng-book 2 http]]



