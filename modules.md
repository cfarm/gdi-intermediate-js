# Modules

ECMAScript 2015 ("ES6") adds modules as a native feature to JavaScript, meaning we can organize our code into separate script files and the browser will automatically run them in the order we need.

## Define the problem

### Code organization benefits

you have some code:


`mysite.js`

it has the following functions

```javascript
function showNavMenu() {
    ...
}

function hideNavMenu() {
    ...
}

function showInstantSearchResults() {
    ...
}

function hideInstantSearchResults() {
    ...
}

function showTooltip() {
    ...
}

function hideTooltip() {
    ...
}

// call all the things
showNavMenu();
hideNavMenu();
showInstantSearchResults();
hideInstantSearchResults();
showTooltip();
hideTooltip();
```

It's getting pretty long! If we want to find and update the hideTooltip() function then we're slogging through lots of other features to do so. If we could split this file up by feature it'd be a lot easier to update and maintain:

navMenu.js
instantSearchResults.js
tooltip.js

but then we'd have to load 3 separate files in our index.html:

```html
<script src="navMenu.js" />
<script src="instantSearchResults.js" />
<script src="tooltip.js" />
```

What's wrong with this? performance, maintenance again (you have to go edit your html to add new modules), dependencies (loading code in the correct order).

Unlike other programming languages JavaScipt did not let you separate files and import them into other JS files natively - until ES6. 

@todo explain global scope problems with this code and the hax we did to get around it - module loaders like require.js, IIFE

## Modules example

navMenu.js:

```javascript
function showNavMenu() {
    ...
}

function hideNavMenu() {
    ...
}

export showNavMenu;
export hideNavMenu;

```

COOL NOTES from https://leanpub.com/understandinges6/read#leanpub-auto-modules

"
1. Module code automatically runs in strict mode and there’s no way to opt-out of strict mode.
2. Variables created in the top level of a module are not automatically added to the shared global scope. They exist only within the top-level scope of the module.
3. The value of this in the top level of a module is undefined.
4. Modules do not allow HTML-style comments within the code (a leftover feature from the early browser days).
5. Modules must export anything that should be available to code outside of the module.
"

... "Any variables, functions, or classes that are not explicitly exported remain private to the module" 
we cannot call showNavMenu from other javascript files or our index.html page unless we explicitly export it.


### Import & Export


### Dependencies
app.js ties it all together. If you've ever used a framework, require.js, AMD or Common.js modules then you're familiar with this concept of code organization.

## Modules exercise


## Browser Support

Because ES6 is still new and being implemented by browser makers, most modern browsers do not support all features including modules. So how do we make sure our ES6 code is run properly in current browsers?

### Transpilers

We have to use **transpilers** to convert our code from ES6 syntax to the previous version of JavaScript so that browsers can run our JS.

>> How to goes here >>