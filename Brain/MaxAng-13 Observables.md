## Intro

What are observables
- think of it as a data source
- following the [[Observer pattern]]
- Represented as a stream
- emits data packages on the stream as the user interacts with the application

What are Observers
- handle data packages within the observable stream
- there are 3 ways to handle the data packages
	- handle data
	- handle error
	- handle stream ends / completion

### Install RxJs

This course examples use the following rxjs packages
```
npm i --save rxjs@6
npm i --save rxjs-compat
```

## Angular Observables
- note on routing content (syntax abit weird)
- Observables are constructs to which you subscribe to be informed about changes in data.
- When a new data piece is emitted, the subscription will know about it

## The core of Observables
- lets build one in `HomeComponent`
- Observables are implemented via the package `rxjs`

### Building a custom Observable

### Errors & Completion

### OK but why Observable
- Rarely you will build your own observables
- most of the time, you will interact with pre-built observables for your application

## Understanding Operators
The magic feature of `RxJs` are the `operators` which 

> [!Notes] most of this notes is written within the 

## Subjects



## Summary

---

