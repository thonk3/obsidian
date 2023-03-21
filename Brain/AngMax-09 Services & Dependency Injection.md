
Business logic unit which can be used by other components of the Agular application

## Logging Service
Builing a logging services

- A serice is just a normal ts class

While it is possible to directly import this class into each individual components.
It is not ideal to manually creating a new instance of that class with in components

> This is when we use Dependency Injection to handle service classes

## Injecting Service Into Component

Depenency - the something a class depends on 
Dependency Injector - injects an instance of this class into the component automatically

This is done via setting arguments in your component constructors
This declares what objects the component "Depends" on to create
```ts
class Component {
	constructor(private loggingService : LoggingService) {}
}
```
Now we only know what this component wants
It does not yet know how this service instance is provided for the component

We need to **provide** an instance / telling Angular
This is done via the `provider` property within the `@Component` decorator 
We only need to provide tht type

## Data Service
A type of service to store and manage our data

Go ahead and create the `AccountService` then rewrite all 3 components to use it

## Understanding Heirachical Injector
Something regarding DI heirachical tree
#review - this part video

The reason why the service was not functioning
In each of the components, we are providing a new instance of the service

To ensure the same instance is passed in to all child components
Pass only set the service as provider for the parents component

## Injecting Services Into Services
samething as components but you need to decorate your service classes with `@Injectable()i`


## Using Service for Cross Component Communication
Let illustrate this by, let say if we want to output something in `NewAccount` component
when the buttons in `Account` is clicked


## Different way of Injection


---

## Practice Services

Fairly Straight forward
#todo Something fun todo is to refactor everything to use class

#todo continue with regular course content but lets just start with Observables for now


