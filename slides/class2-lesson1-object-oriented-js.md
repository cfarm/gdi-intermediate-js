# Object-oriented JavaScript
credit http://slidedeck.io/kpcs/Intro-to-Object-Oriented-JavaScript

What we'll cover:
* What is an object?
* What are attributes and methods?
* What is class-based inheritance?
* What is prototype-based inheritance?
* How do we create objects using inheritance in JavaScript?
* How can we extend a prototype in JavaScript?
* How do we write maintanable code?

## Warm up exercise

### Goal: Understanding objects

1. Create an object representing a product sold at an online pet store (using the [Codepen](http://codepen.io/pen/) website). For example, you could make a "petProduct" object with the properties "name," "category" and "price."

2. Use the push() method to add your product to an array that contains all the products in your online pet store.

3. Display your product on the page using [jQuery DOM manipulation](http://api.jquery.com/category/manipulation/) or native [JavaScript DOM insertion methods](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement).

## What is an object? 

An object can be a variable, function, or data structure.

```javascript
var petProduct = {
    name: 'Catnip',
    category: 'Plants that cats like',
    buy: function() {
        // Code that adds product to shopping cart
    },
    price: 5
};
```


## Uses for object-oriented programming

* Model physical concepts more clearly in your code
* Make your code easier to read
* Create code that is more easily maintainable and reusable


## Attributes and methods 

```javascript
var petProduct = {
    name: 'Catnip', // attribute
    category: 'Plants that cats like', // attribute
    buy: function() { // method
        // Code that adds product to shopping cart
    },
    price: 5 // attribute
};
```

When we talk about objects, we're interested in two main concepts:

* Attributes: object characteristics
* Methods: object functionality

## Group exercise: Shapes
Think about these geometric shapes:

circle, square, rectangle, star, rhombus, triangle

What are some attributes shared by all shapes?
What are some methods that can be applied to all shapes?
Are there any attributes or methods that are unique to only one shape? ... to some shapes?

## Class-based inheritance
Imagine going shopping for some cat food.

You go to the pet store with a concept of what "cat food" is.
You find a particular cat food brand with the qualities your vet told you to look for.
You purchase the tuna flavor of this brand because your cat loves tuna.
In object-oriented terms, we say that you have purchased an instance of the class of objects known as cat foods.

## Prototypal inheritance
Let's imagine another way of shopping for cat food.

You go to the pet store with an empty bag of cat food.
You ask the dealer for a new bag of the same cat food.
The brand, price, and flavor of the cat food are the same, but the bag is full and fresh.
You purchase this particular bag of cat food.
In object-oriented terms, we say that you have purchased an instance of cat food based off of a prototype, from which it inherited some attributes and methods.


## Creating new objects

In JavaScript, we use a constructor function to initialize new objects, and we use the **new** keyword to call the constructor.

```javascript
// Create a constructor function for new products
function PetProduct() {
    // Set attributes of all new products
    this.category = 'Cats';
}

var kittenProduct = new PetProduct();

// kittenProduct can access properties we defined in PetProduct
console.log(kittenProduct.category);    // 'Cats'
```
        
## Adding Arguments

```javascript
// Create a constructor function for new cars
function PetProduct(name, category, price) {
    // Set the given attributes of this object
    this.name = name;
    this.category = category;
    this.price = price;

    // Set attributes of all new cars, independent of arguments
    this.category = 'Cats';
}

var kittenProduct = new PetProduct('Catnip', 'Cats', 5);

// kittenProduct can access properties we defined in PetProduct
console.log(kittenProduct.category);    // 'Cats'
console.log(kittenProduct.name);        // 'Catnip'
```


## Extending the prototype
The prototype is the collection of all the attributes and methods that the object knows about.

The prototype property of an object is used primarily for inheritance: methods and attributes on a function's prototype property are available to instances of that function. 

The prototype can be considered the "original" object, from which "copies" (instances) inherit properties.

Inheritance = Access to the properties and methods created by the parent object(s).


## Extending the Prototype with new methods
```javascript
    function PetProduct() {
        this.inventory = 100;
    }

    // Extend the prototype to define methods for new PetProducts
    PetProduct.prototype.buy = function(quantity) {
        this.inventory = this.inventory - quantity;
    }

    // Instantiate a new PetProduct
    var kittenProduct = new PetProduct();

    // kittenProduct can access methods defined in the prototype
    console.log(kittenProduct.inventory);    // 100
    kittenProduct.buy(20);
    console.log(kittenProduct.inventory);    // 80
```

### Exercise: Creating objects

Beginning with this [CodePen template](http://codepen.io/cfarm/pen/grxYqv?editors=0010), make the following changes to the Product constructor:

1. Add arguments for name, category, and price
1. Add properties for name, category, and price
1. Create a method on the Product object called addToCart(). When that method is called, it should use console.log to output a string like "You added Kitten Mittens to your cart."
1. Instantiate a new Product object and call the addToCart() method on it.
1. Instantiate a second new Product object with different constructor arguments.
1. Bonus: Make the addToCart() method print your message to the HTML on the page using [jQuery DOM manipulation](http://api.jquery.com/category/manipulation/) or [JavaScript's document.write() method](https://developer.mozilla.org/en-US/docs/Web/API/Document/write).
1. Bonus: Make the addToCart() method accept a quantity to add to the shopping cart, and call it with different amounts.

[View the solution](http://codepen.io/cfarm/pen/BKdBMV?editors=0010)


## Extending the prototype with new objects

```javascript
// The constructor function
function PetClothing(name, category, price, size) {
    PetProduct.call(this, name, category, price);
    this.size = size;
}
// Extending the PetProduct object
PetClothing.prototype = Object.create(PetProduct.prototype);

// Instantiate a new PetClothing object
var doggySweater = new PetClothing('Doggy sweater', 'dog clothings', 30, 'medium');
```

Because it inherits from PetProduct, PetClothing has the properties and methods available to PetProduct as well.



```javascript
function MusicVideo(title, uploader, seconds, artist) { // includes all arguments from Video plus new arguments
  Video.call(this, title, uploader, seconds); // new
  this.artist = artist; // set property for artist
}

MusicVideo.prototype = new Video();
MusicVideo.constructor = MusicVideo;

```


## Beginning with this JSBin template, make the following changes:

1. Create a new object called PetProduct that extends Product. Its constructor should also take in an "inventory" argument.
2. Instantiate a new PetProduct object and call the addToCart() method on it.
3. Add a method to MusicVideo called addToWishlist() that uses console.log to output a string like "You added Umbrella Hat for Cats to your Wishlist!"

4. Bonus: Use an array of data and a for loop to instantiate 5 PetProduct objects.
5. Bonus: Make an array of product data with pet products and people products, loop through them, and decide on each one whether to make it a Product or PetProduct object.

1. Create a new object called MusicVideo that extends Video. Its constructor should also take in an artist argument.
2. Instantiate a new MusicVideo object and call the watch() method on it.
3. Add a method to MusicVideo called rockOut() that uses console.log to output a string like "You rocked out to La Bamba by Ritchie Valens!."

4. Bonus: Use an array of data and a for loop to instantiate 5 MusicVideo objects.
1. Bonus: Use an array of data and a for loop to instantiate 5 Product objects.
5. Bonus: Make an array of video data with both normal videos and music videos, loop through them, and decide on each one whether to make it a Video or MusicVideo object.

## Beginning with this JSBin template, make the following changes:

1. Create a new object called MusicVideo that extends Video. Its constructor should also take in an artist argument.
2. Instantiate a new MusicVideo object and call the watch() method on it.
3. Add a method to MusicVideo called rockOut() that uses console.log to output a string like "You rocked out to La Bamba by Ritchie Valens!."

4. Bonus: Use an array of data and a for loop to instantiate 5 MusicVideo objects.
5. Bonus: Make an array of video data with both normal videos and music videos, loop through them, and decide on each one whether to make it a Video or MusicVideo object.

1. Create a new object called MusicVideo that extends Video. Its constructor should also take in an artist argument.
2. Instantiate a new MusicVideo object and call the watch() method on it.
3. Add a method to MusicVideo called rockOut() that uses console.log to output a string like "You rocked out to La Bamba by Ritchie Valens!."

4. Bonus: Use an array of data and a for loop to instantiate 5 MusicVideo objects.
1. Bonus: Use an array of data and a for loop to instantiate 5 Product objects.
5. Bonus: Make an array of video data with both normal videos and music videos, loop through them, and decide on each one whether to make it a Video or MusicVideo object.


## Building HTML with OOJS

You can create objects that know how to interact with your website.

```javascript
petProduct.prototype.displayOnWebsite = function() {
    var $productInfo = $('<p></p>');
    $productInfo.text('You are buying a ' + this.name);

    var $list = $('#product-list');
    $list.append($productInfo);
};
```

## Resources

Add examples of real life OOJS


                
# Forms

You can collect information from users to use in our Object-Oriented JavaScript with HTML forms.

```html
<form class="buy" id="catnip">
    <h3>Catnip for sale</h3>
    <label for="quantity">Quantity:</label>
    <input type="number" id="quantity" name="quantity" value="1">
    <button class="button" id="buy-catnip">Buy catnip!</button>
</form>
```


                
## Retrieving form data

You retrieve the values of form elements using the value property.

```javascript
var quantity = document.getElementById('quantity').value;
console.log (quantity);
```

Or do it with [jQuery](http://api.jquery.com/category/forms/): 
```javascript
var $quantity = $('#quantity').val();
console.log ($quantity);
```


                
## Events

You can retrieve the value of a form at any time, like `onblur` (when a form element loses focus) or `onsubmit` (when the form element is submitted). `preventDefault` lets us hijack the form's default behavior so we can do stuff with JavaScript instead.

```javascript
var submitButton = document.getElementById('buy-catnip');
submitButton.onclick = function (event) {
    event.preventDefault();
    var quantity = document.getElementById('quantity').value;
    console.log (quantity);
}
```


                
## Events using jQuery

Here's the same script with jQuery syntax:

```javascript
var $submitButton = $('#buy-catnip');
$submitButton.click( function(event) {
    event.preventDefault();
    var $quantity = $('#quantity').val();
    console.log ($quantity);
});
```


                
#### Exercise 4

## Add to cart form

Use [this CodePen template](). Write your program with [vanilla JS](http://vanilla-js.com/) or [jQuery](http://api.jquery.com/category/forms/), your choice.

1. In our HTML, find the form markup for buying a cat toy.
2. Using a `submit` event, make the `addToCart()` function display the product name and price on the page. 
2. Using an `onblur` event, create a new method on the `PetProduct` prototype that displays the quantity the user has chosen inside the buy button. For example, the button would say "Buy 4 Catnips!"

Hint: Review <a href="http://cfarm.github.io/gdi-intro-js/class4.html#/10">the submit event</a> for documentation and examples

                
## Form Validation

Often we want to check that users have input the correct types of data into our forms, or the required fields, before we save the data to a database or complete a transaction.

<img src="img/email-validation.png" alt="Example of form validation on an email input field" />


                
## HTML5 Form Validation

With HTML5, we can have the browser perform the validation for us with some simple markup:

```html
<form id="email-signup">
    <h3>Join the Kitten Party Club to find out about new kitten cams!</h3>
    <label for="email">Your email:</label>
    <input type="text" id="email" name="email" required>
  <button type="submit" class="button" id="email-submit">Join</button>
</form>
```
                
## HTML5 Input types

Besides the `required` attribute, we can also specify specific types of data our form inputs will accept as valid:

```html
<label for="email">Your email:</label>
<input type="email" id="email" name="email" required> <!-- now validates for an email address -->
```

## HTML5 Pattern attribute

Validates the field against a Regular Expression pattern:

```html
<label for="email">Your email:</label>
<input type="email" id="email" name="email" required pattern="/@/"> <!-- now validates for an email address that contains an @ symbol -->
```

Check out [Stop Validating Email Addresses With Regex](https://davidcel.is/posts/stop-validating-email-addresses-with-regex/) for why to use such a simple pattern.

## Min, max, and step

The pattern attribute is included here as an optional fallback for browsers which don't support the number field.

```html
<input type="number" min="12" max="120" step="1" id="age" name="age" pattern="\d+">
```

## Maxlength

For text fields (`<input>` and `<textarea>`):

```html
<label for="tweet-text">Tweet a thing</label>
<textarea id="tweet-text" name="tweet-text" maxlength="140" rows="5"></textarea>
```

#### Exercise 5

## Validate our form inputs

Using your Add to Cart form from Exercise 4 or [this CodePen template](), add HTML5 validate attributes that: 

1. Make the quantity field required.
1. Make the quantity accept only whole numbers between 1 and 100.
1. Bonus: Make the quantity maximum the value of the `inventory` property on one of your `PetProduct` instances.


## Where's the JS?

You might need JavaScript form validation if...

* You need to support IE8 & IE9 (see [HTML5 form validation browser support](http://caniuse.com/#feat=form-validation))
* You want to customize your error message copy
* You want to style your error messages with CSS

## novalidate attribute

To use JavaScript validation, we want to disable the browser's default validation errors:

```html
<form id="email-signup" novalidate>
  <h3>Join the Kitten Party Club to find out about new kitten cams!</h3>
  <label for="email">Your email:</label>
  <input type="email" id="email" name="email" required>
  <button type="submit" class="button" id="email-submit">Join</button>
</form>
```

## DOM Manipulation

Remember [DOM manipulation](http://cfarm.github.io/gdi-intro-js/class3.html#/14)?

1. Find the DOM node and store it in a variable
1. Use methods to manipulate the node

```javascript
var emailForm = document.getElementById('email-signup');
var emailInput = document.getElementById('email');
var emailSubmitButton = document.getElementById('email-submit');
```

## Create new DOM elements

```javascript
document.createElement(tagName);
document.createTextNode(text);
document.appendChild();
```

## Create an error message

```javascript
var errorEl = document.createElement('span');
var errorText = document.createTextNode('Please enter a valid email address, thank you muchly');
errorEl.appendChild(errorText);
errorEl.className = 'error'; // adds error class 
emailForm.insertBefore(errorEl, emailInput); // inserts element into DOM with insertBefore() method
```
[Live Example](http://codepen.io/cfarm/pen/QNqxgq?editors=1010)


## Add an event listener

Versus `onsubmit()`: allows multiple event handlers for a single event type, without risk of [overwriting others](http://codepen.io/cfarm/pen/PNJyoP?editors=1010).

`addEventListener()` method takes two arguments: event type, and a callback function that receives notification when the specified event occurs.

```javascript
emailForm.addEventListener('submit', function() { 
    // do something when form is submitted
});
```

## Constraint Validation API

[HTML5 constraint validation API](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/Data_form_validation#The_HTML5_constraint_validation_API)

```javascript
emailForm.addEventListener('submit', function(event) { 
    var emailInputValue = emailInput.value;
    if (emailInput.validity.valid) {
        // yay it's valid, no error needed.
    } else {
        event.preventDefault();  
        emailForm.insertBefore(errorEl, emailInput); // insert our error when invalid on submit
    }
});
```

#### Exercise 6
## Custom validation error

Using your Add to Cart form from Exercise 5 or [this CodePen template]():

1. Edit your form so that the browser will not validate with HTML5.
1. Add vanilla JavaScript or jQuery to create a custom error message HTML element that says something like "quantity must be between 1 and 100"
1. Add an event listener to your JS that displays your custom error message when the submit button is clicked
1. Add CSS to style your message however you like.


#### Exercise 6: Bonus
## Custom validation error


1. Bonus: remove the error message when the form input is corrected and valid.
1. Bonus: make your JavaScript validity conditional remove the error message when the input is corrected and valid.

## jQuery Validation

The [jQuery Validation plugin](http://jqueryvalidation.org/) is a great library for cross-browser support and simplified syntax.

```javascript
$( "#credit-card-form" ).validate({
  rules: {
    field: {
      required: true,
      creditcard: true
    }
  }
});
```


# notes: things to add / change

* use Geolocation in events and forms! click a button to load the nearest cat cafe
* form: search for cafe based on city input
* console methods to debug object oriented js: log, warning
* error object with message property for OOJS methods.
* use regex in validation! 
* bonus exercise for form submit: set a cookie on email signup that stores a promo code. check for the cookie on checkout and insert promo code in form automatically.
* set a cookie when you click "addToWishList" or "addToCart" that remembers what you saved in your cart.
* make exercises for forms use OOJS


# slide section id's:

oojs (3)
forms (25)
modules (47)
tdd 
performance

# todos:

* Codepen exercise cleanup - make super simple.
* combine js-assessment + modules package.json so we only run npm install once.
* compress class2 folder and add link to class2.zip to slide1
* update outline in slide 1 so it's accurate.
* look for empty links by searching ]()
* make notes in notebook for which exercises have a bonus slide
* add survey link at end
* add break slides at 30/50/60?