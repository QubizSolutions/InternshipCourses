# Introduction to HTML, CSS and JavaScript

[1. HTML](#1-html)

[2. CSS](#2-css)

[3. JavaScript](#3-javascript)

[4. Tips](#4-tips)

**Why Study HTML/CSS/JavaScript?**

There are 3 languages, all web developers/ testers must learn:
   1. HTML to define the content of web pages
   2. CSS to specify the layout of web pages
   3. JavaScript to program the behavior of web pages

## <a name="1-html"></a>1.HTML

Basic structure: 

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Page Title</title>
        <!-- Style -->
    </head>
    <body>
        <h1>This is a Heading</h1>
        <p>This is a paragraph.</p>
	    <!-- Scripts -->
    </body>
</html>
```

* The ```<!DOCTYPE html>``` declaration defines this document to be HTML5
* The text between ```<html>``` and ```</html>``` describes an HTML document
* The text between ```<head>``` and ```</head>``` provides information about the document
* The text between ```<title>``` and ```</title>``` provides a title for the document
* The text between ```<body>``` and ```</body>``` describes the visible page content
* The text between ```<h1>``` and ```</h1>``` describes a heading
* The text between ```<p>``` and ```</p>``` describes a paragraph

### **HTML Attributes**

* All HTML elements can have **attributes**
* Attributes provide **additional information** about an element
* Attributes are always specified in **the start tag**
* Attributes come in name/value pairs like: **name="value"**

```html
<a href="http://www.w3schools.com">This is a link</a>
<img src="w3schools.jpg" width="104" height="142">
```

### Class attribute

The HTML class attribute makes it possible to define equal styles for elements with the same class name.

```html
<!DOCTYPE html>
<html>
    <head>
        <style>
        .cities {
            background-color: black;
            color: white;
            margin: 20px 0 20px 0;
            padding: 20px;
        } 
        p{ 
            color: black; 
        }
        </style>
    </head>
    <body>
        <div class="cities">
            <h2>London</h2>
            <p>London is the capital of England.</p>
        </div>
        <div class="cities">
            <h2>Paris</h2>
            <p>Paris is the capital and most populous city of France.</p>
        </div>
    </body>
</html>
```

## <a name="2-css"></a>2.CSS

[CssStructure]: https://github.com/QubizSolutions/InternshipCourses/blob/master/HTML_CSS_JS/Content/Img/css_structure.PNG "CSS structure"
[CssBoxModel]: https://github.com/QubizSolutions/InternshipCourses/blob/master/HTML_CSS_JS/Content/Img/css_box_model.PNG "CSS Box Model"

### **What is CSS?**

* CSS stands for Cascading Style Sheets
* CSS describes how HTML elements are to be displayed on screen, paper, or in other media
* CSS saves a lot of work. It can control the layout of multiple web pages all at once
* External stylesheets are stored in CSS files

![alt text][CssStructure]

### **External Style Sheet**

With an external style sheet, you can change the look of an entire website by changing just one file!
Each page must include a reference to the external style sheet file inside the ```<link>``` element. The ```<link>``` element goes inside the ```<head>``` section:

```html
<head>
    <link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

An external style sheet can be written in any text editor. The file should not contain any html tags. The style sheet file must be saved with a .css extension.
Here is how the **"myStyle.css"** looks:

```css
body {
	background-color: lightblue;
}

h1 {
	color: navy !importan;
	margin-left: 20px;
}
```

### **Internal Style Sheet**

An internal style sheet may be used if one single page has a unique style.
Internal styles are defined within the ```<style>``` element, inside the ```<head>``` section of an HTML page:

```html
<head>
    <style>
        body {
            background-color: linen;
        }

        h1 {
            color: maroon;
            margin-left: 40px;
        } 
    </style>
</head>
```

### **Inline Styles**

An inline style may be used to apply a unique style for a single element.
To use inline styles, add the style attribute to the relevant element. The style attribute can contain any CSS property.
The example below shows how to change the color and the left margin of a ```<h1>``` element:

```html
<h1 style="color:blue;margin-left:30px;">This is a heading.</h1>
```

### **The CSS Box Model**

All HTML elements can be considered as boxes. In CSS, the term "box model" is used when talking about design and layout.
The CSS box model is essentially a box that wraps around every HTML element. It consists of: margins, borders, padding, and the actual content. The image below illustrates the box model:

![alt text][CssBoxModel]

* **Content** - The content of the box, where text and images appear
* **Padding** - Clears an area around the content. The padding is transparent
* **Border** - A border that goes around the padding and content
* **Margin** - Clears an area outside the border. The margin is transparent

The box model allows us to add a border around elements, and to define space between elements.

### **Selector Specificity Weights**

1. **!important:** Any property declaration with the term !important takes highest precendence, even over inline styles. If !important is declared more than once on conflicting properties targeting the same element, you CSS author be shot, and the other precendence rules are in effect. It’s as if the weight of the selector with the !important declaration were 1-X-A-B-C, for that property only (where A, B and C are the actual values of the parent selector as described below). Because of this, important should not be used, but can be handy in debugging.

2. **style="":** If the author includes style attribute on an element, the inline style will take precedence over any styles declared in an external or embedded stylesheet, other than !important declarations. Anyone including style in production should also be shot, Just sayin’. Note that styles added with the JavaScript style (i.e.document.getElementById('myID').style.color = 'purple';) property is in effect creating an inline style ( ... id="myID" style="color: purple"...). The weight of style="" is 1-0-0-0.

3. **id:** Among the selectors you’ll actually be including in your stylesheet, ID’s have the highest specificity. The weight of an id selector is 1-0-0 per id.

4. **class/pseudo-class/attributes:** As shown in the second code block above, class selectors, attribute selectors and pseudo-classes all have the same weight of 0-1-0.

5. **type:** Element type selectors and pseudo-elements, like :first-letter or :after have the lowest value in terms of specificity with 0-0-1 per element.

## <a name="3-javascript"></a>3.JavaScript

[ArithmeticOperators]: https://github.com/QubizSolutions/InternshipCourses/blob/master/HTML_CSS_JS/Content/Img/js_arithmetic_operators.PNG "Arithmetic operators"
[LogicalOperators]: https://github.com/QubizSolutions/InternshipCourses/blob/master/HTML_CSS_JS/Content/Img/js_logical_operators.PNG "Comparison and Logical Operators"

**JavaScript is a high-level, dynamic, untyped, and interpreted programming language**

**JavaScript is an object oriented programming language, used for adding functionality to a web-page**

JavaScript can be used for:
 
* Loading content on the page in an async manner, without refreshing the whole page. Ex:Facebook’s timeline
* Sending data to the server.
* Reading cookies
* Validating forms
* Modifying the HTML in real-time (show-hide / animations / adding content)
* And much more

### **Arithmetic operators:**

![alt text][ArithmeticOperators]

### **Comparison and Logical Operators:**

![alt text][LogicalOperators]

### **JavaScript variables:**

```javascript
var length = 16;                                // Number

var lastName = "Johnson";                       // String

var cars = [1, "Volvo", "BMW"];                 // Array

var x = { firstName:"John", lastName:"Doe" };   // Object
```

* a variable declared without a value will have the value undefined.

* you can declare many variables in one statement. Start the statement with var and separate 

```javascript
var person = "John Doe", carName = "Volvo", price = 200;
```

### **JavaScript Functions:**

A JavaScript function is defined with the **function** keyword, followed by a **name**, followed by parentheses **()**

Inside the function, the arguments behave as local variables

```javascript
function myFunction(p1, p2) {
    return p1 * p2;      
}
```

A JavaScript function can also be defined using an **expression**.

A function expression can be stored in a variable: 

```javascript
var x = function (a, b) {return a * b};
var z = x(4, 3);
```

### **JavaScript Objects:**

```javascript
var person = {
    firstName:"John",
    lastName:"Doe",
    age:50,
    eyeColor:"blue", 
    fullName: function(){
        return this.firstName + " " + this.lastName;
    }
};
```

You can access object properties in two ways:

```javascript
objectName.propertyName
```
```javascript
objectName["propertyName"]
```

You access an object method with the following syntax:
```javascript
objectName.methodName()
```

You can add properties on the fly like this: 
```javascript
objectName.newProperty = “some_value”
```
This will create the property called “newProperty” and assign the value to it

### **JavaScript + HTML**

JavaScript interacts with objects from an HTML page:
* Paragraphs - ```<p>```
* Spans - ```<span>```
* Inputs - ```<input />```
* Divs - ```<div/>```
* etc

To interact with the DOM object, you need to hold a reference to it, in a variable. Getting these references is done by using functions such as: 

* getElementById(‘button_demo’) ```<a class="btn" id="button_demo">Text</a>```
* getElementsByClassName(‘btn’) ```<a class="btn" id="button_demo">Text</a>```
* getElementsByName(‘name’) ```<input class=“name" />```

Note that when using the class name, **multiple** objects can be returned – because the class is not unique in a document. 

The Id, on the other hand, is unique and should be used only once, on **singular** elements – such as a div or a form.

Classes are used for repetitive objects (buttons, paragraphs, lists etc).


JavaScript code can be placed in the page between the ```<head>``` or ```<body>``` tags. The code must be between surrounded by ```<script>``` tags. 

```html
<script>
    document.getElementById("demo").innerHTML = "My First JavaScript";
</script>
```

The alternative is JavaScript code placed in external files, that have the .js extension. 

To reference an external .js file, we use the ```<script>``` tag, like in the second example.
```html
<script src="~/Scripts/app/exemple.js"></script>
```

### **Debugging**

* JavaScript files are sent to the client by the web-server, and are downloaded on each computer – when the page loads.

* Use the browser’s Console, to debug the code, add breakpoints and execute the code line by line. In Google Chrome press F12 to open the console. The loaded files are found in the Sources tab. 

* Add a breakpoint to the desired line and follow the steps to execute the code. The code execution will stop at the breakpoint, and you are able to see contextual values for the variables, go line-by-line pressing F10, or enter subsequent function calls using F11. 


### **Errors**

* JavaScript errors are shown in the console in the form of a list with red font, noting the error and the line in the file at which it occurred.

* An error occurrence stops the code execution, after the error’s line.

## <a name="4-tips"></a>4.Tips

1. Do not use code in the HTML page, always put it in external files.

2. Reference your external files as lower on the page as possible – so they are downloaded after the page content has loaded.

3. The order of the referenced files does matter, if you have dependencies between javascript files.

4. With ASP.NET, always use ScriptBundles. The scripts are added to a bundle, or more, and sent to the client as a single, minified file. Advantages: 
    * Faster loading pages, since it’s only one file
    * In production, your files cannot be easily read / debugged by third parties

5. After each JavaScript modification, clear the browser cache (Ctrl + F5 in Chrome), to be sure that the old Js version is not loaded anymore.

### **Reading & Examples:**

http://www.w3schools.com
