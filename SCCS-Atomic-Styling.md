# Atomic Styling

Used by Bootstrap and more, Atmoic Styling is a techique of having small descriptive classes that can be used in-line with elements across a codebase so each element doesnt have their own class which can have re-written code that applies to another element.

A benefical example of using atmoic-styling using flex:

```
# atmoic.scss

.row{
  display: flex;
  flex-direction: row;
}

.col{
  display: col;
  flex-direction: col;
}

. align-center{
  align-items: center;
}

.jusify-center{
  justify-content: center;
}

.justify-sb{
  justify-content: space-between;
}

.justify-fs{
  justify-content: flex-start;
}

.justify-fe{
  justify-content: flex-end;
}

// display items center row

<div class="row align-center justify-center">
  <button>btnOne</button>
  <button>btnOne</button>
  <button>btnOne</button>
</div>

// will display

--------------------------------
|                              |
|              XXX             |
|                              |
--------------------------------

// display items to the center-right

<div class="row align-center justify-fe">
  <button>btnOne</button>
  <button>btnOne</button>
  <button>btnOne</button>
</div>

// will display

--------------------------------
|                              |
|                          XXX |
|                              |
--------------------------------

```

# Variables 

Within cacading style sheets we cane add variables to make classes more generic. For exmaple we can have a combine atmoic styling practice with variables to make a reuseable, generic class:

```
.width#{$width}{
  width: $width;
}

.height#{$height}{
  height: $height;
}

// using different types 
<div class="height100px"></div>
<div class="height100%"></div>

.size#{$size}{
  min-width: $size;
  max-width: $size;
  min-height: $size;
  max-height: $size;  
}

<div class="size100px"></div>

```


# Loops 

```
// todo ...
```
