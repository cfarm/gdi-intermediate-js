# Object-oriented JavaScript
credit http://slidedeck.io/kpcs/Intro-to-Object-Oriented-JavaScript


Review: objects, events, this

## Goal: Understanding objects

1. Create an object with multiple properties. For example, you could make a "student" object with the properties "name" and "hometown".
2. Use console.log() to print out a sentence that includes the properties of that object. For example, "[name] is from [hometown]."


## Goal: Understanding events and 'this'
http://kpcs.github.io/Intro_OOJS/#/6

1. In HTML, create a link to the website of your choice. 
2. Using a JavaScript "onclick" event, make clicking on the link alert the link’s "href". 

Hint: never used the "onclick" event before, and not sure how to use it? Check out w3schools.com for <a href="http://www.w3schools.com/jsref/event_onclick.asp">some documentation and examples</a>

## Uses for object-oriented programming

- Model physical concepts more clearly in your code
- Make your code easier to read
- Create code that is more easily maintainable and reusable

## Construtors and objects

### Objects 

```
var kittenProduct = {
        category: 'Cat Toys',
        name: 'Catnip Jellyfish',
        buy: function() {
            // Code that adds product to shopping cart
        }
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


## Building HTML with OOJS

You can create objects that know how to interact with your website.

```
KittenProduct.prototype.displayOnWebsite = function() {
    var $productInfo = $('<p></p>');
    $productInfo.text('You are buying a ' + this.name);

    var $list = $('#product-list');
    $list.append($productInfo);
};
```


# Forms

## Warm up exercises

### Goal: Understanding form events

1. In our HTML, find the form markup for buying a cat toy.
2. Using a JavaScript "submit" event, make submitting the form display the product name and price on the page. 

Hint: Review <a href="http://cfarm.github.io/gdi-intro-js/class4.html#/10">the submit event</a> for documentation and examples


## Form Validation

