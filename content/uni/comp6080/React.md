---
title: React
draft: false
tags:
  - webdev
  - computer-science
  - js
  - react
---
Building dynamic, single-page websites with plain JS is complicated, verbose, and takes too long to create simple features.

[[React]] is a library for building [[UI]]s. It allows us to build isolated [[UI]] components in a simple, declarative way. When state changes in app, affected components will __react__ accordingly by re-rendering to reflect the new state.

__Imperative__: Specify the process, not the outcome.
__Declarative__: Specify the outcome, not the process.

## JSX

An extension of [[JavaScript]]. Allows you to treat [[HTML]] markup like you would any [[Javascript]] object or variable.

## CSS

You can `import './App.css';` and that does it.

However, you don't want to use global CSS, because it can leak into unwanted pages if the same name is repeated.

__CSS Modules__:
Instead of `style.css`, use `App.module.css`, then in `App.jsx`, use `import styles from './App.module.css'`, then instead of `className = 'button'`, you do `className = {styles.button}`

__Styled Components__:
```
import styled from 'styled-components';

export const Button = styled.button(() => ({
	backgroundColor: 'black';
	color: 'blue';
}));
```
This works if you want to make everything from scratch in a structured way.


## React Hooks
__useState__:
`const [var, setVar] = useState(0); // where 0 = initial value of var`

__useEffect__:
Takes in a function & array, it's called if one of the dependencies in its dependency array is mutated, or if no array is provided, when every render occurs. Always called asynchronously, after a component has rendered --> If you need to use `useEffect` before component is rendered, use `useLayoutEffect` to trigger after [[DOM]] mutates, but before render.

Common use cases:
- Fetching data.
- Managing subscriptions.
- Setting up timers.
- Performing Native DOM manipulations when needed.



