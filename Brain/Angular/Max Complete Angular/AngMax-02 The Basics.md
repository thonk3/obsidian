> Info I already know but is important
> [How the angular App is Loaded and Started](https://www.udemy.com/course/the-complete-guide-to-angular-2/learn/lecture/6655700)

> This lesson is followed through with the git project [01_basics]()

`@NgModule` decorator metadata
- `bootstrap` array - list components that should be known to Ang at the point of reading Index html
- `declaration` array - list of registered components for ang to recognizes

## Angular Components
- `AppComponent` main root component

hes making a `app/server` component manually instead of the CLI
- `ng generate component server` would be ok
- `server.component.ts` exporting the `ServerComponent` class
	- `@Component` [[TS Declarator]]
		- `metadata` explanation
			- `selector` - html tag to refer the class
			- `templateUrl` - dir to the html template
	- [[TS Declarator]] are a TS feature that 'Enhances' your classess and more

### The Role of AppModule with component declaration

AppModule
- Angular uses components as building blocks of your place
- Uses Modules to bundle different pieces of your app
- For new components
	- Needs to be registered in the AppModule to angular to recognize its existance
	- Under `@NgModule` metadata
		- `declaration` add the new class component that was just created

### Components via the CLI
```bash
ng generate component <component>
## or
ng g c <component>
```
### Components Templates and Styling
- Can use Inline styling
- Can Use Inline HTML within the `@Component` declarator and in the `template` metadata string
- Plain Css styling is pretty basic

### Component Selectors
Regarding the `@Component` declarator, the `selector` metadata, there are many things you can do with it
- Use to mark the `html` tag reference by passsing a regular string
- Used to mark the selector as an `attribute` by encapsulating the string like `[app-selector]`
- Used to mark the selector as a `class` by prepend the string with a dot `.app-selector`

> Not sure when the different selectors are used, hence this is still trivial info

## Practice Components

Basic Practice on creating components
1. Create new Components `WarningAlert` and `SuccessAlert`
2. Output beneath eahh other in `AppComponent`
3. Output a warning or sucess message
4. Styling (optional)

### Components Solution
- Create components via CLI
- Output in AppComponent template
- Output message via string

---

## Understanding Data Binding

> Brief knowledge

- Databinding == Communication
- Communication between your TS Code (Logic) with the Template

Different ways of DataBinding
- Output data (One way Binding)
	- String Interpolation `{{ data }}`
	- Property Binding `[property]='data'`
- React to (User) Events (one way)
	- Event Binding `(event)='expression'`
- Combination of both (Two way  binding)
	- `[(ngModel)]="data"`

### String Interpolation
string interpolation conditions
- Can use terinary expression
- Any expression resolved to a string is ok
- Cannot use blocks (if / esle)
- Cannot use multiline expressions

### Property Binding
`[]` indicates propery binding
- dynamically bind a value to a property in DOM

### Events  Binding


