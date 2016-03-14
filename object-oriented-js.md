# Object-oriented JavaScript
credit http://slidedeck.io/kpcs/Intro-to-Object-Oriented-JavaScript

## Uses for object-oriented programming

- Model physical concepts more clearly in your code
- Make your code easier to read
- Create code that is more easily maintainable and reusable

## Construtors and objects

### Objects 

```
var carObject = {
        make: 'Volkswagen',
        model: 'Rabbit',
        drive: function() {
            // Code that makes car go forward
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
// Assuming Car as defined before
Car.prototype.displayOnWebsite = function() {
    var $carinfo = $('<p></p>');
    $carinfo.text('You are buying a ' + this.model);

    var $list = $('#listofcars');
    $list.append($carinfo);
};
```

## Resources
