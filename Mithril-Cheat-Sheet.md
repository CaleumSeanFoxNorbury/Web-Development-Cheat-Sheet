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
          
  m(Component, {
    className: 'have-a-nice-day',
    callback: () => { m.route.set('#') },
    attr: true
  }, 'Have a nice day!'),
          
  m('div', 'Have a nice day!'),
```

## Skeletons

Blank templates for easy setup and fast coding. These are basic and usually dont contain all resources.

### Component Skeleton 

```
// scss imports ...
import './style.scss'

// module and component imports ...
import m from 'mithril';

export default function Dashboard(): m.Component {
  // global component code ...
  const res: m.Component = {
    oncreate() {
      // runs after the DOM element is created and attached to the document
    },
    view() {
      // containerized view code ...
      return m('div');
      // return the vuew
    }
  };

  return res;
}
```

## Generic Page Content

Generic page content can be be used to have keep related content together in the same file. Compoennt `attrs` can be used to gather url parameters which can condition which view to use.
