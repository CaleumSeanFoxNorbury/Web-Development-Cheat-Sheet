# Advanced Typescript 

### Satisifies operator

The `satisifies` operator can compare a value or expression against a type without actually decalring or changing the resulting type of the expression or value.

**Setting expression/value type**

```
type Colors = "red" | "green" | "blue";

type RGB = [red: number, green: number, blue: number];

const palette: Record<Colors, string | RGB> = {
    red: [255, 0, 0],
    green: "#00ff00",
    bleu: [0, 0, 255]
//  ~~~~ The typo is now correctly detected but palette has now had a set type
};

// But we now have an undesirable error here - 'palette.red' "could" be a string.
const redComponent = palette.red.at(0);
```

**Satisfies expression/value by comparing with type**

```
type Colors = "red" | "green" | "blue";

type RGB = [red: number, green: number, blue: number];

const palette = {
    red: [255, 0, 0],
    green: "#00ff00",
    bleu: [0, 0, 255]
//  ~~~~ The typo is now caught!
} satisfies Record<Colors, string | RGB>;

// Both of these methods are still accessible!
const redComponent = palette.red.at(0);
const greenNormalized = palette.green.toUpperCase();
```

These checks are very useful for when a value can be several types. **Example:**

```
interface ExampleNumbers {
   numberOne: 1,
   numberTwo: 2,
   numberThree: 3
}

let x: Number|ExampleNumbers;

function getNumbers(){
    return 'x';
}

function getNumber(){
    return 5;
}

if(...){
    x = getNumber() satisfies Number;  
} else {
    x = getNumbers() satisfies ExampleNumbers;
}
```

### Recursive type aliases.

// todo 

### Top-level await.

**Example:**

```
async function main(): Promise<void> {
  // await ...
}

main().catch(console.error);
```
(ref: https://typescript.tv/new-features/top-level-await-in-typescript-3-8/)

### Null coalescing.

// todo

### Unlisted property narrowing with the `in` operator 

While using the `in` operator we can now narrow down its type when a key value has been specified within a value with several types.

**Example:**

```
interface Colour {
    red: number;
    green: number;
    blue: number;
}

interface Attrs {
    stalk: number;
    pettle: number;
    leaf: number;
}

// old way ...
function x(obj : Colour|Attrs){
    if (let stalk in (<Attrs>obj)) { // defining its type first
        // 'stalk' now has the type Attrs
    }
}

// new way ...
function x(obj : Colour|Attrs){
    if ("stalk" in obj) { // "stalk" its of type "Attrs" narrowing its type
        // 'stalk' now has the type Attrs
    }
```

**Referneces:**

[2023] https://devblogs.microsoft.com/typescript/announcing-typescript-4-9/
