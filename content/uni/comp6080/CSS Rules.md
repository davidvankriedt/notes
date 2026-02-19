---
aliases:
  - Cascading Style Sheets, CSS
---
`---`

`aliases: [Cascading Style Sheets, CSS]`

`---`

[[CSS Rules|Cascading Style Sheets, CSS]] is a language used to enhance [[HTML]] tags.

[[CSS Rules|Cascading Style Sheets, CSS]]'s styling uses dashes (-), not camelCase or snake_case.

##### Importing CSS:
- Import external file with styles: `<link rel="stylesheet" href="style.css" />`
- Add inline styles to specific element: `<div style="color:red">text</div>`
- Add styles directly to the document:
- ```
	<html>
		<style>
			.class {
			color: red;
			}
		</style>
	</html>
  ```


##### CSS Syntax:
__Selector__: Define elements to apply rule to.
__Property__: One of the style properties.
__Value__: One of the possible values for the given property.

```
[selector] {
	[property]: [value];
}
```

##### Selectors:

Universal Selector - * - Applies to all elements.
.class Selector - Selects all elements within given class.
/# id selector - Selects unique element with given id.
Attribute selector - `selector[attribute=value]` - selects elements with given attribute pair, `input[type=radio]`

##### Combinators:
These establish a relationship between selectors.

- `.A .B` - All class B elements inside class A elements.
- `.A > .B` - All class B elements that are direct children of A.
- `.C + .B` - All class B elements that follow immediately after C.
- `.C ~ .B` - All sibling .B that follow after C.

##### Pseudo-classes:
`[selector]:[pseudo-class]` - Selects elements with a special state.

`button:hover`- button on which user is hovering.
`input:focus`- input which received focus.
`input:disabled` - disabled input.
`a:visited` - visited links.

##### Pseudo-elements:
`[selector]::[pseudo-element]`- Used to create cosmetic content for the element or allows you to style a specific part of the element.

`text::first-letter`- Targets first letter of every text tag.

##### Cascade:
When you have 2 selectors named the __same__ and have the __same__ property, the one defined earliest in the source code is prioritised.

##### Inheritance:
Properties inherit values from parent tags, so you don't have to write rules for __every__ element.

##### Specificity:
If an element has multiple rules with the same property, beside cascade, it'll prioritise specificity of each selector.

`!important`- Overrides all specificity hierarchy. e.g. `color: blue !important;`

__Specificity Hierarchy__:
1. inline !important
2. id !important
3. class !important
4. tag !important
5. inline
6. id
7. class
8. tag
