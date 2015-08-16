# jQuery

## Introduction

jQuery is a JavaScript library. Everything you can do in jQuery is written with regular (sometimes called "vanilla") JavaScript. Therefore, understanding the fundamentals of JavaScript as a language (its constructs and syntax, its orientation to particular programming concepts) is important in order to effectively use jQuery. You want to be careful not to use jQuery as a crutch to avoid engaging with the internals of JavaScript and instead use it as a tool to expedite your work. 

jQuery is particularly useful for manipulating the DOM and providing smooth user experiences. There is also another extension library called jQuery UI that provides some nice effects and methods for enhanced user experiences.

## Where to get it

You can download jQuery from The jQuery Foundation's [website](http://jquery.com/download/). You can also use the [Google Hosted Libraries](https://developers.google.com/speed/libraries/?hl=en). The advantage of the former is that you are able to ensure the library is available. The disadvantage is that you are responsible for maintaining and updating that library in your codebase. The advantage of the latter is ease of use.

## `$(document).ready();`
Loading your JavaScript at the bottom of the page will help you avoid trying to do stuff to elements that aren't yet loaded onto the page, but `$(document).ready();` is an insurance policy against this problem. You should only use one `$(document).ready();` in your js file. When called more than once, things will break.

```
function someFunction(){
  //do a thing;
};

function someOtherFunction(){
  //do some other thing;
};

$(document).ready(function(){
  //someFunction();
  //someOtherFunction();
});
```

## The jQuery object and selecting elements

jQuery lets us grab elements from the DOM in an easy shorthand and turn them into jQuery objects with special methods. You can do it like this:
`jQuery(".some-class-selector");`
but more commonly you will see people get elements with jQuery like this:
`$(".some-class-selector");`

*Pro Tip*: The latter is the most common and is what I will use for all the examples in this clinic. However, be aware that occassionally you may use another library that also uses the `$` namespace and therefore run into conflicts, at which point you should refer to the jQuery [documentation on this topic](http://learn.jquery.com/using-jquery-core/avoid-conflicts-other-libraries/). It's highly unlikely you will need to handle this while you are working on your projects here, but I wanted to expose you to the concept.

jQuery lets you grab elements from the page using their CSS selectors (or elements), which makes it easy to use the Web Dev tools to find the best way to grab what you want.

### Getting an element by ID

`$("#contact-box");`

Since only one element should have any given ID, this is a way to target one item in particular. The `#` indicates that you are selecting an item by ID.

### Getting element(s) by class

`$(".feature");`

Since many elements can have the same class, the return of this could be a collection of jQuery objects with a class of `some-class`. The `.` indicates that you are selecting an item by class.

### Getting element(s) by HTML element type

Selecting all of the `h2` tags on a page:
`$("h2")`

You can combine these techniques to get specific with what you grab. For example, selecting all links in list items of a certain unordered list class might look like this:

`$("ul.a-taco-list")`

Note that HTML elements do not have any prefix to denote their selection (i.e. no `.` or `#`). It works just like your selectors in CSS.

### Assigning a jQuery object to a variable

You can assign any element you select with jQuery to a variable and then call jQuery methods on it.

`var dogeTaco = $("#doge-taco")`

## Manipulating selected elements

To figure out what you can do once you grab the item or items you want from the page, you're going to want to refer to the [jQuery API documentation](http://api.jquery.com/). 

### Hiding an element

`$("#doge-taco").hide();`

[`hide()` documentation](http://api.jquery.com/hide/)

### Changing the styling of element(s)

`$("h2").css("color", "red");`

[`css()` documentation](http://api.jquery.com/css/)

or maybe:
```
$("h2").addClass("blue");
```

[`addClass()` documentation](http://api.jquery.com/addclass/)

### Remove an element and then append it somewhere else

```
var dogeTaco = $("#doge-taco").remove();
$(#contact-box).append(dogeTaco);
```

[`remove()` documentation](http://api.jquery.com/remove/)

[`append()` documentation](http://api.jquery.com/append/)

## Event Handling
jQuery makes event handling super easy. We can attach a listener to any jQuery object and then execute some action when the event takes place.

### Click Listening
Execute an anonymous function when an object is clicked:

```
$("#doge-taco").click(function(){
  $("h2").addClass("blue");
});
```

[`click()` documentation](http://api.jquery.com/click/)

Using `this`:

```
$("#doge-taco").click(function(){
  $(this).hide();
});
```
