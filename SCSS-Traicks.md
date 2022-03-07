## Animation 

### Transformation 

Transformaton is one of a few that uses a reasonable amount of reasources when applied to elements on runtime or whem manipulating the style attributes. Transformation has many properties that allow 3D transformations of an element including rotate scale and more.

**Scale** 

```
  transform: scale(2)
```

Scale transforms an obejcts size with a given parmater.

## Display And Hidden

Using `visibility: hidden` and `display: none` have similar visual propeties, however behind the scenes both style classes have very different properties.

### Hidden Visability

Using `visibility: hidden` only changes the visability of the element and is still visible to the browser and the still exists in the DOM. The element is hidden visiblity properties also takes up the same amount of space and in the same place and follows the same process as if it wasnt visible.

### Display None 

Using `display: none` removes the element altogether from the DOM as because of this the browser will not render or see this, this technique used is best for removing elements that are no longer needed, the element is not permanently gone and can be retrieved back with other `display` properties. 

**Reference:** - https://www.thoughtco.com/display-none-vs-visibility-hidden-3466884
