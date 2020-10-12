
## PROJECT TITLE

Blog SPA (demo) - for testing competency of candidates


## PROJECT DESCRIPTION

A simple, single page application, that will implement the core technologies of our current application stack, made up by the following components:

- `<blog-app>`
- `<blog-card>`
- `<blog-entry>`

All of these components will extend LitElement - a simple base class for creating fast, lightweight web components.

### Blog App
The main element: `<blog-app>`, will be embedded directly into the landing page: `index.html`. Pseudo code:

```
<!-- index.html -->

<blog-app></blog-app>
<script type="module" src="src/dist/blog-app.js">

```
This element will host and showcase a list of 20 cards (`<blog-card>`). A card is a reusable element (widget) and will display a title and the date of a blog post it represents.

Data is hold in the Redux store and accessed by the main element using the callback: `stateChanged()` (see PWA-helpers and the `connect-mixin.js` mixin in dependencies).

This data is then passed via a property<sup>[1](#myfootnote1)</sup> from the parent to the card, and rendered<sup>[2](#myfootnote2)</sup> using a loop:

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

When clicking a card, the user should be "brought" (making this element visible while hiding the rest) to the actual `blog-entry` element, showcasing the title, date and the full bodytext of the blog post. 

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
    //Hint: We can obtain the idx of the current blog post from the url like:
    const path = decodeURIComponent(location.pathname);
    const splitPath = (path || '').slice(1).split('/');
  
    const idxOfCurrentBlogPost = splitPath[1];
    this.blogEntry = state.items[idxOfCurrentBlogPost];
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

<a name="myfootnote2">2</a>: See chapter defining and rendering templates using LitElement:<br>
https://lit-element.polymer-project.org/guide/templates#define-and-render-a-template





