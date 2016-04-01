# Object-oriented JavaScript
credit http://slidedeck.io/kpcs/Intro-to-Object-Oriented-JavaScript

What we'll cover:
- What is an object?
- What are attributes and methods?
- What is class-based inheritance?
- What is prototype-based inheritance?
- How do we create objects using inheritance in JavaScript?
- How can we extend a prototype in JavaScript?
- How do we write maintanable code?

## Goal: Understanding objects

1. Create an object representing a product sold at an online pet store (using the [Codepen](http://codepen.io/pen/) website). For example, you could make a "petProduct" object with the properties "name," "category" and "price."

2. Use the push() method to add your product to an array that contains all the products in your online pet store.

3. Display your product on the page using [jQuery DOM manipulation](http://api.jquery.com/category/manipulation/) or native [JavaScript DOM insertion methods](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement).


## Goal: Understanding events and 'this'
http://kpcs.github.io/Intro_OOJS/#/6

1. In HTML, create a link to the website of your choice using the [Codepen](http://codepen.io/pen/) website. 
2. Using a JavaScript "onclick" event, make clicking on the link alert the link’s "href". 

Hint: never used the "onclick" event before, and not sure how to use it? Check out w3schools.com for <a href="http://www.w3schools.com/jsref/event_onclick.asp">some documentation and examples</a>

## What is an object? 

An object can be a variable, function, or data structure.

```
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

- Model physical concepts more clearly in your code
- Make your code easier to read
- Create code that is more easily maintainable and reusable

## Construtors and objects

### Objects 

```
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

- Attributes - object characteristics
- Methods - object functionality

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

    // Create a constructor function for new products
    function PetProduct() {
        // Set attributes of all new products
        this.category = 'Cats';
    }

    var kittenProduct = new PetProduct();

    // kittenProduct can access properties we defined in PetProduct
    console.log(kittenProduct.category);    // 'Cats'
        
## Adding Arguments

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


## Extending the prototype
The prototype is the collection of all the attributes and methods that the object knows about.

The prototype property of an object is used primarily for inheritance: methods and attributes on a function's prototype property are available to instances of that function. 

The prototype can be considered the "original" object, from which "copies" (instances) inherit properties.

Inheritance = Access to the properties and methods created by the parent object(s).

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


## Extending the Prototype with new methods
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

## Extending the prototype with new objects

// The constructor function
function PetClothing(name, category, price, size) {
    PetProduct.call(this, name, category, price);
    this.size = size;
}
// Extending the PetProduct object
PetClothing.prototype = Object.create(PetProduct.prototype);

// Instantiate a new PetClothing object
var doggySweater = new PetClothing('Doggy sweater', 'dog clothings', 30, 'medium');

Because it inherits from PetProduct, PetClothing has the properties and methods available to PetProduct as well.



```
function MusicVideo(title, uploader, seconds, artist) { // includes all arguments from Video plus new arguments
  Video.call(this, title, uploader, seconds); // new
  this.artist = artist; // set property for artist
}

MusicVideo.prototype = new Video();
MusicVideo.constructor = MusicVideo;

```

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

```
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

## Warm up exercises

### Goal: Understanding form events

1. In our HTML, find the form markup for buying a cat toy.
2. Using a JavaScript "submit" event, make submitting the form display the product name and price on the page. 

Hint: Review <a href="http://cfarm.github.io/gdi-intro-js/class4.html#/10">the submit event</a> for documentation and examples


## Form Validation



## Warm up exercises: For loops and counters

