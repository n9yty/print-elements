## Print selected webpage elements 

This tiny ES6 Javascript module allows printing selected HTML Element nodes from a web page.

### Usage

1. Include the `print_elements.js` script on your page.
2. Include a print stylesheet where you hide all elements having `pe-no-print` class. See below for details.
2. Invoke the `PrintElements.print(...)` function with a list of HTML elements to print the selected elements.

For a full working example, check the `example` directory.

### How does it work

The script traverses the DOM from each of the given elements up to the `BODY` element. All selected nodes and their ancestors 
will be marked with a class to keep them in the print view. All siblings of selected nodes, and
siblings of their ancestors will be marked with a class to hide from print view. 
A print-only css will take care of actually hiding and showing the respective elements.

### Motivation

There are several approaches out there for the problem of how to print a part of an HTML page. 
I felt all of these had some trade-offs, so I tried to find a solution without the side-effects of other attempts.

#### Popular solution no 1. - Media specific styles or stylesheets

This approach requires that you build your whole site print-aware, telling in advance how your pages render when printing. 
It is a very clean solution and requires no JavaScript.
However, you'll have to statically assign classes and css definitions for printable and non-printable sections of your HTML code.
This does not help if you have to decide what to print dynamically.

#### Popular solution no 2. - Create a new document with the selected element's content

This usually goes like grabbing the inner HTML of the given node, insert it into a new document, and print it. 
Some variations suggest to save the current body content, replace it with the given node's content, then print, then revert the body content to the original.
Either way, it is messy - preserving styles can be tricky, will detach event handlers if replacing the current body content, and so on. 

## Benefits of this library

* No need to statically declare what is printable and what is not - just invoke the print function with any nodes, any time.
* No need to move around DOM nodes
* No new window or tab when printing
* Keeps all the styles for the selected elements
* Keeps all event bindings, style definitions - it doesn't do anything invasive with your document.
