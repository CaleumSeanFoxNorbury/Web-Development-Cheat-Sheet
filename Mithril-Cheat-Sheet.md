# Mithril 

JavaScript framework for building frontend web-components.

## Quick Start With Webpack Installaton 

Mithril can be installed to JavaScript application by initalising the application as an NPM module and installing the packages through that manager.

```
npm init --yes
npm install mithril --save
npm install webpack webpack-cli --save-dev
```

Add a run entry script `package.json`

```
{
 // ...
 "scripts": {
     "start": "webpack src/index.js --output bin/app.js -d --watch"
 }
}
```

render body of the mithril components within `src/index.html`

```
import m from "mithril";
m.render(document.body, "hello world");
```

create applications entry point in `index.html`

```
<!DOCTYPE html>
<body>
 <script src="bin/app.js"></script>
</body>
```

## Syntax 

### vnodes

virtual nodes are nodes from a virtual DOM tree which acts similar to a schema of the actual DOM tree and its nodes. VNodes can be created easily with the `m()` function. 

```
  vnode = m(selector, attrs, children)
```

**Example:**

```
  m('div', {style: 'height: 200px'}),
          
  m(Button, {
    className: 'have-a-nice-day',
    onclick: () => { m.route.set('#') },
    fill: true
  }, 'Have a nice day!'),
          
  m('div', 'Have a nice day!'),
```
