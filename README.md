
## PROJECT TITLE

Blog SPA (demo) - for testing competency of candidates


## PROJECT DESCRIPTION

A simple, single page application, that will implement the core technologies of our current application stack, made up by the following components:

- `<blog-app>`
- `<blog-card>`
- `<blog-entry>`

### Blog App
The main element: `<blog-app>`, will be embedded directly into the landing page: `index.html`. Pseudo code:

```
<!-- index.html -->

<blog-app></blog-app>
<script type="module" src="src/dist/blog-app.js">

```
This custom element will host and showcase a list of 20 card widgets (`<blog-card>`). Cards will use the same reusable custom element (extending LitElement), showcasing a title and date - data is passed via a property<sup>[1](#myfootnote1)</sup> from the parent to the card and rendered using a loop:

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
	- Web Components base class for creating and rendering into the Shadow DOM of our own Custom Elements

• Typescript
	- For typing element methods and compiling Javascript to the latest spec when its the case

• Redux
	- For storing and accessing mock data for the list of cards and the eindividual blog entry element

• Pwa-helpers
	- `router.js` for handling navigation between pages
	- `connect-mixin.js` for connecting our Custom Element to the Redux store

• Snowpack
	- Bundling project dependencies only! Ie: LitElement, Redux.


-----------------

## HOSTING:

We recommend Glitch or any other web based solution for hosting, that's powered by a Node.js and capable of serving this single page application.

## Footnotes

<a name="myfootnote1">1</a>: See chapter on binding properties to template properties:<br>
https://lit-element.polymer-project.org/guide/templates#bind-properties-to-templated-elements

<a name="myfootnote2">2</a>: See chapter on binding properties to template properties:
https://lit-element.polymer-project.org/guide/templates#bind-properties-to-templated-elements





