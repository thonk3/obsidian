So far the app is retrieving and displaying fake data.

refactoring `HeroesComponent` focuses on supporting the view and making it easier to **unit test with a mock service**

## Why Use Services

Components should not fetch / save data directly.
They should focus on presenting data and delegate access to a service

> This tutorial creates `HeroService` that all application class that can use to get heroes.
> We are not creating service with the `new` keyword.
>
> This service use the `dependency injection` that ang supports to inject it into the `HeroesComponent` constructor

Services are a great way to share info among classes that don't know each other.
Creates a `MessageService` next and inject in in these two places
- Inject in `HeroService` which uses the service to send a message
- Inject in `MessageComponent`, which  displays that message, and also display the ID when the user click a hero

> Lots of text

---

## Create the HeroService

run to create a service called `hero`, this generates a skeleton class in `src/app/hero.services.ts`
```
ng generate service hero
```

### `@Injectable` service

the new service `Injectable`.
This marks the class as one that participate in the DI system,
The `HeroService` class is going to provide an injectable service, it can also have its own injected dependencies.

`@Injectable()` decorator accepts a metadata object for the service similar to the other decorators in the component class

### Get the hero data

The `HeroService` can get data from anywhere.

For now we are still using the mock data

- add the `Hero` type and mock-hero data

---

## Provide the HeroService

new we make the `HeroService` available to the DI system before ang can inject into `HeroComponent`
We do this by **registering a provider** which can creates / deliver a service.

In this case it instantiates the `HeroService` class to provide to the service.

We register the `HeroService` with the injector.
The Injector is the object that chooses and injects the provider, where the app requires it

by default `ng generate service` register a provider with the root injector for your services via the meta data

When services are provided at the root level,
NG creates a single, shared instance of `HeroServie` and injects into any class that asks for it.
Registering the provider in the `@Injectable` metadata also allows NG to optimize an app by removing the services if its not used

---

## Update the HeroesComponent

- delete HEROES import and now change to import the `HeroService`
- injects the `HeroService` as a parameter to the constructor of `HeroComponent`
- when NG creates the `HeroComponent`, the DI system sets the `heroService` parameter to the singleton instance of `HeroService`
- creates a method to retrieve the heroes from the service
- call the `getHeroesFromService()` in `ngOnInit()`
  - while its possible to call the func in constructor, its bad practice
  - reserve constructor for minimal initialization such as wiring const params to props
  - it shouldnt call any function that makes HTTP request to remote servers

---

## Observable data

> Here comes the pain `RxJs` - `Observables` 

later on in `pt6-HTTP` you can see how Angular `HttpClient` method returns RxJs `Observables`.
This tutorial simulates RxJs `of()` function

in `HeroService`
- so import the `of()` function from RxJs
- `of(HEROES)` returns an `Observable<Hero[]>` that emits a single value (the mock array)

### Subscribe in `HeroesComponent`

so now as the `heroService.getHeroes()` function now return an Observable instead of `Hero[]`
The `HeroesComponent` needs change to use the observable

The big difference is `Observable.subscribe()`

- previous version assignment occurs synchronously, as if the server could return heroes instantly or the browser could freeze the UI while it waits for a response
- the new version (`observables`) wait for it to emit the array of heroes which can happen anytime in the future.
- `subscribe()` method passes the emitted array to the callback. that sets the `heroes` prop
- this **asynchronous** approach works when the `HeroService` request heroes from the server

---

## Show Messages

This guides
- adding `MessageComponent` that displays application message at the bottom of the screen
- creating injectable, application wide `MessageService` for sending message to be displayed
- injecting `MessageService` into `HeroService`
- displaying message when `HeroService` fetches heroes successfully

## Add messages to hero service

- create the component `MessageComponent`
- add the component into the main `AppComponent`
- create the service `MessageService`
- injects `MessageService` into `HeroService`
- edit `getHeroes()` to also send message from `HeroService`

Now displaying the message from HeroService
- `MessageComponent` should display all message all messages sent by `HeroService`
- now import `MessageService` into `MessageComponent`
- injects is as a `public`  prop because it is bind in the template
- now binds the MessageComponent template

> Angular only binds to `public` components

now you can mess around with in `HeroComponent` to add more logging messages

---

## Summary

- refactored data access to `HeroService` calss
- registered `HeroService` as the provider of its service at the root level so it can be injected anywhere
- used angular DI
- gave `HeroService` `get data` method an async signature
- first look at `Observables`
- created `MessageService` for loosely coupled communication between classes