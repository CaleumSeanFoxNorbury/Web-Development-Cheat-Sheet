# Bubble Example  


## Basic Bubble UI

### HTML 

```
<div class="main-circle">
  56%
</div>
```

### CSS 

```
  .main-circle {
    position: relative;
    width: 100px;
    height: 100px;
    border: 2px solid black;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .small-circle {
    position: absolute;
    width: 20px;
    height: 20px;
    border: 1px solid black;
    border-radius: 50%;
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 12px;
    z-index: 999;
    background-color: 
  }
```

### JS

```
function calculatePosition(percentage) {
  var center_x = 50; // Adjusted to the center of the main circle
  var center_y = 50; // Adjusted to the center of the main circle
  var radius = 50; // Adjusted to half of the main circle's size

  var angleInRadians = (-percentage * 2 * Math.PI) + (Math.PI / 2);
  var x = center_x + radius * Math.cos(angleInRadians);
  // Use subtraction for y-coordinate to reverse direction
  var y = center_y - radius * Math.sin(angleInRadians);

  return { left: x, top: y };
}

function createSmallCircle(mainCircle, smallCircles, percentage) {
  const { left, top } = calculatePosition(percentage);

  const smallCircle = document.createElement('div');
  smallCircle.className = 'small-circle';
  smallCircle.style.left = left + 'px';
  smallCircle.style.top = top + 'px';
  smallCircle.textContent = '1/0'; // Replace with your content

  document.body.appendChild(smallCircle);
  smallCircles.push(smallCircle);
}

const mainCircle = document.querySelector('.main-circle');
const smallCircles = [];

// Create multiple smaller circles
for (let i = 0; i < 8; i++) {
  createSmallCircle(mainCircle, smallCircles, i / 8);
}
```

### View 

![image](https://github.com/CaleumSeanFoxNorbury/Web-Development-Cheat-Sheet/assets/33324819/65d8e94e-0444-439d-877d-6cc92a45f6ca)
