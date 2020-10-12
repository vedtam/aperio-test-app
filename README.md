
## PROJECT TITLE

Blog SPA (demo) - for testing competency of candidates


## PROJECT DESCRIPTION

A simple, single page application, that will implement the core technologies of our current application stack, made up by the following components:

- `<blog-app>`
- `<blog-card>`
- `<blog-entry>`

### Blog App
The main element will be embedded directly into `index.html`. Pseudo code:

```
<!-- index.html -->

<blog-app></blog-app>
<script type="module" src="src/dist/blog-app.js">

```
This custom element will host and showcase a list of 20 cards (`<blog-card>`). Cards will use the same, reusable custom element (extending LitElement), showcasing a title and date - data is passed via a property from the host (blog-app) to the card element and sit inside a loop:

```
//blog-app.js

...

@property({type: Array})
items: any[] = [];

render() {
   return html`
     ${this.items.map((item, idx) => html`
	<a href="/blog-entry/${idx}">
	  <blog-card .data="${item}"></blog-card>
	</a>
    `)}
}

stateChanged(state) {
    this.items = state.items;
}
...
```

When clicking a card, the user should be brought to the actual blog entry element, showcasing the title, date and the full bodytext of the blog post:

```
//blog-entry.js

...

@property({type: Object})
blogEntry?: any;

render() {
  return html`
    <h2>${this.blogEntry?.title}</2>
	<h5>${this.blogEntry?.date}</5>

	<main>${this.blogEntry?.bodytext}</main>
   `)}
}

stateChanged(state) {
    this.blogEntry = state.items[3];
}

...

```

-----------------

## DEPENDENCIES:

• Lit-Element
	- Web Components base class for creating and rendering into the Shadow DOM of our Custom Elements

• Typescript
	- For typing in element methods and compiling Javascript to the latest spec

• Redux (optional)
	- For storing and accessing mock data for the list of cards and the eindividual blog entry element (page)

• Pwa-helpers
	- `router.js` for handling navigation between pages
	- `connect-mixin.js` (optional) for connecting our Custom Element to the Redux store

• Snowpack
	- Bundling project dependencies only! Ie: LitElement, Redux.


-----------------

## HOSTING:

We recommend Glitch or any other web based solution for hosting, that's powered by a Node.js and capable of serving this single page application.







