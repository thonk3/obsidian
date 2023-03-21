
# Expanding the Application
before continuing with the application, lets review the app and break it down into its logical component

So the app will consist of two main components
1. `Application` the overal application, containing the form used to submit new articles
2. `Article` each individual article and links

> In larger apps, the form would probably become its own component.
> For simplicity, we will only use two component to make data passing between components easier

OK lets create the app `angular-reddit`

## Adding CSS
bait to buy source code
The guide is using semantic UI so maybe [I can install it myself]([Getting Started | Semantic UI (semantic-ui.com)](https://semantic-ui.com/introduction/getting-started.html#install-nodejs))
> [How to use Semantic UI in your Angular app (Of course it's possible) | Daniel Kreider](https://danielk.tech/home/how-to-add-semantic-ui-components-to-your-angular-app-without-getting-frustrated)
## The Application Component
We starting with building the `Application` component that will
1. store the current list of articles
2. hold the form for submitting new articles

> we will use the root `app` component for this 

- guide go through creating the form template

## Adding Interaction
The form so far is only using plain html elements and does not contain any  interaction logic yet.
Now we will add a `<button>` with an `onClick` event listener that will call a function when the user clicks it

> we use the Event binding syntax ()

> They are currently using reference for this form, to pass values from the input elements to the onclick function

```html
<form class="ui large form segment">
  <h3 class="ui header">Add a Link</h3>

  <div class="field">
    <label for="title">Title: </label>
    <input type="text" name="title" id="title" #newTitle>
  </div>

  <div class="field">
    <label for="Link">Link: </label>
    <input type="text" name="link" id="link" #newLink>
  </div>

  <button
    class="ui positive right button"
    (click)="addArticle(newTitle, newLink)">
    Submit Link
  </button>
</form>
```

OK so the input tags we use `#` reference to tell ang to assign to task to a local var???????????
We can then pass them as variables to the onclick function `addArticle()`

In this part we've made 4 changes
1. created button tag
2. created `addArticle()` and bind it to the `(click)` event
3. added attributes to the input tag to pass its value to the `addArticle()` function
> The following sections cover these steps in reverse order

### Binding `input` to values
```html
<input name="title" #nameTitle>
```

The markup tells ang to bind `<input>` to the variable `newTitle`
this syntax '#newTitle' is called a `resolve`
This makes the var `newTitle` available to other expressions within this view

`newTitle` is now an `object` that represents this `input` DOM element (`HTMLInputElement` type)
And we can retrieve the value using `newTitle.value`

### Binding actions to events
> event binding you know this #skip page73

### Defining the Action Logic
> defining the onclick function #skip page 74

## Adding the Article Component
 
#todo - continue the tutorial pg75
OK now, we have a form, but is not adding anything to the Article List

Now we will create the `Article` component to represent the individual submitted articles

```shell
ng g c article
```
there is 3 parts to define this new cmponent
1. define the component view in the ==template==
2. define the properties by annotating the class with `@Component` directive
3. define component-definition class containing our logic
 
### Creating `ArticleComponent` template
#skip page 77 explaining the html template
explaining angular data interpolation

### Creating `ArticleComponent`
#skip pg78 explaining `@Component` directive metadata
#skip pg79 walking through the class definition

The only nonstandard thing I see is 
```ts
@HostBinding('attr.class') cssClass='row';
// css class we want to apply to the "host" of this component
```
A Component Host is the element this component is attatched to. 
> do they mean the parent?

We can set props on the host element by using `@HostBinding`
In this case, we are asking angular to keep the value of the host element class to be in sync with the prop `cssClass`

> oh so this is attatching `class="row"` to `<app-article>` 
#TODO What is `HostBinding`


### Using `ArticleComponent`
Now lets reference this into the root `app` component

#skip pg82 talk through declaring the component in NgModule

#### Re Upvote-Downvote buttongThe upvote or downvote button
```html
<a href...></a>
```
will cause the page to reload instead of updating the list

By default, Js ==propages the click event to all parent components==
Because og that, the browser would try to follow the emptylink, telling the browser to reload

> to fix, make the event handler function to return false.
> hence the browser wont refresh the page
> 
> Oh seems like a default a onclick functionality

---
# Rendering multiple rows
Right now its only displaying a single article
To make ang display more
A good practice is to create a data structure representing an `Article

> this is a plain js task and not an angular component
```ts
// src/app/article/article.model.ts
export class Article {
	title: string;
	link: string;
	votes: number;

	constructor(t:string, l:string, v?: number) {
		this.title = t;
		this.link = l;
		this.votes = v || 0;
	}
}
```
Now lets also update the `Article` component logic to use this instead

Everything is standard but
Its mentioning the code is still "off"
`voteUp()` and `voteDown()` ==breaks the encapsulation of the article class by changing the internal properties directly==

> Law of Demeter
> A given object should assume as little as possible about the structure or properties of other objectso

to fix this ==convention== issue. add the voteup vote down methods on the article class

> The Idea of this is the Article component should mutate data in the object
> This lets `Article` ecapsulate what functionality should happen to a model when voting happens

> In "real" apps, the internals of the model would be a lot more complicated
> - makes api request 
> Hence you would'nt want this sort of model-specific code in the component controller

### Storing Multiple articles
> #skip  p91 you know this, change to array collection
> use ngIf to render multiple elements
> passing article object to the article component

---
# Adding New Articles
> Simple implementation

Modify `addArticle` function to push a new `Article` object into the article list 


---
# Finishing Touches
#skip p97 not important, but fun to look through
## Displaying the Article Domain

## Sorting based on score


---
# Deployment

## Building our app for Production


## Uploading to a Server

## Installing `now`

#todo - continue the tutorial pg100

---


- wrapping up
might skip typescript section