# Coding Standards And Best Practices
 
**Client-Side Coding Professional Standards**

## Introduction 
Coding standard and best practices generally improve the quality of the code and the systems performance while running, within this document we will explain the best coding standards and practices based around JavaScript and its iBes development environment to imporve its quality and performance.

## JavaScript 
### Source file basics

File Name 

Names of files should always be lower case, and can include dashes(-) or underscores(_), the framework and project naming convention should be consistent and relevant to the meaning of the file.
File Formatting And Whitespace Characters 
The space char (ASCII Horizontal Space Character) is the only white space character to be found throughout source files(/src/) and if so will be ignored. Tab characters are not used for indentations, clang-format will format on save once configurated within a code editor. This keeps a consistent format throughout the code.

See here for how whitespace characters are categorised and how different programming languages defines whitespace character sets - https://stackoverflow.com/a/18169122.

Source file structure

### License or copyright information, if present 

Usually legal documents should contain the copyright information however the date and copyright logo should be displayed at the start of the user experience to show that the application is protected.

### ES Modules

Imports 

Import statements must not be line wrapped. ES modules must use the import statement to include another ES module instead of using the  goog.require  this should error or emit a warning if tried for standard up-to-date development environments. Imports should always be at the top of a script tag or JS file. Examples:

```
import './sideeffects.js'; //everything

import * as goog from '../closure/goog/goog.js';  //everything as variable

import * as parent from '../parent.js'; //everything as variable

import {name} from './sibling.js'; //multiple exports from './sibling.js'
```

### The File’s Implementation

All functional implementation should follow after all file dependency information is declared and separated by at least one blank line for better readability. This includes any local modules decorations that are used within the same scope(constants, variables, classes, functions, ect).

```
import './otherModule.js'; 

import './otherModule.js'; 

import './otherModule.js'; 

const aConstant = ‘Cant Change !’ ;

var variable = 1;
```

### Formatting

Clang-Format

Clang-format has been constructed to ensure that the formatter performs the correct format on JavaScript files and formats depending on line(column) length, readability and characters, and scope construction/braces. Using this formatter keeps a strong, consistent format throughout javascript applications and prevents any source control issues where code can be committed wrong or missed when style formatting changes.
Braces/Defining Scope 
Braces (e.g. {} ) are required for defining scops. Conditional statements, functions, ect all require a scope and for better practice even if the scope only includes one line but see below exception. The first code line must begin on a new line of the scope.
Seen as bad practice:
```
if (someVeryLongCondition())

  doSomething();

for (let i = 0; i < foo.length; i++) bar(foo[i]);
```
Exception: If a scope only contains a short one line of code and the condition has no else statement, then this may be kept on the same line with no braces when it improves readability.

```
if (shortCondition()) foo();
```

Block Indentations 

Each time a new scope is defined the indentations increase by two white spaces or one generic tab length. This shows the reader what’s included in each scope and prevents issues that might occur when using variables that arnt defined in a particular scope. Block indentations also improves the files structures readability and keeps consistency throughout the application.

Statements

There should be one statement per line, separated by a line break (;), replying on automatic semicolon insertion is forbidden.

Column Limit 

Javascript modules have a column limit of 80 characters long, any line that exceeds 80 chars ling will require to be line wrapper. Exceptions:

```
    goog.module, goog.require and goog.requireType statements.
    ES module import and export from statements.
    Lines where obeying the column limit is not possible or would hinder discoverability. Examples include: 
    A long URL which should be clickable in source.
    A shell command intended to be copied-and-pasted.
    A long string literal which may need to be copied or searched for wholly (e.g., a long file path).
```

Line Wrapping

When a single line exceeds the column limit of 80 characters long or even just for better readability, the statement should be broken down into several lines depending on the statement. There is no right-way of line-wrapping code in every situation as all scenarios will be completely different not just in code, but there meaning. Clang-Format would automatically find the best format for your statement scenario.

### Comments

When a developer either uses hard to read code, hacky solutions or just code that might be hard to understand, code comments are important to show other developers or the reader what’s happening and why, projects are normally worked on by big groups it is important for all member to know what is happening in all parts of a project and why the solution has been chosen 

Block comment style 

Block comments are indented at the same level as the associated code which is normally found below the comments. Please note that other languages use many different comments syntax however for better practice JavaScript files use the below syntax for comments:

```
/*

 * This is

 * okay.

 */


// And so

// is this.


/* This is fine, too. */
```

Comments are not enclosed in boxes drawn with asterisks or other characters. Don’t implement PHP comments on a JavaScript file like /** … */ .

### Parameter Names

Parameter name comments should be used when the name of the parameter or its value does not indicate the meaning of the parameter.

### Languages Features 

Local Variable Declarations

Use const and let, the keyword for declaring variables with var should be avoided due to var variables not being block scoped but they are functional scoped. This meaning var variables can be associated with local global unless they are functional bound. Const should be used by default unless a variable needs to be re-defined.
One Variable Per Declaration 

For better readability and to prevent type errors, only declare one variable on one line using only one declaration key word. 

```
Let a = 100, b = 200;

// turns into 

Let a = 100;

Let b  = 100;
```

Declare When Needed, Initialized As Soon As Possible 

Declared variables don’t always inherit a value and a value isn’t always set on the declaration of a variable meaning variables can be undefined at the start of their life cycle, however they shouldn’t be declared and initialized far away from each other. Instead, they should be declared and initialised where they are used to minimalize their scope which also minimise resources  that the application uses which will improve performance.

Declare Types As Needed 

Annotations can be used above a variable a declaration to indicates its type and sometimes a definition of what the variable is used for. Short annotations can be declared inline depending on how long the annotation is and also this depends on if this improves readability or not. Note: do not mix inline and line wrapped annotations and this can get very ugly and confusing to read. Example:

```
const /** !Array<number> */ data = [];


/**

 * Some description.

 * @type {!Array<number>}

 */

const data = [];


Array Literals 
Use Trailing Commas 
Using Trailing commas where ever there could be a line break between the array scope. This keeps statements from being too long column wise and improves readability and the style of the JavaScript document, creating a more consistent code base. Example:

const values = [

  'first value',

  'second value',

];
```

Do Not Use the Variadic Array Constructor

The `Variadic Array Constructor` is the object of the Array type that can be used to declare an array, however if an array needed an explicit size, then using the object to declare the Array is allowed, example:

```
new Array(length)
```

Using the brackets [ and ] we can declare an array and the values of the array without having to limiting the objects capabilities. Example:    

```
// Bad Practice 

Const a = new Array(variableOne, variableTw0);

// Good Practice
//make an array with size, but undefined content 

Const a = new Array(sizeOfArray);

Const a = [valueOne, valueTwo];
```

None-numeric properties

Do not use any non-numeric properties for an array apart from the arrays length, use map or object instead. Th reason behind avoiding non-numeric properties is because arrays will iterate over. However for and forEach statements will skip over non-numeric properties meaning things can be lost and issues could occur. Please see a better description of where non-numeric array keys can be found and used - https://stackoverflow.com/a/52395969

Good Practice:

```
let arr = [
    'example-one',
    'example-two'
];
```

Bad Practice:

```
let arr = ['cribriform plate','mastoid','hyoid'];
arr.exampleOne = 'brown';
arr.exampleTwo = 'white';

for(let i in arr){
    console.log(i);

    //0,1,2,3,exampleOne,exampleTwo
}
```

Destructuring 

When only wanting to target only certain elements in an array without iterating through the whole array, literals can be assigned to values on the left-hand side of a statement. This speeds up performance when dealing for any amount of data but especially when the array is full of data. Example Scenario: 

You are wanting the first 3 elements of an array to have literals and the rest within another literal.

```
Const [valueOne, valueTwo, valueThree, …rest] = getResults(); 

Let [, b, , d] = arr; // gets the second and fourth  value of array
```

Within the above example, values 1 – 3 can easily be accessed without going through the whole array. Bad Practice:

```
Function([a, b, c] = [4, 5, 6]){ ... }  // use params 
```

Spread Operator 

Array literals(like mentioned above) can use the spread operator … to gather one or more literals from an array. This is specially handy if you are wanting to only want to declare a few items from an array as literals and the rest in another literal. Array.Prototype constructions need to refer to the spread operator due to better readability and more simplified code.

```
Const [valueOne, valueTwo, valueThree, …rest] = getResults(); 
```

### Object Literals 

Use Trailing Commas

When line breaks code but the functionality process is still flowing, then use trailing commas which will improve the users chances of following the process without getting lost. Object literals will need to be separated by trailing commas.
Object Constructors

Like arrays, object constructors should be avoided for better consistency throughout the code. Use object braces instead:

```
Let a = {};

Let b = {valueOne: ‘String’, valueTwo: 100};
```

Quoted/Unquoted Keys

Object literals can be represented by either structs(unquoted/or symbols) or dicts(quoted/computed keys). These representations of how literals are defined in an object shouldn’t be mixed to keep consistency throughout the application.

```
{

	width: 42; 		// struct-style unquoted key

	`maxWidth`: 23;	// dict-style quoted key

}
```

The rule mentioned above should also be applied to passing parameters into functions, object literals should be checked against undefined not null, this should be represented by if property is false or not and not using the object function hasOwnProperty.

Method Shorthand

Methods can be defined on object literals when using the function name shorthand:

```
{

	value: ‘coding’,

	getValue(){

		return this.value; 	// returns `coding`

	}

}
```

Note: Referring to this keyword, using this.value refers to the object literals themselves. Arrow functions can be used to refer to the scope outside the object literals like so:

```
{

	this.stuff = ‘coding’

	return {

		stuff: ‘not coding’

		method: () => this.stuff	// returns `coding`

	}
}
```


Shorthand Properties

Short hand properties are variables that can be added without any defined keys, as the variable that should be defined before the object already has a name, this is the key to the property. Example:

```
Const a = 1;

Const b = 2;

Const obj = {
	a,	
	b,
	add(){ return this.a + this.b }
};
```

Destructuring 

Object Destructuring patterns should be used for defining object keys which can be used to access that property from the object. Function parameters can also use the same pattern if the value might not be passed in or conditionally if the parameter is undefined.

```
function exampleFunc(str = ‘this string is used if str is undefined’)
```

### Classes

Classes are representations of vertical objects that have properties, constructing a more object-oriented style of programming.

```
class Foo {
  constructor() {
    /** @private @const {!Bar} */
    this.bar_ = computeBar();

    /** @protected @const {!Baz} */
    this.baz = computeBaz();
  }
}
```

Link - https://google.github.io/styleguide/jsguide.html#features-classes


Constructors

Constructors are optional within a class, subclasses constructors must be super, interfaces should declare non-method properties in constructors and only define variable properties within interfaces.

Fields 

Field properties of an objects should be constructed with the correct accessible keywords, private, protected and public. Most fields should be private with public functions for gathering or manipulating the properties where possible, more sensitive functionality/data needs to be protected and only accessed within its own class, public functions again can be called for manipulating protected fields outside the class. Better object-field mapping increases security and better readability on entity relationships. Once the constructor has finished building, no properties should be added or removed from the object, as this significantly hinders VM’s ability to optimise. If properties need to be initialised after the constrictor has built, then keep these properties as undefined until ready to manipulate.

Static Methods 

Module-local functions should be considered over private static methods if this does not affect readability, this keeps functionality in relevant places. If static methods are used, then certain rules should be applied when calling them: 

- Should only be called on the base class itself 
- Should not be called on variables containing a dynamic instance 
- Should not be called directly on a subclass that doesn’t define the method itself

Old-Style Class Declarations 

ES6 class declarations should be used at all times. goog.defineClass, framework class definitions(e.g. Framework.class) and other methods outdated methods that belong to ES5 should not be used.
Good Practice:

```
classs AClass {
    id: 1,
    name: 'This is a name'
};
```

Bad Practice:

```
const user = {
    id: 1,
    name: 'This is a name'
};

Framework.class{
    id: 1,
    name: 'This is a name'
};

goog.class{
    id: 1,
    name: 'This is a name'
};
```

### Do Not Manipulate Prototypes Directly 

The ES6  class declaration is much more readable for defining properties than using prototypes properties. Frameworks like Angular should be exempt to this rule and should use prototypes  if even-worse work arounds are considered.

Getters And Setters 

For JavaScript classes, do NOT use getters and setters for class properties. These functions are difficult to pass around and have limited support in the complier as JavaScript has just started introducing OO styled coding, so some features will be easier to replicate in a more original way. Data binding frameworks like Angular should be excused from this rule as this could be unavoidable. If used, Getters should not manipulate any variable or property state just gather the data associated.

Overriding toString 

The toString function can eb overridden but must always be practical in case of failing which will cause complier and run time issues depending on how the operation is failing.

Example of overriding toString with a function:

```
	function doSomething() { }

	

	doSomething.prototype.toString = function(){

		return “[object doSomething]”;

	}
```

Example of overriding toString with an object:

```
let objStr = new Object();

console.log(“The object to string equals: “+ objStr);
```

Interfaces 

Interfaces may be declared similar to ES6 class declarations and can be used as a schema that implicitly implemented by a class or an object literal. This having a schema to check again will emit complier errors if any issue happens preventing run time issues or using values that arnt expected.

```
	interface Attrs{

		location: Location, 

		name?: string|undefined,

		total: number

	}
```

Function

Top-Level Functions 

Top-level functions are global properties of objects defined in JS modules(e.g. parseInt). Using the object export, we are able to export functions to be used by other JS modules or they can be declared locally and optionally exported. Export syntax looks similar to:

```
	export function doSomething(){

		…

	}
```

And to import this function from another JS module, use similar syntax:

```
	Import { doSomething } from ‘./path/to/file’
```

Note: use the following export methods to export functions, classes and more as this is the updated, preferred method also keeping the ES6 style consistent around a system.

Nested Functions And Closures 

Nested Functions: 

```
const doSomething = function(){

		const doSomethingAgain = function(){	
		  // ...
    }
}	
```


All nested functions should contain a name for a function that should be declared to a local const, this gives better usage and easier access to the nested function.

Arrow Functions 

As mentioned above, the concise ES6 arrow functions: 

```
() => { … } 
```

These functions preferred over the keyword function syntax and other methods around concealing scopes(e.g. const self = this;). This providing a brief and functional syntax. Example:

```
	doSomething(var => doSomethingElse(paramOne, paramTwo))
```

Never do:

```
	const functionVar = () => doSomething();
```

Parameter And Return Types 

Function parameters and return types should be addressed through annotations so the reader knows what the function takes and returns, the annotation should also have a brief explanation of what the function does and this should be consistent throughout the system. 

```
/**

 * @param {string} required This parameter is always needed.

 * @param {string=} optional This parameter can be omitted.

 * @param {!Node=} node Another optional parameter.

 */
```

### Function Parameters 

Required Parameters 

Required parameters should also be declared first within the parameter list, these parameters should also be noted on the function annotations. 

Optional Parameters 

Optional parameters should come after the required parameters have been declared, and maybe assigned with equal operator to assign to a default parameter if needed to be initialised if undefined when function has been ran. 

```
doSomething function(required, optional = ‘this is opts’, total = 3){
    …

}
```

Rest Parameters 

Rest parameters is a ES6 parameter used for adjustable parameters that can take any types or amount, this makes function more robust and can be well-suited to more generic functionality. An explanation of how to define rest parameters and why we should use them in certain situations:

```
function doSomething(paramOne,  …rest){

	let sum = 0;

	for(let i of input){

		sum += 1;

	}


	return sum;	

}

console.log(doSomething(undefined, 1, 2);               // output 3

console.log(doSomething(undefined, 1, 2, 3);           // output 6

console.log(doSomething(undefined, 1, 2, 3, 4, 5);   // output 15    
```

Spread Operator 

This operator (…) which is similar to the rest parameters mentioned above, but the reverse. This operator allows an iterable to fill all parameters within a function. 

```
function sum(x, y, z){

  return x + y + z;

}


const numbers = [1, 2, 3];


console.log(sum(...numbers));                   // output: 6


console.log(sum.apply(null, numbers));   // output: 6
```

Generics 

If functionality can be made generic then this function should be included within an associated public JS module that can be used by other modules giving this generic function easily accessed round the system, generic functionality prevents re-writing the same/similar code and allows its robust process to be used in most situations relating to the desired goal of the functionality.

- String Literals 
- Use Single Quotes
- String literals should be defined with a single quote notation(’) instead of the double quote notation(”) as this was the original way of defining the literal. If the string literal contains a single quote character, use a template string to stop the issue of ending the string literal. String literals should not extend over multiple lines.
Good Practice:

```
let string = 'This is a string';
```

Bad Practice:

```
let string = "This is a string";
```

Template Literals 

Template literals are defined with the backtick and are used to allow embedded expressions into the strings, these can expand multiple lines and are very useful for simplifying code. Example:

```
function arithmetic(a, b){

  return `Here is a table of arithmetic operations:

${a} + ${b} = ${a + b}

${a} - ${b} = ${a - b}

${a} * ${b} = ${a * b}

${a} / ${b} = ${a / b}`;

}
```

// Or like…

```
return `This is the variable: ${variable}`;
```

No Line Continuations 

Line continuations are used within strings to break onto new lines, this is an old practice and now should not be used. Instead the string should be broken into certain parts and displayed like so:

```
// Do Not

const longString = 'This is a very long string that far exceeds the 80 \

    column limit. It unfortunately contains long stretches of spaces due \

    to how the continued lines are indented.';
    


// Do, Instead 


const longString = 'This is a very long string that far exceeds the 80 ' +

    'column limit. It does not contain long stretches of spaces since ' +

    'the concatenated strings are cleaner.';
```

Number Literals

Numbers can be specified in any base structure represented by lower-case letters. Never include leaving 0s. 

### Control Structures 

For Loops
After the introduction to ES6, there are now 3 different kind of for loops.

For-In

for…in statements are used for iterating over properties of an object that are keyed by string values.

```
const object = { a: 1, b: 2, c: 3 };

for (const property in object){

  console.log(`${property}: ${object[property]}`);

}
```

For-Of

for…of statements are used for iterating over properties from an initerable object like objects or arrays.

```
const array1 = ['a', 'b', 'c'];


for (const element of array1){

  console.log(element);

}
```
for…of and Object.Keys  should be preferred over for-in when possible.

For

for statements are used for initiating over any collection of data that can be initerated over although Object.Keys would be preferred when dealing with objects that have numerable keys. For statements are specially handy when using the initiator. 

Exceptions 

Exceptions are a very important part of JavaScript and should be used when exceptional circumstances occur. When throwing errors the Error object should always be used or subclasses of Error with the new syntax.

Note: Custom exceptions should be used where possible to transfer the error so that the error doesn’t break the program and additional information can be passed into the exception about the error.

```
try{

	…

} catch(e){

	Console.log(e); // log error

}
```

Empty Catch Blocks 

Empty catch blocks should be only used when passing error need no following actions. If an error needs to be ignored(Please note errors should rarely be silenced as they can cause other issues) then empty catch blocks can be used but commented are required in the block to show the readers what’s happening, why the error is being silenced and why no following actions are required.
Switch Statements 

The general syntax of a switch statement, the default  switch is required as if all switches fall through an else would be the best solution.

```
switch (input){

  case 1:

  case 2:

    prepareOneOrTwo();

  	// fall through

  case 3:

    handleOneTwoOrThree();

    break;

  default:

    handleLargeNumber(input);

}
```

This

The keyword this should never be used to reference something that’s not scoped/global. this should only be used to reference current object or class definitions and can be used to break out of scope using arrow functions.
Equal Checks 

If the type of both variables being compared are the same, use identity checks which will help computer performance, this is because normal comparing operators(==, !==) will loop over all types before comparing the values but identity operators(===, !==) will only compare their values as the types are expected to be the same.

Naming

Rules Common To All Identifiers 

Naming variables, function, ect within JS modules should be as descriptive as possible and should always be alphanumeric and lower camel case, This excluding class, file names.  Very rarely a framework like Angular might require a dollar sign. Examples:

```
	nameOne

	thisIsAnotherName

	misunderstood
```

Rules By Identifier Type

Package Names

Package Names should always be lower camel case.

Class Names

Class Names should always be upper camel case, this includes class like structures like interface. interface names should normally be adjectives or an adjective.

Method Names

Function Names are always written in lower camel case, these names are normally verbs or a verb phrase which describes what the method does(e.g. sendMessage or add).

Underscores may appear in JavaScript unit tests test names to separate logical components, there is no right way for naming test methods.

Constant Names

Constant names should use CONSTANT_CASE which is all upper case letters separated by underscores(_).  Constant names are typically nouns or noun phases. 

Local Aliases And References 

JavaScript’s primitive types are passed by values by objects are passed by reference, passing variable references can be done by converting this to an object with that value.  Constants in function scopes should be lower camel case.

```
// declare an object with property x

var obj = { x: 1 };

var aliasToObj = obj;

aliasToObj.x ++;

alert( obj.x ); // displays 2
```

Note: Aliases must be const.

None Constant Field Names

All None-Constant field names should be lower camel case, these names are typically nouns or noun phases that describe what values they hold.

Parameter Names

All parameter names should be written in lower camel case, this should also be the case in the parameter is expecting a constructor value. A single char should not be used as a parameter name like e for error.

Local Variable Names

Local variable names are written in lower camel case except module-local constants which should be CONSTANT case.

Template Parameter Names

Template parameter names should be concise and kept short but descriptive, these parameters should be all capital letters.

Module-Local Names

Local names that are exported are considered private, this includes:

- Classes
- Functions 
- Variables
- Module-Local Constants  

And other module-local identifiers should follow the same rule sets.

### JavaScript Modules 

Markdown

JavaScript Modules are written in markdown and sometimes includes HTML where necessary. 

Note: some JavaScript tools might ignore plain text formatter so this should be considered depending what formatter you are using.

JSDoc Tags And Annotations

JSDoc is a markup language used to annotate JavaScript Modules. Each Javascript Doc tag should have its own line with the tag following an explanation. Example of how annotations should look throughout JavaScript modules:

```
/**

 * Place more complex annotations (like "implements" and "template")

 * on their own lines.  Multiple simple tags (like "export" and "final")

 * may be combined in one line.

 * @export @final

 * @implements {Iterable<TYPE>}

 * @template TYPE

 */

class MyClass {

  /**

   * @param {!ObjType} obj Some object.

   * @param {number=} num An optional number.

   */

  constructor(obj, num = 42) {

    /** @private @const {!Array<!ObjType|number>} */

    this.data_ = [obj, num];

  }

}
```

### Policies  

Complier Warnings 

Standard Warning Set

For standards development environments, complier warning are required to prevent issues happening before the project can run. These warning should indicate what and where the error is and what is causing it, most code editors will reply on CI/CD tools to perform most of the development workflow.

Supress Warnings 

Supressing warning should be very rare and only done when controller and a general understanding of the issue is covered. Suppressing issues can cause other issues and should only be done for temporary fixes until a solution can be applied.

Deprecation 

Any Deprecated method, class, interface or more should be marked with the annotation @deprecated. If deprecated aspects of a JavaScript module have either been deprecated for a while or even just useless, removing these will clean code up and prevent reading deprecated methods for newer solutions.

- Frameworks 
- Mithril

JSX

JSX is a syntax extension that comes with the mithril installation which allows the writer to use mithril functions to write HTML with distributed JavaScript, this functionality is not required for best coding standards but has been put into place to allow a easier flow for building views with HTML.

Example:

```
function MyComponent() {

    return {

        view: () => (

            <main>

                <h1>Hello world</h1>

            </main>

        )

    }

}

// can be written as…

function MyComponent() {

    return {

        view: () =>

            m("main", [

                m("h1", "Hello world"),

            ])

    }

}
```

Javascript expressions can be included within JSX tags by using curly({ … }) braces like so:

```
	{variable}
```

JSX tags can include methods, styles, attributes and more. Components can be rendered with this syntax by using upper camel case to include the Javascript modules component.

```
m(ListComponent);
```

ES6+ On Legacy Browsers

MitrhilJS was originally written in ES5 however is now fully compatible with ES6+, imports should be done by the modules url path and not using the Nodes Magic Module Resolution. As most modern browsers support ES6+, some old browser might not like internet explorer, thus meaning ES5 content should only be used. 

Animation

During modern development, amination is normally used to make application seem more alive while having moving and changing features drawing readers attention and is a good practice to use to style application features. MithrilJS has many external options to achieve rich complex animations. Example of CSS animation: 

```
// css | scss | styling

.fancy {animation:fade-in 0.5s;}

@keyframes fade-in {

    from {opacity:0;}

    to {opacity:1;}

}


var FancyComponent = {

    view: function() {

        return m(".fancy", "Hello world")

    }

}


m.mount(document.body, FancyComponent);
```

Important: when creating animations with CSS, it is important just to use the styles opacity and transform rules which can be hardware-accelerated with modern browsers and shouldn’t affect the applications performance unlike other CSS  rules which could have a huge impact on the applications performance.

Key Concepts 

VNodes

Virtual DOM trees are data-structure representations of actual DOM trees which includes virtual nested DOM nodes and are referenced within mithril as vnodes. Mithril re-builds the DOM on every render cycle making DOM manipulations should be minimized by using virtual nodes instead:

```
// define a component

var ExampleComponent = {

    view: function(vnode) {

        return m("div", vnode.attrs, ["Hello ", vnode.children])

    }

}


// consume it

m(ExampleComponent, {style: "color:red;"}, "world")
```

Components 

Always write mithrils view components in a view function.

Note: Any Javascript object that contains the view method is a mithril component. This doesn’t have to be on another module. 

```
    view: function(vnode) {

        return m("div", vnode.attrs, ["Hello ", vnode.children])

    }
```

Lifecyle Methods 

Components can have additional lifecycle methods defined when declared as a vnode type like so:

```
function initialize(vnode) {

    console.log("initialized as vnode")

}

m(ComponentWithHooks, {oninit: initialize})


// or…

m(ComponentWithHooks, {onsubmit: () => initialize})

```

Note: lifecycle methods run like async methods and don’t overlap, they run after the previous `vnode` method has finished.

Keys

Make use of mithrils component key attribute as they can be especially useful for defining unique attribute which can be used to get the specific component.

```
	{key: variable}
```

Auto Redraw System

The auto redraw system has three main functions that allows the developer to fast render and render the DOM. This also occurs on state data manipulates, component state changes and after a components event handlers have finished their process:

```
var MyComponent = {

    view: function() {

        return m("div", {onclick: doSomething})

    }

}


function doSomething() {

    // a redraw happens synchronously after this function runs

}


m.mount(document.body, MyComponent)
```

The three function mithril providers for controller the rendering the application are:

- m.mout
- m.route
- m.router

Path handling

Generally there are two types of paths for retrieving different aspects of an application like data, pages and components. Theses types are labelled as so:

    Raw Paths - These paths are normally just strings that directly link to an external asset from the current Javascript module.
    Parameterized Paths - These types of paths allow the developer to insert variables/values into the path allowing to pass information between pages. 


Uncertain Standards 

Class Attributes *

Mentioned in a few sources online, underscores(_) should follow after private class attribute name declarations however we haven’t seen any clear evidence of this on pre-any existing iBe code. Please see references for details.

General Terminology 

This

Note: Please see Object Literals / Method Shorthand for a better explanation of how var self = this can be avoided.

this object is runtime bounded to the current objects or classes scope and can differ between meaning depending on the scenario. this should never be assigned to a variable instead Method Shorthand should be used. 
Avoid doing this:

```
	let self = this;

	let a = ‘Got A!’;

	function(){

		console.log(self.a); //	this would output “Got A!”					

    }
```

And replace with this:

```
	let a = ‘Got A!’;

	let doSomething = () => {

		console.log(this.a); //	this would output “Got A!”	

	}

	doSomething();
```

Simplifying Code

Adding multiple event listeners 

Multiple events can be added to a DOM element without having to list every event and add them separately. This is done by looping over an array that contains all events needed to be added to a DOM element.
Original 

```
element.addEventListener(‘click’, () => doSomething());

element.addEventListener(‘touchstart’, () => doSomething());

element.addEventListener(‘mousedown’, () => doSomething());
```

Simplified 

```
	[‘click’, ‘touchstart’, ‘mousedown’].forEach(

event => element.addEventListener(event, doSomething());
```

## Appendices 

### References

Javascript Standards 

[2021] - https://google.github.io/styleguide/jsguide.html

[2021] - https://dev.to/johnwolfe820/should-you-never-truly-use-var-bdi

[2021] - https://stackoverflow.com/a/52395969

[2021] - https://stackoverflow.com/a/6307570

[2021] - https://www.geeksforgeeks.org/javascript-rest-operator/

[2021] - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax

[2021] - https://stackoverflow.com/a/1687019

Mithril Standards 

[2021] - https://mithril.js.org/

