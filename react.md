
## basic types
{{ ::cards-header:: }}

### Components

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
```

```jsx
class Hello extends React.Component {
  render () {
    return <div className='message-box'>
      Hello {this.props.name}
    </div>
  }
}
```

```jsx
const el = document.body
ReactDOM.render(<Hello name='John' />, el)
```

Use the [React.js jsfiddle](http://jsfiddle.net/reactjs/69z2wepo/) to start
use (or the unofficial [jsbin](http://jsbin.com/yafixat/edit?js,output))

{{ ::card-item:: }}

### Properties

```html
<Video fullscreen={true} />
```

```jsx
render () {
  this.props.fullscreen
  ···
}
```

Use `this.props` to access properties passed to the component.

See: [Properties](https://reactjs.org/docs/tutorial.html#using-props)

{{ ::card-item:: }}

### States

```jsx
this.setState({ username: 'rstacruz' })
```

```jsx
render () {
  this.state.username
  ···
}
```

Use states (`this.state`) to manage dynamic data.

See: [States](https://reactjs.org/docs/tutorial.html#reactive-state)

{{ ::card-item:: }}

### Nesting

```jsx
class Info extends React.Component {
  render () {
    const { avatar, username } = this.props

    return <div>
      <UserAvatar src={avatar} />
      <UserProfile username={username} />
    </div>
  }
}
```

Nest components to separate concerns.

See: [Composing Components](https://reactjs.org/docs/components-and-props.html#composing-components)

{{ ::card-item:: }}

### Children

```jsx
<AlertBox>
  <h1>You have pending notifications</h1>
</AlertBox>
```

```jsx
class AlertBox extends React.Component {
  render () {
    return <div className='alert-box'>
      {this.props.children}
    </div>
  }
}
```

Children are passed as the `children` property.

{{ ::group:: }}
## Defaults
{{ ::cards-header:: }}

### Setting default props

```jsx
Hello.defaultProps = {
  color: 'blue'
}
```

See: [defaultProps](https://reactjs.org/docs/react-component.html#defaultprops)

{{ ::card-item:: }}
### Setting default state

```jsx
class Hello extends React.Component {
  constructor (props) {
    super(props)
    this.state = { visible: true }
  }
}
```

Set the default state in the `constructor()`.

See: [Setting the default state](https://reactjs.org/docs/react-without-es6.html#setting-the-initial-state)

{{ ::group:: }}
## Other components
{{ ::cards-header:: }}

### Function components

```jsx
function MyComponent ({ name }) {
  return <div className='message-box'>
    Hello {name}
  </div>
}
```

Functional components have no state. Also, their `props` are passed as the first parameter to a function.

See: [Function and Class Components](https://reactjs.org/docs/components-and-props.html#functional-and-class-components)

{{ ::card-item:: }}
### Pure components

```jsx
class MessageBox extends React.PureComponent {
  ···
}
```

Performance-optimized version of `React.Component`. Doesn't rerender if props/state hasn't changed.

See: [Pure components](https://reactjs.org/docs/react-api.html#react.purecomponent)

{{ ::card-item:: }}

### Component API

```jsx
this.forceUpdate()
```

```jsx
this.setState({ ... })
```

```jsx
this.state
this.props
```

These methods and properties are available for `Component` instances.

See: [Component API](http://facebook.github.io/react/docs/component-api.html)

{{ ::group:: }}
## Lifecycle
{{ ::cards-header:: }}

### Mounting

| Method | Description |
| --- | --- |
| `constructor` _(props)_ | Before rendering [#](https://reactjs.org/docs/react-component.html#constructor) |
| `componentWillMount()` | _Don't use this_ [#](https://reactjs.org/docs/react-component.html#componentwillmount) |
| `render()` | Render  [#](https://reactjs.org/docs/react-component.html#render) |
| `componentDidMount()` | After rendering (DOM available) [#](https://reactjs.org/docs/react-component.html#componentdidmount) |
| --- | --- |
| `componentWillUnmount()` | Before DOM removal [#](https://reactjs.org/docs/react-component.html#componentwillunmount) |
| --- | --- |
| `componentDidCatch()` | Catch errors (16+) [#](https://reactjs.org/blog/2017/07/26/error-handling-in-react-16.html) |

Set initial the state on `constructor()`.
Add DOM event handlers, timers (etc) on `componentDidMount()`, then remove them on `componentWillUnmount()`.

{{ ::card-item:: }}

### Updating

| Method | Description |
| --- | --- |
| `componentWillReceiveProps` *(newProps)* | Use `setState()` here |
| `shouldComponentUpdate` *(newProps, newState)* | Skips `render()` if returns false |
| `componentWillUpdate` *(newProps, newState)* | Can't use `setState()` here |
| `render()` | Render |
| `componentDidUpdate` *(prevProps, prevState)* | Operate on the DOM here |

Called when parents change properties and `.setState()`. These are not called for initial renders.

See: [Component specs](http://facebook.github.io/react/docs/component-specs.html#updating-componentwillreceiveprops)

{{ ::group:: }}
## DOM nodes
{{ ::cards-header:: }}

### References

```jsx
class MyComponent extends React.Component {
  render () {
    return <div>
      <input ref={el => this.input = el} />
    </div>
  }

  componentDidMount () {
    this.input.focus()
  }
}
```

Allows access to DOM nodes.

See: [Refs and the DOM](https://reactjs.org/docs/refs-and-the-dom.html)

{{ ::card-item:: }}
### DOM Events

```jsx
class MyComponent extends React.Component {
  render () {
    <input type="text"
        value={this.state.value}
        onChange={event => this.onChange(event)} />
  }

  onChange (event) {
    this.setState({ value: event.target.value })
  }
}
```

Pass functions to attributes like `onChange`.

See: [Events](https://reactjs.org/docs/events.html)

{{ ::group:: }}
## Other features
{{ ::cards-header:: }}

### Transferring props

```html
<VideoPlayer src="video.mp4" />
```

```jsx
class VideoPlayer extends React.Component {
  render () {
    return <VideoEmbed {...this.props} />
  }
}
```

Propagates `src="..."` down to the sub-component.

See [Transferring props](http://facebook.github.io/react/docs/transferring-props.html)

{{ ::card-item:: }}

### Top-level API

```jsx
React.createClass({ ... })
React.isValidElement(c)
```

```jsx
ReactDOM.render(<Component />, domnode, [callback])
ReactDOM.unmountComponentAtNode(domnode)
```

```jsx
ReactDOMServer.renderToString(<Component />)
ReactDOMServer.renderToStaticMarkup(<Component />)
```

There are more, but these are most common.

See: [React top-level API](https://reactjs.org/docs/react-api.html)


{{ ::group:: }}
## JSX patterns
{{ ::cards-header:: }}

### Style shorthand

```jsx
var style = { height: 10 }
return <div style={style}></div>
```

```jsx
return <div style={{ margin: 0, padding: 0 }}></div>
```

See: [Inline styles](https://reactjs.org/tips/inline-styles.html)

{{ ::card-item:: }}

### Inner HTML

```jsx
function markdownify() { return "<p>...</p>"; }
<div dangerouslySetInnerHTML={{__html: markdownify()}} />
```

See: [Dangerously set innerHTML](https://reactjs.org/tips/dangerously-set-inner-html.html)

{{ ::card-item:: }}

### Lists

```jsx
class TodoList extends React.Component {
  render () {
    const { items } = this.props

    return <ul>
      {items.map(item =>
        <TodoItem item={item} key={item.key} />)}
    </ul>
  }
}
```

Always supply a `key` property.

{{ ::card-item:: }}

### Conditionals

```jsx
<div>
  {showMyComponent
    ? <MyComponent />
    : <OtherComponent />}
</div>
```
{{ ::card-item:: }}

### Short-circuit evaluation

```jsx
<div>
  {showPopup && <Popup />}
</div>
```

{{ ::group:: }}
## New features
{{ ::cards-header:: }}

### Returning fragments

```js
render () {
  // Don't forget the keys!
  return [
    <li key="A">First item</li>,
    <li key="B">Second item</li>
  ]
}
```

You can return multiple nodes as arrays.

See: [Fragments and strings](https://reactjs.org/blog/2017/09/26/react-v16.0.html#new-render-return-types-fragments-and-strings)

{{ ::card-item:: }}
### Returning strings

```js
render() {
  return 'Look ma, no spans!';
}
```

You can return just a string.

See: [Fragments and strings](https://reactjs.org/blog/2017/09/26/react-v16.0.html#new-render-return-types-fragments-and-strings)

{{ ::card-item:: }}

### Errors

```js
class MyComponent extends React.Component {
  ···
  componentDidCatch (error, info) {
    this.setState({ error })
  }
}
```

Catch errors via `componentDidCatch`. (React 16+)

See: [Error handling in React 16](https://reactjs.org/blog/2017/07/26/error-handling-in-react-16.html)

{{ ::card-item:: }}

### Portals

```js
render () {
  return React.createPortal(
    this.props.children,
    document.getElementById('menu')
  )
}
```

This renders `this.props.children` into any location in the DOM.

See: [Portals](https://reactjs.org/docs/portals.html)

{{ ::card-item:: }}

### Hydration

```js
const el = document.getElementById('app')
ReactDOM.hydrate(<App />, el)
```

Use `ReactDOM.hydrate` instead of using `ReactDOM.render` if you're rendering over the output of [ReactDOMServer](https://reactjs.org/docs/react-dom-server.html).

See: [Hydrate](https://reactjs.org/docs/react-dom.html#hydrate)

{{ ::group:: }}
## Property validation
{{ ::cards-header:: }}

### PropTypes

```js
import PropTypes from 'prop-types'
```

See: [Typechecking with PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html)

#### Basic

| type | Description |
| --- | --- |
| `any`                     | Anything                             |
| `string`                  | String                                 |
| `number`                  | Number                                 |
| `func`                    | Function                             |
| `bool`                    | True or false                        |

#### Enum

| type | Description |
| --- | --- |
| `oneOf`_(any)_            | Enum types                           |
| `oneOfType`_(type array)_ | Union                                |

#### Array

| type | Description |
| --- | --- |
| `array`                   | Array                                |
| `arrayOf`_(...)_          | ---                                  |

#### Object

| type | Description |
| --- | --- |
| `object`                  |                                      |
| `objectOf`_(...)_         | Object with values of a certain type |
| `instanceOf`_(...)_       | Instance of a class                  |
| `shape`_(...)_            |                                      |

#### Elements

| type | Description |
| --- | --- |
| `element`                 | React element                        |
| `node`                    | DOM node                             |

#### Required

| type | Description |
| --- | --- |
| `(···).isRequired`        | Required                             |

{{ ::card-item:: }}
### Basic types

```jsx
MyComponent.propTypes = {
  email:      PropTypes.string,
  seats:      PropTypes.number,
  callback:   PropTypes.func,
  isClosed:   PropTypes.bool,
  any:        PropTypes.any
}
```
{{ ::card-item:: }}
### Required types

```jsx
MyCo.propTypes = {
  name:  PropTypes.string.isRequired
}
```

{{ ::card-item:: }}

### Elements

```jsx
MyCo.propTypes = {
  // React element
  element: PropTypes.element,

  // num, string, element, or an array of those
  node: PropTypes.node
}
```

{{ ::card-item:: }}

### Enumerables (oneOf)

```jsx
MyCo.propTypes = {
  direction: PropTypes.oneOf([
    'left', 'right'
  ])
}
```

{{ ::card-item:: }}

### Arrays and objects

```jsx
MyCo.propTypes = {
  list: PropTypes.array,
  ages: PropTypes.arrayOf(PropTypes.number),
  user: PropTypes.object,
  user: PropTypes.objectOf(PropTypes.number),
  message: PropTypes.instanceOf(Message)
}
```

```jsx
MyCo.propTypes = {
  user: PropTypes.shape({
    name: PropTypes.string,
    age:  PropTypes.number
  })
}
```

Use `.array[Of]`, `.object[Of]`, `.instanceOf`, `.shape`.

{{ ::card-item:: }}

### Custom validation

```jsx
MyCo.propTypes = {
  customProp: (props, key, componentName) => {
    if (!/matchme/.test(props[key])) {
      return new Error('Validation failed!')
    }
  }
}
```

{{ ::group:: }}
## Also see

* [React website](https://reactjs.org) _(reactjs.org)_
* [React cheatsheet](https://reactcheatsheet.com/) _(reactcheatsheet.com)_
* [Awesome React](https://github.com/enaqx/awesome-react) _(github.com)_
* [React v0.14 cheatsheet](react@0.14) _Legacy version_

