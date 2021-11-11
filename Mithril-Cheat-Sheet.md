# Mithril 

JavaScript framework for building frontend web-components.

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
