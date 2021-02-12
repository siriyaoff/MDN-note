# CSS Basics 21.02.09~
## What is CSS?
### CSS(Cascading Style Sheets)
- style sheet language(neither programming language nor markup language)
- to style HTML elements selectively
- need to be linked in `<head>` of an HTML document like`<link href="style.css" rel="stylesheet">`

### Anatomy of a CSS ruleset
![Anatomy of a CSS ruleset](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics/css-declaration-small.png)
- Selector
	- HTML element name at the start of the ruleset
- Declaration
	- single rule like `color: red;`
	- specifies element's properties to style
- Properties
	- HTML element's property to affect
- Property value
	- value for a given property
- Syntax of a ruleset
	- Apart from the selector, each ruleset must be wrapped in `{}`
	- Use `:` to separate the property and its value
	- Use `;` to separate each declaration
	- To select multiple elements as selector, use `,` as separator
		```css
		p, li, h1 {
			color: red;
		}
		```

### Different types of selectors
| Selector name			| What does it select | Example |
| :--- | :--- | :--- |
| Element selector		| All HTML elements of the specified type. | `p`<br>selects `<p>` |
| ID selector			| The element with the specified ID. Each id value should be unique. | `#my-id`<br>selects `<p id="my-id">` |
| Class selector		| The element(s) with the specified class. Classes can be duplicated. | `.my-class`<br>selects `<p class="my-class">` and `<a class="my-class">` |
| Attribute selector	| The element(s) with specified attribute. | `img[src]`<br>selects `<img src="myimage.png">` but not `<img>` |
| Pseudo-class selector	| The specified element(s) but only when in the specified state. | `a:hover`<br>selects `<a>` but only when the mouse is hovering over the link |

이 외에도 많은 selector가 있음([MDN Selectors guide](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors){:target="_blank"} 참고

## Fonts and text
```css
html {
	font-size: 10px;
	font-family: "Open Sans", sans-serif;
}
h1 {
	font-size: 60px;
	text-align: center;
}
p, li {
	font-size: 16px;
	line-height: 2;
	letter-spacing: 1px;
}
```
- If there is a space in the font name, the font should be wrapped by double quotes

## CSS: all about boxes
CSS layout is mostly based on the *box model*. Each box taking up space on your page has properties like:  
![figure for the properties](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics/box-model.png)
- `padding` : the space around the content
- `border` : the solid line outside the padding
- `margin` : the space around the outside of the border
- `width` (of an element)
- `background-color` : the color behind an element's content and padding
- `color` : the color of an element's content(usually text)
- `text-shadow` : for the text inside an element
- `display` : sets the display mode of an element

**Example**  
CSS:
```css
html {
  font-size: 10px;
  font-family: 'Open Sans', sans-serif;
}


h1 {
  font-size: 60px;
  text-align: center;
}

p, li {
  font-size: 16px;
  line-height: 2;
  letter-spacing: 1px;
}


html {
  background-color: #00539F;
}

body {
  width: 600px;
  margin: 0 auto;
  background-color: #FF9500;
  padding: 0 20px 20px 20px;
  border: 5px solid black;
}

h1 {
  margin: 0;
  padding: 20px 0;
  color: #00539F;
  text-shadow: 3px 3px 1px black;
}

img {
  display: block;
  margin: 0 auto;
}
```

HTML:
```html
<!DOCTYPE html>
<html>
  <head>
	<meta charset="utf-8">
	<title>My test page</title>
	<link href="http://fonts.googleapis.com/css?family=Open+Sans" rel="stylesheet" type="text/css">
	<link href="style.css" rel="stylesheet" type="text/css">
  </head>
  <body>
	<h1>Mozilla is cool</h1>
	<img src="https://raw.githubusercontent.com/mdn/beginner-html-site-styled/gh-pages/images/firefox-icon.png" alt="The Firefox logo: a flaming fox surrounding the Earth.">

	<p>At Mozilla, we’re a global community of</p>

	<ul> <!-- changed to list in the tutorial -->
	  <li>technologists</li>
	  <li>thinkers</li>
	  <li>builders</li>
	</ul>

	<p>working together to keep the Internet alive and accessible, so people worldwide can be informed contributors and creators of the Web. We believe this act of human collaboration across an open platform is essential to individual growth and our collective future.</p>

	<p>Read the <a href="https://www.mozilla.org/en-US/about/manifesto/">Mozilla Manifesto</a> to learn even more about the values and principles that guide the pursuit of our mission.</p>
  </body>
</html>
```

shows an HTML document like below:  
![example page](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics/website-screenshot-final.png)

**Explanation**
- `margin` and `padding`
	- can have 1/2/3/4 values with several units(`em`, `%`, `px`, ...) or `auto`
		- 1 value : 4 sides
		- 2 values : vertical | horizontal
		- 3 values : top | horizontal | bottom
		- 4 values : top | right | left | bottom
	- `margin` creates extra space around an element, while `padding` creates it within an element
	- browsers apply default styling to the `<h1>` element -> there are margins in headings
	- top, bottom margins have no effect on non-replaced inline elements such as `<span>`, `<code>` **not** headings(=block elements)

※ replaced elements : elements that css cannot change the content of the elements except its position, such as `<iframe>`, `<img>`, ...

- `text-shadow` has 4 values(horizontal offset | vertical offset | blur radius | base color)

- `display` property
	- `<img>` is an inline element. To apply `margin`, it has to be treated as block element. -> Use `display: block;`!
	- 웹페이지에서 `<img>`가 `<body>` 안에 있는 구조, 즉 이미지의 width가 600px 미만이라 가정한 상태임. 만약 600px 이상일 경우 body를 넘어서 표시됨. -> 이미지 너비를 미리 줄이거나 CSS에서 이미지 사이즈를 정의해줘야함!

------
css는 unknown canvas에 대해 웹페이지가 잘 읽힐 수 있도록 만들어짐
모든 css 코드들은 하나의 suggestion일 뿐이고 browser가 author, user, system을 종합해서 웹페이지를 보여줌
css 코드들은 브라우저가 이해가능한 것은 수용하고 그렇지 않은 것들은 무시하는 형태로 컴파일됨
따라서 backward compatible함


# CSS first steps
## What is CSS?
Document : a text file structured using a markup language(html, xml, ...)  
Presenting a document = converting a document  
Browsers(kinds of user agent) are designed to present documents visually

### CSS syntax
CSS is a rule-based language.

An example of the rule:
```css
h1 {
	color: red;
	font-size: 5em;
}
```
- The rule opens with a **selector**. Then we have a set of curly braces `{ }`. Inside, there will be one or more **declarations**(=`[PROPERTY]: [VALUE];`)

### CSS Modules
Property를 잘 찾을 수 있게 Module로 분류해놓음(MDN reference에서 찾을 수 있음, e.g. [Backgrounds and Borders](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Backgrounds_and_Borders){:target="_blank"})

#### CSS specifications
모든 web standards technologies는 standards organizations가 만드는 specifications(or "specs")라는 문서에 의해 정의된다. CSS의 경우 W3C의 CSS Working Group에 의해서 specification이 만들어진다. CSS specs는 user agents에서 기능들이 작동하도록 구현하는데 도움을 주는 목적으로 작성된 것이다. 즉CSS에 대한 이해를 위해 읽는게 아니고, CSS, browser support, specs의 관계에 대해서만 이해하고 있으면 됨
- Once CSS has been specified then it is only useful for us in developing web pages if one or more browsers have implemeneted it.

=> spec에 정의되어있으면 css code에 사용할 수 있지만 browser에서 구현해놓아야 적용됨

## Getting started with CSS
- Add CSS to an HTML document by adding `<link>` in the head of the document.  
`<link rel="stylesheet" href="styles.css">`
- `selector` matches an HTML element name directly  
Choose multipe elements with `,`

### Adding a class
In HTML, we can add a class to elements:  
`<li class="special">Item two</li>`

In CSS, we can target the class by creating a selector starts with a full stop(`.`)
- `.special {` : any element has a class of `special`
- `li.special {` : any `<li>` has a class of `special`
- `li.special, span.special {` : any `<li>` or `<span>` have a class of `special`  
※ `.special, h1`과 같이 생성자를 섞어서 사용할 수도 있음

※ 한 element에 대해 모두 같은 스타일을 적용할 일은 잘 없기 때문에 항상 선언할 때 `class`를 추가하는 것이 좋음!

### Styling things based on their location in a document
- There are a number of combinators for kinds of this purpose, such as `descendant combinator`, `adjacent sibling combinator`, ...

#### Descendant combinator `' '`
`A B {` : Target `B` element nested inside `A`(B is a descendant of A)  
e.g. `li em { ...` selects any `<em>` nested inside `<li>`

#### Adjacent sibling combinator `+`
`A + B {` : Target `B` right after `A`  
`A`, `B` is at the same hierarchy level in the HTML  
e.g. `h1 + p { ...` selects any `<p>` directly after `<h1>`

### Styling things based on state
Some elements can have several states like visited, unvisited, hover, clicked(activated), ...  
We can style elements in specific states by using `:`  
`a:visited { ...` selects any `<a>` visited

**Combinations possible!**  
- `body h1 + p .special { ...` : any element with a class of `special` inside a `<p>` which comes just after an `<h1>` which is inside a `<body>`  
- `p a.ac:hover { ...` : `<a>`  with class `ac`, state `hover`, inside a `<p>`  
※ `ul+p` : `<ul>`이 끝난 직후의 `<p>`(`</ul>` 다음의 `<p>`)

***************************
궁금한거
`a`에서 `font-weight: bold;`, `a:visited`에서 `font-weight: normal;`이라 선언하면 visited상태인 링크는 bold가 그대로 적용되어있음. visited가 우선일 것 같은데 왜이런지 모르겠음(color는 둘다 설정되어있으면 visited걸로 바뀌는데 font-weight, font-style은 a에서 900, 이탈릭이고 visited에 normal, normal일때 a꺼가 그대로 유지됨) : pseudo-class 우선순위 찾아봐야할듯!
```css
a {
	color: red;
	font-weight: 900;
	font-style: italic;
}

a:visited {
	color: green;
	font-weight: normal;
	font-style: normal;
}
```
`:`는 combinator가 아닌가?(정의?) : pseudo-class임!

## How CSS is structured
### Applying CSS to HTML
Three methods available to apply CSS to a document: with an external stylesheet, with an internal stylesheet, and with inline styles.
#### 1. External stylesheet
`<link rel="stylesheet" href="styles.css">` in `<head>` of an HTML document.
- most common and useful method
- possible to link a single CSS file to multiple web pages

#### 2. Internal stylesheet
`<style> CSS CODE </style>` in `<head>` of an HTML document
- useful in some circumstances such as blocked from modify external CSS files.  
but for sites with many pages, internal stylesheet is less efficient.(one simple styling change requires editing multiple pages.)

#### 3. Inline styles
`<p style="color:red;bacground-color: yellow;"> ... </p>` for each element needs styling
- **Avoid it when possible!**
	- the least efficient for maintenance
	- mixes presentational code(CSS) with HTML
- few circumstances such as email(to achieve compatibility with email clients), only allowed to edit the HTML body.

### Selectors
valid selectors:  
```css
h1
a:link
.classes
#ids /*id should be unique!*/
*
.box p
.box p:first-child
h1, h2, .intro
```
- `A:first-child` : 같은 부모를 가진 A elements 중 첫 번째 자식 선택(div안에 첫 번째 p, body안에 첫 번째 p 등으로 여러 개가 선택될 수 있음)  
※ Learn more about selectors in the next module: CSS selectors

#### Specificity
If two selectors select the same element, CSS apply the rules by **cascade** and **specificity**.

**cascade** rule  
Later styles replace conflicting styles that appear earlier in the stylesheet.  
e.g.  
```css
p {
	color: red;
}

p {
	color: blue;
}
```
- the paragraph text will be blue by the cascade rule.

**specificity** rule  
If two selectors select the same element, CSS apply the rule that has more specificity. It is stronger than the cascade rule.

### Properties and values
- **case-sensitive**!!
- based on US spelling(no `colour`)
- If a property or a value is not valid, it is completely ignored by the browser's CSS engine.

#### Functions
There are some functions we can use within CSS, such as `calc()`, `rotate()`  
e.g. `width: calc(90%-30px);`, `transform: rotate(0.8turn);`

### @rules
@rules("at-rules") provide instruction for what CSS should perform or how it should behave.  
**Example**  
`@import`
- to import a stylesheet into another CSS stylesheet
- `@import 'styles2.css';`

`@media`
- to create media queries(conditional logic for applying CSS styling(responsive image에서 사용하는 것)
```css
@media (min-width: 30em) {
  body {
    background-color: blue;
  }
}
```

### Shorthands
Properties set several values in a single line, such as `font`, `background`, `padding`, `border`, `margin`
e.g.  
`background: red url(bg-graphic.png) 10px 10px repeat-x fixed;`  
is equivalent to  
```
background-color: red;
background-image: url(bg-graphic.png);
background-position: 10px 10px;
background-repeat: repeat-x;
background-attachment: fixed;
```

> **Warning**: An omission in CSS shorthand can **override previously set values**.
> A value not specified in CSS shorthand reverts to its initial value.

### Comments
`/* Handle basic element styling */`  
`/* Handle specific elements nested in the DOM  */`  
와 같이 주석 달아놓는게 좋음.

**comment out the code**  
```css
/*.special {
  color: red;
}*/
```

### White space
There is no semantic role for white spaces, but it improves readability.

Property names and property values never have white space!

## How CSS works
### How does CSS actually work?
Simplified steps when a browser loads a webpage: 
1. The browser loads the HTML.
2. It converts the HTML into a DOM(Document Object Model). The DOM represents the document in the computer's memory.
3. The browser fetches most of the resources(images, CSS, ...) linked to by the HTML document. + handling JavaScript
4. The browser parses the fetched CSS, and sorts the rules by selector types into different "buckets"(element, class, ID, ...). Based on the selectors, it works out which rules should be applied to which nodes in the DOM, and attaches style to them as required (this intermediate step is called a render tree).
5. The render tree is laid out with the rules applied appropriately.
6. The visual display of the page is shown on the screen (this stage is called painting).

A Diagram of the process:  
![simple view of the process](https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps/How_CSS_works/rendering.svg)

### About the DOM
A DOM is a **tree-like structure**. Each element, attribute, and piece of text in the markup language becomes a DOM node in the tree structure. The nodes are defined by their relationship to other DOM nodes. It is **where CSS and the document's content meet up**.

### A real DOM representation
