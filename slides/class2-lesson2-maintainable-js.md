# Modules

@todo: use object oriented code examples for modules

ECMAScript 2015 ("ES6") adds modules as a native feature to JavaScript, meaning we can organize our code into separate script files and the browser will automatically run them in the order we need.

## Define the problem

## Code organization benefits

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

It's getting pretty long! If we want to find and update the hideTooltip() function then we're slogging through lots of other features to do so. 

If we could split this file up by feature it'd be a lot easier to update and maintain:

* product.js
* petProduct.js
* catFood.js
* doggySweater.js

but then we'd have to load 3 separate files in our index.html:

```html
<script src="product.js"></script>
<script src="petProduct.js"></script>
<script src="catFood.js"></script>
<script src="doggySweater.js"></script>
```

What's wrong with this? 

performance, maintenance again (you have to go edit your html to add new modules), dependencies (loading code in the correct order).

## JavaScript Modules
Unlike other programming languages JavaScipt did not let you separate files and import them into other JS files natively - until ES6/ES2015. 

Browsers don't yet support native JS modules.

@todo explain global scope problems with this code and the hax we did to get around it - module loaders like require.js, IIFE

```javascript
function Product(name, category, price) {
  this.name = name;
  this.category = category;
  this.price = price;
}

Product.prototype.addToCart = function(quantity) {
  var plurality = '';
  if (quantity > 1) {
    plurality = 's';
  }
  var message = 'You added ' + quantity + ' ' + this.name + plurality + ' to your cart.';
  console.log(message);
  document.write('<h1>' + message + '</h1>');
}

export Product;
```

### Code organization wishlist:

* we'd load one JS file for performance purposes
* we'd have multiple module files for development purposes
* we'd be able to load modules as needed for when code is dependent on another file

## CommonJS and Node

CommonJS is a module format that lets you export and import code between separate files. 

A build tool (for example Gulp, Grunt, and webpack) is used to compile your site's JS file.


### Import & Export



## Setup exercise files

@todo: windows???

1. [Install Node.js](https://nodejs.org/en/)
1. Open terminal/command line
1. Run `npm install` from the class2 folder
1. Run `npm run build`
1. Run server: `python -m SimpleHTTPServer`
1. Go to [http://localhost:8080](http://localhost:8080) in browser

#### Exercise 7
## Organize your OOJS code

1. Organize the code from `mySite.js` into separate files inside the `class2/js/` folder.
1. Update the module.exports object in each module to export your functions.
1. Import your dependencies into app.js using the `require` statement.
1. Create new instances of your prototype objects in app.js, referencing your imported modules.


### More about modules

[Require.js](http://requirejs.org/) uses the [AMD module](http://wiki.commonjs.org/wiki/Modules/AsynchronousDefinition) format and does not need a build step, as it runs solely in the browser.

## Test-Driven Development


First, write your test case that defines what will happen based on user behavior or interaction.

For example:

* "when I click the submit button, an alert function is triggered."
* "when I click the submit button, an alert function is triggered."


## Unit tests
* define it
* run it!
* make it break!
* code example of function that makes it pass

## Group Exercise

Use your unit test template to make your first test (which should fail).

Write the function to make the test pass.

## JS Assessment

Setup JS Assessment locally:

1. In Terminal navigate to the `class2/js-assessment` folder
2. Run `npm start`
3. Go to http://localhost:4444/ in your browser
4. Open 'app' folder inside our class files in Sublime Text.

#### Exercise 8
## JS Assessment

Write the following JS Assessment functions so that they pass their corresponding tests:

1. arrays.js
2. flowControl.js

#### Exercise 9
## PetProduct Unit Test

Edit `class2/test/petClothing.js` so that it has the following new tests:

1. `petClothing.prototype` should have a property named `tryOnClothing`
1. `tryOnClothing` property `typeof` should be a function
1. `tryOnClothing` method expects an argument that is an object
1. `tryOnClothing` method returns a message of "Fluffy tried on the Umbrella Hat for Cats and looks amazing in it."

Refactor the `petProduct.js` module so that is passes the unit tests, one test at a time.
