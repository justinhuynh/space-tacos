# Understanding jQuery

jQuery is a JavaScript library. Everything you can do in jQuery is written with regular (sometimes called "vanilla") JavaScript. Therefore, understanding the fundamentals of JavaScript as a language (its constructs and syntax, its orientation to particular programming concepts) is important in order to effectively use jQuery. You want to be careful not to use jQuery as a crutch to avoid engaging with the internals of JavaScript and instead use it as a tool to expedite your work. 

jQuery is particularly useful for manipulating the DOM and providing smooth user experiences. There is also another extension library called jQuery UI that provides some nice effects and methods for enhanced user experiences.

## Where to get it

You can download jQuery from The jQuery Foundation's [website](http://jquery.com/download/). You can also use the [Google Hosted Libraries](https://developers.google.com/speed/libraries/?hl=en). The advantage of the former is that you are able to ensure the library is available. The advantage of the latter is ease of use.

## The jQuery object

jQuery lets us grab elements from the DOM in an easy shorthand and turn them into jQuery objects with special methods. You can do it like this:
`jQuery("#doge-taco");`
but more commonly you will see people get elements with jQuery like this:
`$("#doge-taco");`



