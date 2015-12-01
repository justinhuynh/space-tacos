# jQuery

## Introduction

jQuery is a JavaScript library. Everything you can do in jQuery is written with regular ([sometimes jokingly called "vanilla"](http://vanilla-js.com/)) JavaScript. Therefore, understanding the fundamentals of JavaScript as a language (its constructs and syntax, its orientation to particular programming concepts) is important in order to effectively use jQuery. You want to be careful not to use jQuery as a crutch to avoid engaging with the internals of JavaScript and instead use it as a tool to expedite your work.

jQuery is particularly useful for manipulating the DOM and providing smooth user experiences. There is also another extension library called jQuery UI that provides some nice effects and methods for enhanced user experiences.

## Where to get it

You can download jQuery from The jQuery Foundation's [website](http://jquery.com/download/). You can also use the [Google Hosted Libraries](https://developers.google.com/speed/libraries/?hl=en). The advantage of the former is that you are able to ensure the library is available. The disadvantage is that you are responsible for maintaining and updating that library in your codebase. The advantage of the latter is ease of use. Eventually you may want to switch to using a gem to load jQuery, such as [jquery-rails](https://github.com/rails/jquery-rails).

## Where to write your jQuery in your Sinatra app

When you write custom JavaScript or jQuery for your app, you should write the code in separate files and then include a link to it in your layout file or in the views where you want it. You'll do this with a `<script>` tag. In my example here, I just include it in my `index.erb` file, since that's my only view:

```
    <script src="/js/taco.js"></script>
  </body>
</html>
```

When you have many external JavaScript files, you'll want to name and organize them for the view they involve. If you have some JS that affects a particular module or feature that is included on multiple pages, group it in a file that is logically named for that module or feature.

## PRO-TIP ALERT: `$(document).ready();`
Loading your JavaScript at the bottom of the page will help you avoid trying to manipulate elements that aren't yet loaded onto the page, but `$(document).ready();` is an insurance policy against this problem. It's particularly useful for images or other content which may load after a js file at the end of the `<body>` or in the `<footer>`.

PRO TIP: It's best to only use one `$(document).ready();` in your js file as you get started. While technically you *can* use more than one, it is slightly slower (an optimization concern), more verbose (a style/readability concern) and arguably harder to debug (a developer experience concern). It also gets you into the habit of organizing your code into discrete functions.

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

*Pro Tip*: The latter is the most common and is what I will use for all the examples in this clinic. However, be aware that occassionally you may use another library that also uses the `$` namespace and therefore run into conflicts, at which point you should refer to the jQuery [documentation on this topic](http://learn.jquery.com/using-jquery-core/avoid-conflicts-other-libraries/).

jQuery lets you grab elements from the page using their CSS selectors (or elements), which makes it easy to use the Web Dev tools to find the best way to grab what you want. The ones built into Chrome, Safari, and Firefox are all really nice, but you might also enjoy [this add-on](http://chrispederick.com/work/web-developer/).

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

### Showing an element

`$("#doge-taco").show();`

[`show()` documentation](http://api.jquery.com/show/)

### GET FANCY! FADE OUT!

`$("#doge-taco").fadeOut();`

[`fadeOut()` documentation](http://api.jquery.com/fadeOut/)

### Changing the styling of element(s)

`$("h2").css("color", "red");`

[`css()` documentation](http://api.jquery.com/css/)

or maybe:
```
$("p").addClass("blue");
```

[`addClass()` documentation](http://api.jquery.com/addclass/)

### Remove an element and then append it somewhere else

```
var dogeTaco = $("#doge-taco").remove();
$("#contact-box").append(dogeTaco);
```

[`remove()` documentation](http://api.jquery.com/remove/)

[`append()` documentation](http://api.jquery.com/append/)

## DOM traversal

jQuery has some really nice functions to help you traverse the DOM and manipulate elements in relation to others. For example, if I grab an element and want to select its siblings based on whether they have certain characteristics, I can do that:

```
$("li.fancy").nextAll("li").css("background-color", "MediumSeaGreen");
```

[`nextAll()`](http://api.jquery.com/nextAll/) accepts an argument to use as a filter. In this case, we only want sibling elements that are `<li>`'s. If we add a random `<p>` tag in there, it won't get selected.

You can also grab siblings prior to the element you initially select with [`prevAll()`](http://api.jquery.com/prevAll/). Some other sibling methods, i.e. elements nested in the same element together, include [`siblings()`](http://api.jquery.com/siblings/), [`prev()`](http://api.jquery.com/prev/), and [`next()`](http://api.jquery.com/next/).

There are also methods to grab the [`parent()`](http://api.jquery.com/parent/) or [`children()`](http://api.jquery.com/children/) of a given element, or to remove all elements that match a specific criteria (`not()`). Check out all the [DOM traversal](http://api.jquery.com/category/traversing/) methods in the docs.

## Event Handling
Event handling is a process where we use JavaScript to "listen" for some interaction with an element, and then usually execute some corresponding action when that interaction takes place.

jQuery makes event handling super easy. We can attach a listener to any jQuery object and then execute some action when the event takes place.

### Click Listening
Execute an anonymous function when an object is clicked:

```
$("#doge-taco").click(function(){
  $("h2").addClass("blue");
});
```

[`click()` documentation](http://api.jquery.com/click/)

Or use `this` to perform some action on the object that was clicked:

```
$("#burrito-gram").click(function(e){
  e.preventDefault(); // because we're clicking on a link, we have to prevent it from doing link-y things, i.e. going to another page.
  $(this).hide();
  $(this).parent().append('<input type="text"></input><input class="button success" type="submit">');
});
```

### Mouseover
Execute an anonymous function when the mouse is hovering over an element:

```
$("#copyright").mouseover(function(){
  $(this).append("<img src=\"/img/solar_flare.jpg\"/>");
});
```

In addition to mouse events, jQuery also supports keyboard events. As you can probably imagine, this can make form validation without a page reload super smooth.

## PRO TIP ALERT: A word about raw DOM elements versus jQuery objects
From the jQuery FAQ:

> A jQuery object is an array-like wrapper around one or more DOM elements. To get a reference to the actual DOM elements (instead of the jQuery object), you have two options. The first (and fastest) method is to use array notation:

> ```
> $( "#foo" )[ 0 ]; // Equivalent to document.getElementById( "foo" )
> ```
> The second method is to use the .get() function:
> ```
> $( "#foo" ).get( 0 ); // Identical to above, only slower.
> ```
> You can also call `.get()` without any arguments to retrieve a true array of DOM elements.

When you use `$(".get-some-elements-by-class")`, what you get back is a jQuery object, which has methods that can be called on it. It's like a wrapper around the *actual* DOM element. If you need to get the latter so that you can call native DOM methods on it, you must first use one of the two techniques above.

Likewise, if you have a DOM element and need to use a jQuery method on it, you can assign it to a variable and wrap it like so:

```
var foo = document.getElementById(someId);
$(foo);
```
You'll know if you're confusing these two concepts if you get errors like these at any point in your console:

```
"event.target.closest is not a function"'
```
or
```
"TypeError: Object [object Object] has no method 'setAttribute'"
```
