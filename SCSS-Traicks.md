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

### Tricks and Object Styles

## Fade Gradient 

For fading, like when overflow had been hidden buit extend functionality is present we can represent this to the user as contents fade out.

```
.fade-gradient {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 31px;
  background: linear-gradient(to bottom, rgba(255, 255, 255, 0), rgba(255, 255, 255, 1));
  z-index: 900;
}
```

## Relative and absolute positioning 

We may need both benefits of positioning types and this can be done by embeddeding both styles.

```
`<div id="success-badge" style="position: absolute; overflow: visible;">
    <div style="position: relative; bottom: 27px; left: ${($(card).width() / 2) + 20}px">
         <div style="background-color: white; border: 1px solid lime; padding: 5px; border-radius: 50px;">
             <i style="color: lime; padding-left: 2px; padding-right: 2px;" class="fas fa-check" </i>
         </div>
    </div>
</div>`
```

# block fixes for different size texts

```
/* Option 1: Prevent text wrapping and maintain single line */
.tfc-oc-grid-btn .elementor-button-text {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.tfc-oc-grid-btn .elementor-button-content-wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
  min-height: 50px; /* Adjust as needed */
}

/* Option 2: Allow wrapping but maintain proper alignment */
.tfc-oc-grid-btn .elementor-button-content-wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
  min-height: 60px; /* Increase to accommodate wrapped text */
  gap: 10px;
}

.tfc-oc-grid-btn .elementor-button-text {
  flex: 1;
  line-height: 1.2;
}

.tfc-oc-grid-btn .elementor-button-icon {
  flex-shrink: 0; /* Prevent icon from shrinking */
  align-self: flex-start; /* Align icon to top when text wraps */
  margin-top: 4px; /* Fine-tune vertical alignment */
}

/* Option 3: Use smaller font size for longer text */
.tfc-oc-grid-btn .elementor-button-text {
  font-size: clamp(12px, 2.5vw, 14px); /* Responsive font size */
  line-height: 1.3;
}

.tfc-oc-grid-btn .elementor-button-content-wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 8px 12px;
}

/* Option 4: Center multi-line text vertically */
.tfc-oc-grid-btn .elementor-button-content-wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
  min-height: 60px;
}

.tfc-oc-grid-btn .elementor-button-text {
  display: flex;
  align-items: center;
  flex: 1;
  text-align: left;
  line-height: 1.3;
}

/* Option 5: Make all buttons the same height */
.tfc-oc-grid-btn .elementor-button {
  height: 70px; /* Fixed height for all buttons */
  display: flex;
  align-items: center;
}

.tfc-oc-grid-btn .elementor-button-content-wrapper {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  padding: 0 15px;
}

.tfc-oc-grid-btn .elementor-button-text {
  flex: 1;
  line-height: 1.2;
  padding-right: 10px;
}

.tfc-oc-grid-btn .elementor-button-icon svg {
  width: 25px; 
  height: 25px;
}

```

### Clamp

Resize based on scale of the viewport, with standardised size values.

***Example using h tags ***

```
h1 {
    font-size: clamp(24px, 4vw, 32px);
}
h2 {
    font-size: clamp(20px, 3vw, 24px);
}
h3 {
    font-size: clamp(16px, 2.5vw, 18px);
}

```

