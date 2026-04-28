---
title: WebJS
draft: false
tags:
  - webdev
  - computer-science
  - js
---
## How to include JS files:
- __inline__:
	```
	<html>
		<script>
			... <-- here
		</script>
	</html>
	```

- __external__:
```
	<html>
		<head>
		</head>
		
		<body>
			<script type="text/javascript" src="script.js"></script>
		</body>	
	</html>
```
--> you can include it in the head or top of the body when you need js to run before [[DOM]] elements are rendered. However, it's usually put at the end of the body tag.


## DOM

The [[DOM]] (Document Object Model) is an interface that allows [[JavaScript]] to interact with [[HTML]] through the browser.

__DOM Data Types__:
- Document - Root of the entire DOM.
- Element - node in DOM tree.
- NodeList - an array of elements.

Different [[HTML]] tags correspond to different [[DOM]] element types.

The [element](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement) interface allows us to read and write to the [[DOM]].

__Reading the DOM__:
- document:
```
	getElementById(id);
	getElementsByTagName(name);
	getElementsByClassName(className);
	querySelector(query); // a more general reader
```

__Writing to the DOM__:
```
	let element = document.createElement("div");
	let textNode = document.createTextNode("hello");
	
	element.appendChild(textNode);
	element.removeChild(textNode);
	
	let button = document.createElement("button");
	
	button.setAttribute("disabled", "");
	
	element.style.left = "50px"; // only present if style is set inline or script
```

__For CSS written style__:
```
let computedStyle = window.getComputedStyle(element, null);
let bgColour = computedStyle.getPropertyValue("background-color")
```



## Events

[[Events]] are interactions client-side on page.

__Adding event handlers__:
1. HTML: `<input onclick="alert('Clicked!')>`
2. DOM Property: 
```
	let element = document.getElementById('btn');
	element.onClick = () => alert('Button has been clicked!');	
```
3. addEventListener:
```
	let handler = () => alert('Hello!');
	
	element.addEventListener('click', handler);
	element.removeEventListener();
	
	// the event parameter passes an event object that gives
	// detail about specific event, e.g. 'hover'
	
	element.addEventListener('hover', () => {
		console.log(event.type); // 'hover'
	});
```

Events propagate from target element to the root of the DOM. To avoid this, add `event.stopPropagation()` to event handler.

To stop default behaviour, e.g. a button in a form refreshing the page, use `event.preventDefault()`.

## Persistence

[[Persistence]] refers to being able to retain data between states.

Server-side: A [[database]].
Client-side: The user's machine.

### Local Storage
`window.localStorage` - an [[API]] that allows you to read & write to storage object in document
--> stored data is persisted between sessions

__When to use__:
- When there's no server
- For data that isn't crucial if lost
- For data specific to only one user

__When not to use__:
- When security of data is important.
- For large amounts of data.
- For complex data.
- When data is needed on multiple devices.

__API__:
```
localStorage.setItem(key, value); // add data item

const value = localStorage.getItem(key); // retrieve item

localStorage.removeItem(key); // remove item

localStorage.clear(); // remove all items
```
