
CSS is a cascade of globals with varying degrees of specificity, which can easily become a nightmare to manage without some fore-thought about how you go about writing your CSS.

This document outlines goals and guiding principles for architecting CSS to scale and remain maintainable in component-based systems, e.g. React, Angular, Ember


### Goals

The ability to write css in a predictable and maintainable fashion that ensures the lowest level of specificity while still remaining modular and scalable.

* Maintainability
	* Styles should be written semantically, with the lowest specificity possible and should be architected with the spirit of ITCSS.
* Modular
	* Styles are component-based and follow a naming convention that is suited for component-based architecture.	 
* Scalable
	* We do not resort to using a crutch in order to trump specificity, i.e. `!important` or `.my-class.my-class`, etc

### Guiding Principles

**Maintainability** | 
**Modularity** | 
**Scalablility**

* DRY until it makes sense, don't be afraid to duplicate css code.  CSS is unique in that the context in which a style is applied can change based on state, viewport size and specificity.  Too many utilitarian classes (e.g. `pull-left`) increases the amount of css classes, can cause bloat and makes a component-based architecture less predictable. 
* Semantics!  Name something based on what it is, not how it looks or behaves.
	* Use multiple classes to style.  As opposed to a single class built using @extend that builds on other classes.
	* Use a convention for structuring component classes.  e.g. BEM, SMACSS, OOCSS, ITSCSS, SUIT, etc, etc.	
	* Component-based classes
	 * Avoid type selectors, e.g. `item-list a { ... } // bad`
* All styles must have a prefix, e.g. `.monkey-list`, `.monkey-grid`
* Selector nesting should not be anymore than 3 levels deep.
	* e.g. `.monkey-list .monkey-list__item .monkey-list__item-description .btn { ... } // bad` 
* Use `js-` prefixes for javascript and test automation hooks.
* Use ID's when you need to anchor something, not as a style hook.
* Chose a framework like SMACSS, BEM, OOCSS, etc and stick to it.  It honestly doesn't matter how you decide to abstract components, but I've found BEM to work pretty well.

Example:

```
/* Component */
.user-list {
	/* States */
	&--active {
	}
	&--disabled {
	}
}
/* Component part */
.user-list__item {
}
```

#### Folder Structure

The guiding principals of maintainability, modularity and scalability are imbedded in how files are laid out.  This folder structure is inspired by Harry Robert's ITCSS.

* Config – Color, typography, global variables
* Tools – globally used mixins and functions. It’s important not to output any CSS in the first 2 layers.
* Base – reset and/or normalize styles, box-sizing definition, etc. This is the first layer which generates actual CSS.
* Elements – styling for bare HTML elements (like H1, A, etc.). These come with default styling from the browser so we can redefine them here.
* Structure – styling for pages, container components or anything else that pertains to structure.
* Components – specific UI components. This is where majority of our work takes place and our UI components are often composed of Objects and Components
* Overrides – utilities and helper classes with ability to override anything which goes before in the triangle, eg. hide helper class

### Performance / Optimizations

* Compare the size of files after HTTP compression!

### References / Inspiration

* http://maintainablecss.com/
* http://csswizardry.com/2016/02/mixins-better-for-performance/
* https://medium.com/peergrade-io/structuring-css-in-large-projects-37f1695f5ec8#.8lwys1kup
* http://nicolasgallagher.com/about-html-semantics-front-end-architecture/