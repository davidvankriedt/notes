---
title: CSS Layouts
draft: false
tags:
  - computer-science
  - css
  - webdev
---
![[div-layout-diagram.jpg]]

### Block Elements

[[Block elements]] start with a new line & stretch to the full width of the container.

A very common example of a block element is a div. The diagram above shows the different layers that make up a div, border being the outer line of the div - note that the margin exists __outside__ of the div, so it doesn't affect the content inside the div but rather elements in the parent element.

__Example__:

text before
__block element__
	__inner block__
text after


### Inline Elements

[[Inline elements]] have the size of the content - they don't stretch to the full width of the container or start with a new line.

A common example of an inline element is a span.

__Properties__:
- `display:none` - hides element.
- `visibility:hidden` - keeps element there but makes it invisible.
### Float
Removes element from normal flow and puts it to the left/right of the container & allows other inline elements to wrap around it.

### Position

##### Static
The [[static position]] positions an element based on normal flow. Offset properties have no effect on it. This is the default value of the __position__ property.

##### Relative
The [[relative position]] positions an element based on the top-left corner of its parent element. Offset properties __will__ apply to it based on its default position.

##### Absolute
The [[absolute position]] will offset properties based on the closest parent element with a non-static position.

### Overflow
Sets how element will show its content when it overflows the edges.

`visible` - content visible outside edges (default).
`hidden` - hide, no scroll.
`auto` - hide, yes scroll.
`scroll` - hide, always show scroll bar, regardless of whether content is overflowing.

### Flexbox

[[Flexbox]] is a very powerful tool for laying out elements that was introduced after developers found a need for displaying items in a more efficient fashion than using __position__. It defines a layout where children could be positioned in any direction and change their size based on available space.

If we want to use flexbox, in the parent container we do `display:flex`.

`flex-direction`- defines direction of children.
`justify-content`- defines alignment of main axis.
`align-items`- aligns children on cross axis.
`flex-wrap`- manages overflow of children.
`align-content`- similar to `justify-content`, but in cross axis.
`order`- defines order of a child relative to other children.
`flex`- defines ratio of child size relative to other children.

---
### Useful links
- [css spec](https://www.w3.org/TR/CSS2/) 
- [check browser support](https://caniuse.com)
- [useful css tricks](https://css-tricks.com)
- [css triggers you can make](https://csstriggers.com)

