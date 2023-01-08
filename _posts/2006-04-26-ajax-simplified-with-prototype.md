---
title: "AJAX: Simplified beyond belief with Prototype"
date:  2006-04-26 00:00:00 -0700
layout: single
---

Before reading this I assume you know your JavaScript.

Creating your own AJAX slash AJAH handler in JavaScript can be a huge pain in the neck. For those who have been struggling with AJAX for a while there’s an easy way out. Its called “prototype” a JavaScript framework that aims to ease development of dynamic web applications. And that’s a direct quote from prototype.conio.net. AJAX is not the only thing that prototype handles, it also eases regular operations such as the `document.getElementById(’myeElementId’);` by simplifying it as `$F(’myElementId’);`.

Now, for the AJAX part in which we are all interested. Let’s say you have a div container like below:

```html
<div onclick="myMakeRequest('myElement');" id="myElement">
My Container
</div>
```

Which `onclick` is going to find the function `makeRequest` which in turn will replace the innerHTML property of this particular div (myElement) with the AJAX response.

Normally when generating your own AJAX-code you’ll be creating `xmlHTTPRequest`, probing browsers etc, etc. Prototype simplifies this by giving you something like this:

```js
function myMakeRequest(elementId) {
    var url = 'my_file.xml'; // Your XML file
    var Ajax = new Ajax.Updater({success: elementId},url,{method: 'get'});
}
```

The good thing about this method is that your page or your .js file isn’t humongous in filesize. The thing that isn’t so great about it is that the prototype library is 54KB in size which could make your page quite slow qua loading time on a slower connection (non-broadband).

Still, it’s easier than coding it all yourself, I mean; what’s the point in reinventing the wheel? Especially a well-formed wheel. Below follows the entire code that will display the example given above.

```html
<script src="prototype.js" type="text/javascript"></script>
<script type="text/javascript">
    function myMakeRequest(elementId) {
        var url = 'my_file.xml'; // Your XML file
        new Ajax.Updater({success: elementId},url,{method: 'get'});
    }
</script>
<div onclick="myMakeRequest('myElement');" id="myElement">
    My Container
</div>
```

Sources and Requirements:

* [Prototype](http://prototype.conio.net/)
* [MDN: Ajax Getting Started](http://developer.mozilla.org/en/docs/AJAX:Getting_Started)
