
> [!Note] source
> https://dzone.com/articles/angular-app-state-management-with-ngrx

## What
- state management library
- redux implemnetation for angular
- wr first look at the problem its solving
- then understand the concepts behing NgRx

## Application State
- Theoretically, this is the entire memory of the app
- But typically its
	- data from api calls
	- user inputs
	- presentation ui state
	- app references
> Its the data that differentiate the difference between 2 states of the application

## Problem this solve

Assume the case theres a list of customers in the app, and ==this is the state we're trying to manage==
Some API calls and user inputs can change the customer state (adding / removing)

The changes should then be ==reflected in the UI and other dependent components==

So in this case we can
- hold a golbal variable to hold the list 
- add/remove customers from/to it
- write code to update the UI dependencies

> NgRx is a great design for most state management requirements.

## NgRx State Management
lets look at its components:
- `store` - holding the application's state
- `action` - unique event dispatched from components and services, that describes how the state should be changed. (*addcustomer* can be an action that change the state)
- `reducer` - all state changes happens within the reducer, 
	- it responds to the dispatch action
	- basing on the action, will create a new immutable state and return it to the store
- `selector` - functions used for obtaining parts of the store
- `effect` - mechanism that listens to dispatched actioons in an observable stream, process the server's response, return new actions either immedietly or asyncronously to the reducer to change the state. (not using in this app)

![[slide1.jpg]]
The UI and other components ==dispatches== the action.
Actions can have payloads that is used to change the state.

The reducere creates a new state as described by the (dispatched) action and returns it to the store.
When the store is ==updated with the new state==, it notifies the UI and all dependant components.
Each components reacts to the state change and will update to reflect the change.
![[final.gif]]

The "Add New Customer" ui control **dispatches** the AddCustomer action with the new customer as the payload for that action.

The reducer takes AddCustomer action and create the new customer comes as a payload and create a new immutable action with the existing customer
It will then update the store with the new customer list.
Finally itll notify the UI using Observables and the UI is updated with the customer list

---

## Code Time

### Prereq
- nodejs
- angular cli

### 1. Create ang app via the cli
standard app

### 2. Install NgRx and tools
ng add @ngrx/store
ng add @ngrx/store-devtools

> what are they doing with schematic

### 3. Setup
####  Add NgRx store to app
> See what this does and try to do it without the CLI

what is this nonsense 
```shell
ng generate @ngrx/schematics:store State --root --module app.module.ts
```

#### Create submodule for Customer
Create separat module for customer 
```shell
ng g module customer
```

####  Create Customer model
create model class for Customer
```shell
ng g class model/customer
```
```ts
export class Customer {
	name: string = '';
}
```

### 7. Add actions
starting to add NgRx related code
The state were managing ins the ==collection of customers==
And the collection's state can be changed using the actions

> the fuck this can be generated via cli too
> select No for failture state
```shell
ng g action customer/store/action/Customer
```

### 8. Add Reducer
All state changes ocur within the reducers based on dispatched Action
The reducer does not mutate the current state
It will create a new state tree and set the current store instead

> failure actions > no
> use create functions > yes
```shell
ng g reducer customer/store/reducer/customer
```

### 9. Add Selector
generate selector to grab the collection from the Store
```shell
ng g selector customer/store/selector/Customer
```

### 10. Add UI component for View Customers
UI component is we/ ill just copy paste

### 11. Add UI Controls to add New Customers

### 12. Add StoreModule for feature in customer module
> notsure what it is
> Feels like a submodule thing




### 13. Import CustomerModule in AppModule

### 14. Update AppComponent with CustomerView and CustomerAdd Component 

### 15. Run 

---

## Takeaway
#review on what is happening
