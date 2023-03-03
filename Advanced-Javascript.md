# Javascript Cheat Sheet

## Variable To Boolean

Turning a variable to a boolean expression can easily be done by using the shorthand (`!!`) syntax. This allows variables to be turned into boolean expressions.

**Example:**

`(!!variable) ? doSomething() : doSomethingElse()`

The expression above, tests if the variable `variable` is undefined or not by turning returning true if populated and false if undefined or false;

## Clang Formatter

Clang-Formatter is a coding fomatter for C# and is used to format and orangise code automatically. Using Clang-Formate for Javascript is considered good pratice for organising code and prevents version/source control overriding commits due to changes in code styles and indentations. Clang-Format can be added to many code editors and has many save options. For good pratice, format on save helps format regularly.      

**Reference:** - https://llvm.org/

## Find all unique items within an array 

```
var scores = [12, 12, 5, 3, 5, 6, 6];
let res = [];

scores.forEach(score => {
  var x = score;
  var index = scores.indexOf(x);  
  
  if(index !== -1){
    // remove the item
    scores.splice(index, 1);
  }
  
  if(!scores.includes(x)){
    res.push(x);
  } else {    
    index = scores.indexOf(x);   
    if(index !== -1){
      // remove the item
      scores.splice(index, 1);
    } 
  }     
});

console.log(res); 
```
