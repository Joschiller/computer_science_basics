# React

- [Usage](#usage)
- [References](#references)
- [Overview](#overview)
  - [Components](#components)
    - [Rules](#rules)
    - [Immutable state](#immutable-state)
    - [HTML Ordered List (`<ol />`)](#html-ordered-list-ol-)
- [JSX](#jsx)
  - [Attributes](#attributes)
  - [Elements](#elements)
  - [Components](#components-1)
    - [State](#state)
    - [Hooks](#hooks)
    - [Events](#events)
    - [Refs](#refs)
  - [Conditional Rendering](#conditional-rendering)
  - [Lists of Elements](#lists-of-elements)
  - [Controlled Components](#controlled-components)
- [Design](#design)

## Usage

- web devenlopment
- UI framework
- based on [JavaScript](./JavaScript.md) or [TypeScript](./TypeScript.md), [HTML](./HTML.md) and [CSS](./CSS.md)

## References

> https://reactjs.org/docs/getting-started.html
>
> https://reactjs.org/tutorial/tutorial.html
>
> https://react.dev/learn
>
> https://react.dev/reference/react

## Overview

standard script

```tsx
ReactDOM.render(
  html_code,
  document.getElementById('root');
);
```

### Components

```tsx
// class components
class name extends React.Component {
  // methods, attributes and constructors can be added
  constructor(props) {
    super(props); //mandatory!
    ... // e.g. set state here
  }
  // render is called repeatedly
  render() {
    // this.props => attributes, that were set in jsx
    // this.state => inner state, set in the constructor, read/initialize via this.state and set via setState(...)
    // typescript code
    return ( /* jsx */);
  }
}

// function components (if only rendering once an less inner logic needed)
const name = () => {
  // typescript code
  return ( /* jsx */)
}
function name(props) {
  // typescript code
  return ( /* jsx */)
}

// export
export default name
```

- HTML-based description is short form to code description (JSX)
- each React element is a JavaScript object, each component is available in JSX as `<name />`
- Events (e.g. onClick) can be set in JSX: `event={(...) => { code }}`

#### Rules

- current state should be handled in uppermost component, lower components only have a render method that gets the needed props via jsx
- convention for events: on[Event] throws, handle[Event] catches
- when the state changes, handle it as immutable

#### Immutable state

1. read the state, copy needed data (Array via .slice())
2. update the data
3. call setState with the new data

OR directly call setState with new data (based on the old in an immutable way)

- immutable Arrays: .slice(), .concat(...) instead of .push(...), .map(...)
- Advantages:
  - changes can be tracked later on, an old status can be restored from a history
  - changes can be detected directly, because the referenced object changed and not its contents
  - consistent re-rendering (see shouldComponentUpdate())

#### HTML Ordered List (`<ol />`)

- each element needs a unique property “key” to be set (to determine when the element was added/moved/deleted for rendering)
- this has to be set when the element is generated (e.g. via a map method on an array)
- map can take different arguments:
  - (arg0) => ...
  - arg0 = handled element
  - (arg0, arg1) => ...
  - arg1 = index of the handled element

## JSX

- mainly HTML (outermost tag can always be “div”)
- each JavaScript/TypeScript part needs to be wrapped in { ... }
- when extending the JSX over several lines => surround with ( ... ) to prevent automatic semicolons to be placed in between
- JSX can be passed around like JavaScript/TypeScript objects => can be used in variables and control structures (conditional rendering)

### Attributes

- are set in the HTML-tag
- strings with "..." and code with { ... }
- JSX is more closely related to JavaScript then to HTML (camelCase naming)
- the props of the element contain all the attributes and the "children: ..."

### Elements

- single parts of a component
- react only updates, what is necessary

| HTML                    | React                                                                                |
| :---------------------- | :----------------------------------------------------------------------------------- |
| `<div id="root"><div/>` | `code` <br/> `ReactDOM.render(element_in_the_code, document.getElementById('root'))` |

### Components

- JavaScript functions that take inputs (props) and return a react element describing the GUI
- Attributes and Children get passed to the component in the props
- lifecycle Methods (e.g. can use any additional needed properties for the class):
  - mounting (when rendered to page): creating resources that are needed by a new component
  - unmounting (when removed from page): destroying resources when component is destroyed
  - componentDidMount (is rendered to page)
  - componentWillUnmount (before removal from page)
  - componentDidUpdate (after updated in DOM)
- component composition
  - build a component using several childs
  - create specializations using more general childs and setting specific props
  - add a frame around children using { props.children } => showing JSX children

```tsx
// function that is called once
function Name(props) {
  return (JSX);
}

// render() is called repeatedly
class Name extends React.Component {
  [constructor(props) {
    super(props);
    //e.g. set state
  }]
  [componentDidMount() { ... }]
  [componentWillUnmount() { ... }]
  render() {
    return (JSX);
  }
}
```

Rules:

- Necessary (!) convention: Component names start with uppercase! to be seen as such in the JSX (otherwise it would be like an HTML-tag)
- larger components should be split in smaller reusable components
- Strict rule: All React components must act like pure functions with respect to their props. => PROPS ARE READ ONLY! => used for static properties

#### State

> stores additional properties; used for interactivity
>
> Browser: one state is only available in one tab

```tsx
// Constructor
this.state = ...; // only use this assignment in the constructor

// Elsewhere
this.setState(state); // updates the state AND rerenders the component; merges the current state with the new state (only overrides provided properties)
this.setState((state, props) => { ... }); // updates the state when the props are up to date
```

Rules:

- state is only passed down to included components, state only affects components below
  - upper components should not care if a child has a state or not
  - child components should not care where any props come from
- state should be stored at the closest common ancestor of several components => the ancestor controls the state below and holds the common state
  - the state is part of the props of the child components
  - property changes in the childs are communicated using an event (even if the event has no handler assigned, this is no problem)
  - the parent is the single "source of truth”"for the data

#### Hooks

- State for functional components (not available in class components)
- uses the fact, that functions can contain functions => crate inner functions

```tsx
import React, { useState, useEffect } from 'react';

const [var, setVar] = useState(value); // access to state
useEffect(() => { ... }); // access to lifecycle methods; combines all lifecycle methods into one
```

#### Events

```tsx
event={function}
```

to prevent default behaviour:

- add parameter “e” to handling function and use e.preventDefault()
- to use correct “this” in an event callback

  - bind this to the callback method in the constructor

    or

  - define method as arrow function and assign it to a class field

    or

  - define callback as arrow function (this may use more memory)

- more details see: https://reactjs.org/docs/handling-events.html

#### Refs

> Refs are needed to access state in event handlers

```tsx
const [arg, _setArg] = useState(...)
const argRef = useRef(arg)
const setArg = (...) => {
  _setArg(...)
  argRef.current = ...
}

const somethingHandler = () => {
  // can access argRef.current here to have access to state of arg
}
```

> Refs can also be attached to reference components. For their initialization use:

```tsx
const componentRef = useRef<HTMLSomeTypeOfComponentElement>(null);
// can be accessed using componentRef.current!...
```

### Conditional Rendering

- embed conditions in JSX using { ... } => render based on specific props
- { condition && component } => true = render; false = ignore => but the condition must return a read boolean (not int or string …)
- can also use ternary operator
- to hide a component itself => return null instead of JSX

### Lists of Elements

```tsx
<ul>
  {someArray.map((element, i) => (
    <SomeComponent key={i} {...furtherProps} />
  ))}
</ul>
```

- must provide a key for each list element (create unique string from data or use item index if the order does not change (see https://reactjs.org/docs/lists-and-keys.html#keys))

### Controlled Components

- Form/Textarea/Select (Dropdown) all have the attribute "value"
  - use controlled components (https://reactjs.org/docs/forms.html) to catch input changes (like bindings)
  - provide value via state and update state using event onChange of the form
- e.g. https://codepen.io/gaearon/pen/WZpxpz?editors=0010

## Design

- take mock => find single components and subcomponents using the "single responsibility principle"
- the static data model is represented in the props
- the state stores the dynamic/interactive data => should be minimal => rest will be computed

1. Mock
2. static model => props
3. identify state
4. identify parent component that holds the state
5. add inverse data flow (events)

FURTHER: https://reactjs.org/docs/accessibility.html
