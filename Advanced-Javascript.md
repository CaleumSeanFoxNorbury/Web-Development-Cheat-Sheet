# Javascript Cheat Sheet

## Variable To Boolean

Turning a variable to a boolean expression can easily be done by using the shorthand (`!!`) syntax. This allows variables to be turned into boolean expressions.

**Example:**

`(!!variable) ? doSomething() : doSomethingElse()`

The expression above, tests if the variable `variable` is undefined or not by turning returning true if populated and false if undefined or false;

## Clang Formatter

Clang-Formatter is a coding fomatter for C# and is used to format and orangise code automatically. Using Clang-Formate for Javascript is considered good pratice for organising code and prevents version/source control overriding commits due to changes in code styles and indentations. Clang-Format can be added to many code editors and has many save options. For good pratice, format on save helps format regularly.      

**Reference:** - https://llvm.org/

## Arrays 

### Find all unique items within an array 

The below statement works by first filtering duplicates and none duplicates into their own arrays that is returned by `.filter`; then filtering each array if their length is equal to `1` meaning no duplicates.

`chars.filter(y => x === y)` returning an array for each value including their duplciates. Filtering this value by checking each arrays length against `1` will remove all arrays with duplicates. 

```
let chars = ['A', 'B', 'A', 'C', 'B'];
let nonDuplicates = chars.filter(x => chars.filter(y => x === y).length === 1)

console.log(nonDuplicates);
```
