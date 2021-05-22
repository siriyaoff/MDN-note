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

이 외에도 많은 selector가 있음([MDN Selectors guide](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors){:target="_blank"} 참고)

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
- The rule opens with a **selector**. Then we have a set of curly brackets `{ }`. Inside, there will be one or more **declarations**(=`[PROPERTY]: [VALUE];`)

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
**Example**:  
HTML code:  
```html
<p>
  Let's use:
  <span>Cascading</span>
  <span>Style</span>
  <span>Sheets</span>
</p>
```

converted DOM:  
```
P
├─ "Let's use:"
├─ SPAN
|  └─ "Cascading"
├─ SPAN
|  └─ "Style"
└─ SPAN
   └─ "Sheets"
```

rendered outputs:  
```
Let's use: Cascading Style Sheets
```

### Applying CSS to the DOM
- After a DOM created, the browser will parse the CSS, sort it, apply the rules, and paint the final visual representation to screen.

### What happens if a browser encounters CSS it doesn't understand?
- Just moves on to the next bit of CSS
- cascade rule을 이용해서 새로운 기능을 지원하지 않는 browser에 대해 alternatives를 제공할 수 있음

e.g.  
```css
.box {
  width: 500px;
  width: calc(100%-50px);
}
```


# CSS building blocks
## Cascade and inheritance
### Conflicting rules
#### The cascade
Stylesheets **cascade**. The order of CSS rules matter. When two rules have equal specificity, the last one will be used.  
e.g.  
```css
h1 { 
    color: red; 
}
h1 { 
    color: blue; 
}
```  
-> `<h1>` will be colored blue

#### Specificity
If multiple rules have **different selectors but still select the same element**, the browser decides which rule to apply by the **specificity**. It is basically a measure of how specific a selector's selection will be:
- An element selector is less specific
- A class selector is more specific

e.g.  
```css
.main-heading { 
    color: red; 
}
        
h1 { 
    color: blue; 
}
```  
-> `<h1>` with class `.main-heading` will be colored red.

#### Inheritance
Some CSS property values in the parent elements are inherited by their child elements, and some aren't. For example, `color` and `font-family` inherit, but `width` does not inherit.

### Understanding how the concepts work together
These three concepts(cascade, specificity, and inheritance) together control which CSS applies to what element

### Understanding inheritance
#### Example
CSS:  
```css
.main {
    color: rebeccapurple;
    border: 2px solid #ccc;
    padding: 1em;
}

.special {
    color: black;
    font-weight: bold;
}
```

HTML:  
```html
<ul class="main">
    <li>Item One</li>
    <li>Item Two
        <ul>
            <li>2.1</li>
            <li>2.2</li>
        </ul>
    </li>
    <li>Item Three
        <ul class="special">
            <li>3.1
                <ul>
                    <li>3.1.1</li>
                    <li>3.1.2</li>
                </ul>
            </li>
            <li>3.2</li>
        </ul>
    </li>
</ul>
```

|Result:|
|:---|
|![Inheritance ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-inheritance-ex1.PNG?raw=true)|

- We have given the outer `<ul>`(with class `main`) a border, padding, and font color. The color has applied to the direct children, but also the indirect children. Same for another class `special`. But things like widths, margins, padding, and borders do not inherit.(Probably not an effect we would ever want!)
- Which properties are inherited by default and which aren't is largely **down to common sense.

#### Controlling inheritance
There are four special universal property values for controlling inheritance. Every CSS property accepts these values.
- `inherit`
	- sets the property value to be the same as that of its parent element
	- "turns on inheritance"
- `initial`
	- sets the property value to the initial value of that property
- `unset`
	- resets the property to its natural value(If the property is naturally inherited it acs like `inherit`, otherwise it acts like `initial`)
	- property가 `color`같은거면 `inherit`, `width`같은거면 `initial`과 같이 취급, shorthand로 다 같이 정의할 때 omitting으로 문제 일어나지 않도록 쓰는 용도인듯
- `revert` : newer value, limited browser support

#### Example
CSS:  
```css
body {
    color: green;
}
          
.my-class-1 a {
    color: inherit;
}
          
.my-class-2 a {
    color: initial;
}
          
.my-class-3 a {
    color: unset;
}
```

HTML:  
```html
<ul>
    <li>Default <a href="#">link</a> color</li>
    <li class="my-class-1">Inherit the <a href="#">link</a> color</li>
    <li class="my-class-2">Reset the <a href="#">link</a> color</li>
    <li class="my-class-3">Unset the <a href="#">link</a> color</li>
</ul>
```

|Result:|
|:---|
|![universal property ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-universal-property-ex1.PNG?raw=true)|

- `a { color: red;}`를 추가하면 맨 위 링크만 빨간색으로 변함(다른 것들은 `' '` combinator, class selector로 specificity가 더 높은 rule이 적용되어있기 때문)

#### Resetting all property values
The CSS shorthand property `all` represents all properties. So we can use it usefully when we debug. If we apply `all: unset;` declaration, all rules applied will be initialized except the inherited properties.

#### Example
CSS:  
```css
blockquote {
    background-color: red;
    border: 2px solid green;
}
        
.fix-this {
    all: unset;
}
```

HTML:  
```html
<blockquote>
	<p>This blockquote is styled</p>
</blockquote>

<blockquote class="fix-this">
	<p>This blockquote is not styled</p>
</blockquote>
```

|Result:|
|:---|
|![all property ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-all-property-ex1.PNG?raw=true)|

- `all`도 다른 property와 같이 conflicting rule에 의해 처리됨
- `all`은 모든 property를 포함하기 때문에 padding과 같은 ruleset으로 정의하지 않았지만 기본적으로 정의해주는 속성(padding, margin 등)도 같이 `unset`됨

### Understanding the cascade
There are three factors to consider. Later ones overrule earlier ones:
1. Source order
2. Specificity
3. Importance

#### Source order
- Exactly the same weight -> the last one wins.

#### Specificity
- More specific rule is chosen by the browser.(Specificity > Source order)
- A class selector has more weight than an elemen selector -> class selector rules will override the element selector rules.
	- overwrite only the same properties, not the entire rules!
- To avoid repetition, define generic styles for the basic elements then create classes for specific cases.

**How to calculate specificity**  
Essentially a value in points is awarded to different types of selectors, and adding these up gives you the weight of that particular selector, which can then be assessed against other potential matches.  
The amount of specificity is measured using four different values(thousands, hundreds, tens, and ones): 
1. **Thousands** : 1 if declaration is inside a `style` attribute(= **inline styles**) -> No selectors, so always specificity=1000
2. **Hundreds** : 1 for each **ID selector** contained inside the overall selector
3. **Tens** : 1 for each **class selector**, **attribute selector**, or **pseudo-class** contained inside the overall selector
4. **Ones** : 1 for each **element selector** or **pseudo-element** contained inside the overall selector

**Note**: The universal selector(`*`), combinators(`+`, `>`, `~`, `' '`), and negation pseudo-class(`:not`) have no effect on specificity

#### Example
```css
/* specificity: 0101 */
#outer a {
    background-color: red;
}
        
/* specificity: 0201 */
#outer #inner a {
    background-color: blue;
}

/* specificity: 0104 */
#outer div ul li a {
    color: yellow;
}

/* specificity: 0113 */
#outer div ul .nav a {
    color: white;
}

/* specificity: 0024 */
div div li:nth-child(2) a:hover {
    border: 10px solid black;
}

/* specificity: 0023 */
div li:nth-child(2) a:hover {
    border: 10px dashed black;
}

/* specificity: 0033 */
div div .nav:nth-child(2) a:hover {
    border: 10px double black;
}
```
- A 11 class selectors combined would not overwrite the rules of one id selector! This is only an approximate example for ease of understanding.
- 하지만 113, 112 순으로 rule이 선언되어 있으면 112는 적용이 안됨.(자릿수가 이해를 돕기 위한 개념이라는 것이지 각 selector의 정량적 차이는 specificity 계산에 적용이 됨!!!)

#### !important
`!important` makes a declaration the most specific thing.

#### Example
CSS:  
```css

#winning {
    background-color: red;
    border: 1px solid black;
}
    
.better {
    background-color: gray;
    border: none !important;
}
    
p {
    background-color: blue;
    color: white;
    padding: 5px;
}           
```

HTML:  
```html
<p class="better">This is a paragraph.</p>
<p class="better" id="winning">One selector to rule them all!</p>
```

|Result:|
|:---|
|![css important ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-important-ex1.PNG?raw=true)|

- id selector가 두 번째 p에 적용되어 원래는 테두리가 있어야 하지만 class selector의 속성을 따름
	- class selector의 border declaration에 `!important`가 있기 때문에 specificity가 가장 높게 설정되었기 때문에 overriding되지 않음
- `!important`처리 되어있는 declaration을 overriding하는 방법
	- 같은 specificity를 가진, 뒤에 있는 selector의 같은 att declaration에 `!important`를 적용(source order를 이용)
	- 더 높은 specificity를 가진 selector의 같은 att declaration에 `!important` 적용

※ Don't use it if you can avoid it

### The effect of CSS location
The importance of a CSS declaration depends on what stylesheet it is specified in. It is possible for users to set custom stylesheets to override the developer's styles.

### To summarize
Conflicting declarations will be applied in the following order, with later ones overriding earlier ones:
1. Declarations in user agent style sheets (e.g. the browser's default styles, used when no other styling is set)
2. Normal declarations in user style sheets (custom styles set by a user)
3. Normal declarations in author style sheets (these are the styles set by us, the web developers)
4. Important declarations in author style sheets
5. Important declarations in user style sheets

Sometimes users have to override web developer styles. This can be achieved by using `!important` in their rules.

## CSS selectors
### What is a selector?
- The first part of a CSS Rule
- A pattern of elements and other terms tell the browser which HTML elements should be selected
- The selected element(s) are referred to as the *subject of the selector*
- Selectors are defined in the CSS Selectors specification(The majority of selectors are defined in the Level 3 Selectors specification, which is a mature specification)

### Selector lists
The individual selectors can be combined into a *selector list* so that the rule is applied to all of the individual selectors. (By adding a comma)
- White space is valid before or after the comma
- If any selector in the group is invalid, the whole rule will be ignored!

e.g.  
```css
h1,
.special {
  color: blue;
}
```

※ Types of selectors  
There are a few different groupings of selectors.(about 4 groups)

### Type, class, and ID selectors
This group includes selectors that target an HTML element, a class(`.`) or an ID(`#`).  
```css
h1 {}
.box {}
#unique {}
```

#### Type selectors
- also known as *tag name selector* or *element selector*  
e.g. `span { color: rebeccapurple; }`

#### The universal selector `*`
The universal selector(`*`) selects everything in the document(or inside the parent element). Since the universal selector makes global changes, we use it for very specific situations, such as making selectors easier to read(`article :first-child` to `article *:first-child`)

#### Class selectors `.`
**2 ways to use class selector**
- Target classes on particular elements : `span.highlight`
- Target an element has more than one class applied : `.notebox.warning`

#### ID selector `#`
- Target an ID on particular elements : `h1#heading`
- Don't use the same ID multiple times in a document!(causes strange behavior)
- Use in situations like you don't have access to the markup and cannot edit it

### Attribute selectors
The attriute selectors select **certain attribute(or with a particular value) on an element**:  
```css
a[title] {}
a[href="https://example.com"] {}
```

#### Presence and value selectors

|Selector|Example|Description|
|:---|:---|:---|
|[*attr*]|`a[title]`|elements with an *attr* attribute|
|[*attr*=*value*]|`a[href="https://example.com"]`|elements with an *attr* attribute whose value is exactly *value*|
|[*attr*~=*value*]|`p[class~="special"]`|elements with an *attr* attribute whose value is exactly *value*, or contains *value* in its (space separated)list of values|
|[*attr*&#124;=*value*]|`div[lang|="zh"]`|elements with an *attr* attribute whose value is exactly *value* or begins with *value* immediately followed by a hyphen(`-`)|

- `div[lang|="zh"]`는 `<div lang="zh-*">`를 선택함
- [*attr*=*value*]는 값이 정확히 *value*인것만(다른 값이 더 있을 경우 선택하지 않음)  
[*attr*~=*value*]는 값에 *value*가 포함된 것(whitespace-separated list에)  
즉, [class="a"]는 class="a b"인 element를 포함하지 않음!!
- [class~="a"]가 class="ab"인 element를 포함하지 않음!!(list에 원소가 ab이기 때문)

#### Substring matching selectors

|Selector|Example|Description|
|:---|:---|:---|
|[*attr*^=*value*]|`li[class^="box-"]`|elements with an *attr* attribute whose value begins with *value*|
|[*attr*$=*value*]|`li[class$="-box"]`|elements with an *attr* attribute whose value ends with *value*|
|[*attr*\*=*value*]|`li[class*="box"]`|elements with an *attr* attribute whose value contains *value* anywhere within the string|

#### Case-sensitivity
- Add `i` before the closing bracket(`]`) to match attribute values case-insensitively!  
e.g. `li[class^="a" i]` matches `<li class="Ab">`
- `s` for forcing case-sensitive, but not very useful, less supported

### Pseudo-classes and pseudo-elements
This group of selectors includes pseudo-classes, pseudo-elements.

#### Pseudo-classes
Pseudo-classes is a selector that style **certain states of an element**.  
Pseudo-classes are keywords that start with a colon.

**Simple pseudo-classes**  
They tend to act as if you had applied a class to some part of your document, often helping you cut down on excess classes in your markup, and giving you more flexible, maintainable code.
- `:first-child`, `:last-child`, `:only-child`, `:invalid` (`<input>`, `<form>`에서 입력이 invalid할 때), ...
- `article p:first-child` selects `<p>` which is first child of `<article>`
- `:first-child` is equivalent to `*:first-child`

**User-action pseudo classes**(dynamic pseudo-classes)  
They tend to act as if a class had been added to the element when the user interacts with it.
- `:hover`, `:focus`, `:link`, ...

#### Pseudo-elements
Pseudo-elements(`::`) select a **certain part of an element** rather than the element itself.  
Pseudo-elements behave in a similar way, however they act as if you had added a whole new HTML element into the markup, rather than applying a class to existing elements.  
Pseudo-elements start with a double colon `::`.  
Some early pseudo-elements used the single colon syntax, modern browsers support single- or double-colon syntax for backwards compatibility.
- `::first-line`
- `article p::first-line` selects the first line of `<p>` which is nested in `<article>`

#### Combining pseudo-classes and pseudo-elements
- `article p:first-child::first-line`

#### Generating content with ::before and ::after
These(`::before`, `::after`) are used along with the `content` property to insert content into your document using CSS. This use is referred to as "**Generated Content**" in CSS.

#### Example
```css
.box::before {
  content: "This should show before the other content.";
}
```
- `.box` 클래스가 적용된 element 전에 `content`의 property value가 표시됨
- ""을 `content`의 value로 넣고 `display: block;`을 적용해서 도형같은걸 넣을 수도 있음
- 텍스트를 value로 넣어도 브라우저에서 그 텍스트 선택 불가(~~가끔 리스트 마커가 드래그되지 않을 때가 있었는데 이렇게 추가한듯~~ list marker는 `li`의 `list-style-type`으로 조정!)

### Combinators
The combinators combine other selectors in order to target elements within our documents.

#### Descendant combinator
The descendant combinator(`' '`) combines two selectors(`A B`) such that `B` is selected if `B` has `A` as its ancestor.  
Selectors that utilize a descendant combinator are called *descendant selectors*.

#### Example
`body article p` selects `<p>` inside `<article>` which is inside `<body>`.

#### Child combinator
The child combinator(`>`) combines two selectors(`A > B`) such that `B` is selected if `B` is a direct children of `A`.  
Descendant elements further down don't match.  
The following selects paragraphs that are direct children of `<article>` elements using the child combinator(`>`):  
```css

article > p {}

```  
※ Descendant combinator `' '` selects all the descendants while child combinator(`>`) selects direct children.

#### Adjacent sibling combinator
The adjacent sibling selector(+) is placed between two CSS selectors(`A + B`). It matches only those elements matched by the `B` that are the next sibling element of the `A`.  
A common use case is to do something with a paragraph that follows a heading, such as *abstract*.

#### Example
`h1 + p` selects paragraphs after `<h1>`

#### General sibling combinator
The general sibling combinator(`~`) combines two selectors(`A ~ B`). It selects all the B that are siblings of A, even not directly adjacent.

#### Example
`p ~ img` selects all `<img>` elements that come anywhere **after** `<p>` elements.

#### Using combinators
> Take care however when creating big lists of selectors that select very specific parts of your document. It will be hard to reuse the CSS rules as you have made the selector very specific to the location of that element in the markup.
>
> It is often better to create a simple class and apply that to the element in question. That said, your knowledge of combinators will come in very useful if you need to get to something in your document and are unable to access the HTML, perhaps due to it being generated by a CMS.

## The box model
### Block and inline boxes
In CSS, there are broadly two types of boxes - **block boxes** and **inline boxes**. These characteristics refer to how the box behaves in terms of page flow, and in relation to other boxes on the page:

### Block box
- The box will break onto a new line.
- The box will extend in the inline direction to fill the space available in its container.
- The `width` and `height` properties are respected.
- Padding, margin and border will cause other elements to be pushed away from the box.

By default, headings and `<p>` use `block` as their outer display type.

### Inline box
- The box will not break onto a new line.
- The `width` and `height` properties will not apply.
- Vertical padding, margins, and borders will apply but will not cause other inline boxes to move away from the box.
- Horizontal padding, margins, and borders will apply and will cause other inline boxes to move away from the box.

By default, `<a>`, `<span>`, `<em>`, `<strong>` display inline.

The type of box(`block`, `inline`) is defined by `display` property and these are the **outer** value of `display`.

### Aside: Inner and outer display types
Boxes have an *inner* display type which dictates how elements inside that box are laid out.(cf. *outer* display type : `block` / `inline`)  
By default, the elements inside a box are laid out in **normal flow**(just like any other block and inline elements)
With `display: flex;`, the outer display type is `block`, but the inner display type is changed to `flex`.(There are various other inner values such as `grid`)

### Examples of different display types
CSS:  
```css
p, 
ul {
  border: 2px solid rebeccapurple;
  padding: .5em;
}

.block,
li {
  border: 2px solid blue;
  padding: .5em;
}

ul {
  display: flex;
  list-style: none;
}

.block {
  display: block;
}      
```

HTML:  
```html
<p>I am a paragraph. A short one.</p>
<ul>
  <li>Item One</li>
  <li>Item Two</li>
  <li>Item Three</li>
</ul>
<p>I am another paragraph. Some of the <span class="block">words</span> have been wrapped in a <span>span element</span>.</p>
```

|Result:|
|:---|
|![display type ex1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-display-type-ex1.png?raw=true)|

CSS:  
```css
p, 
ul {
  border: 2px solid rebeccapurple;
}

span,
li {
  border: 2px solid blue;
}

ul {
  display: inline-flex;
  list-style: none;
  padding: 0;
} 

.inline {
  display: inline;
}
```

HTML:  
```html
<p>
    I am a paragraph. Some of the
    <span>words</span> have been wrapped in a
    <span>span element</span>.
</p>     
<ul>
  <li>Item One</li>
  <li>Item Two</li>
  <li>Item Three</li>
</ul>
<p class="inline">I am a paragraph. A short one.</p>
<p class="inline">I am another paragraph. Also a short one.</p>
```

|Result:|
|:---|
|![display type ex2](https://github.com/siriyaoff/MDN-note/blob/master/images/css-display-type-ex2.png?raw=true)|

- `block` : 새로운 줄에서 시작, 너비 지정 없으면 부모 노드의 너비를 모두 차지, `span`과 같은 inline element에도 `display: block;`을 부여할 수 있음, 반대도 가능(`ul`에 inline 부여)
- `inline` : 줄바꿈 없음, '글자처럼 취급'이랑 비슷
- `flex` : 적용 대상 element에 자식노드가 있어야 함(flex를 부여하면 자식노드들이 flex하게 display됨), 부모노드는 block인데 부모노드가 차지한 영역을 flex하게 자식노드들이 나눠가짐
- `inline-flex` : 부모노드가 inline element로 display되고 자식노드들을 표시하는데 필요한 공간만큼만 차지함, 줄바꿈 없음

### What is the CSS box model?
The full CSS box model applies to block boxes(inline boxes use only some of the behavior defined in the box model).

#### Parts of a box
Layers in the block box:  
![diagram of the box](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model/box-model.png)
- Content box : content area
	- size : `width`, `height`
- Padding box : padding around the content as white space
	- size : `padding` and related properties
- Border box : border box wraps the content and any padding
	- size and style : `border` and related properties
- Margin box : outermost layer, wrapping the content, padding and border as whitespace between this box and other elements
	- size : `margin` and related properties

#### The standard CSS box model
In the standard box model, `width` and `height` defines the width and height of the *content box*. Then any padding and border is added.

#### Example
CSS:  
```css
.box {
  width: 350px;
  height: 150px;
  margin: 10px;
  padding: 25px;
  border: 5px solid black;
}
```

|Result:|
|:---|
|![standard box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model/standard-box-model.png)|

The space taken up by the box using the standard box model will be 410px(350+25+25+5+5) * 210px(150+25+25+5+5).  
**Note**: The margin is not counted towards the actual size of the box. It affects only the space outside the box. The box's area stops at the border.(보여지는 박스의 크기는 border까지임)

#### The alternative CSS box model
In the alternative box model, `width` is the width of the visible box(width to the border). Therefore the content area width is `width` minus the width for the padding and border.  

#### Example
The same CSS as used above would give the below result.  
![alternative box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model/alternate-box-model.png)

By default, browsers use the standard box model.  
Use `box-sizing: border-box;` to turn on the alternative model.  
To set all the elements to use the alternative box model:  
```css
html {
  box-sizing: border-box;
}
*, *::before, *::after {
  box-sizing: inherit;
}
```

> Internet Explorer used to default to the alternative box model, with no mechanism available to switch.

### Margins, padding, and borders
#### Margin
- invisible space around an box.
- can have positive or negative values
- longhand properties : `margin-top`, `margin-right`, `margin-bottom`, `margin-left`

**Margin collapsing**  
If there are two elements whose margins touch,
- both margins are positive : those margins will combine to become one margin, bigger of the two
- one or both margins are negative : the amount of negative value will subtract from the total(하나만 음수면 더한 값을 사용, 둘 다 음수면 둘 중 더 작은 값을 사용)

#### Borders
There are four borders(*top*, *right*, *bottom*, *left*), and each border has a *style*, *width* and *color* that we might want to manipulate.

#### Example 
```css
border: 1px groove grey;
border-top: 1px double grey;
border-style: dashed ridge none dotted;
border-right-width: 2px;
border-bottom-color: blue;
```
- 방향이 포함된 properties에서는 모양(1px double grey 같이)을 shorthand로 사용할 수 있고, 모양이 포함된 properties에서는 방향을 shorthand로 사용할 수 있음
- 뱡향과 모양을 한꺼번에 shorthand로 사용할 수는 없음(`border: 1px solid black 2px double pink` 이런거 안됨)

#### Padding
- space between the border and the content area
- no negative values
- longhand properties : `padding-top`, `padding-right`, `padding-bottom`, `padding-left`

### The box model and inline boxes
As we mentioned above at the **Inline boxes**,
- `width` and `height` are ignored
- vertical margin and padding are respected but don't change the relationship of other content to our inline box
- horizontal margin and padding are respected and cause other content to move away from the box

#### Example
CSS:  
```css
span {
  margin: 20px;
  padding: 20px;
  width: 80px;
  height: 50px;
  background-color: lightblue;
  border: 2px solid blue;
}
```

HTML:  
```html
<p>
    I am a paragraph and this is a <span>span</span> inside that paragraph. A span is an inline element and so does not respect width and height.
</p>
```

|Result:|
|:---|
|![inline box ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-inline-box-ex.png?raw=true)|

### Using display: inline-block
`inline-block` is a middle ground between `inline` and `block`.
- The `width` and `height` properties are respected
- `padding`, `margin`, and `border` will cause other elements to be pushed away from the box  
=> avoid the overlapping like above, but inline

#### Example
CSS:  
```css
span {
  margin: 20px;
  padding: 20px;
  width: 80px;
  height: 50px;
  background-color: lightblue;
  border: 2px solid blue;
  display: inline-block;
}
```

HTML:  
```html
<p>
    I am a paragraph and this is a <span>span</span> inside that paragraph. A span is an inline element and so does not respect width and height.
</p>
```

|Result:|
|:---|
|![inline block ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-inline-block-ex.png?raw=true)|

- 저 예제에서는 80!=20+20+2+2이므로 standard box model 사용중
- `<p>`는 block element이기 때문에 `<span>`에 `display: block;`을 적용시켜도 줄만 바뀔 뿐 p의 border가 두 개로 나눠지지 않음!
- nav bar같은거 만들 때 `<a>`의 링크 클릭 범위를 넓힐 때 inline-block 많이 사용(padding 넣어서 영역 넓히고 이게 overlapping되지 않도록 해줌)

## Backgrounds and borders
### Styling backgrounds in CSS
#### Background colors
A `background-color` extends underneath the content and padding box of the element.

#### Background images
A `background-image: url(/*image url*/);` displays an image pointed by the url.  
A background image displays on top of the background color.  
By default,
- The large image is not scaled down to fit
- The small image is tiled to fill the box.

**Controlling background-repeat**  
A `background-repeat` property is used to control the tiling behavior of images.  
The available values are `no-repeat`, `repeat-x`, `repeat-y`, `repeat`.  
e.g. `background-repeat: no-repeat;`

**Sizing the background image**  
A `background-size` property sizes the image to fit inside the background.  
It can take length(`100px` or `10em`) percentage(`100%`) values, or keywords(`cover`, `contain`).
- length, percentage values : 지정한 크기로 이미지를 scale
	- 값을 하나로 지정 : image의 aspect ratio 유지, width를 그 값으로 설정
	- 두 개로 지정 : aspect ratio 무시, width, height를 설정(1000px 등으로 크게 설정하면 box 바깥으로 나감)
- `cover` : aspect ratio 유지, box가 채워지도록 크기 조정
	- image 잘릴 수 있음
	- box가 세로로 길 경우 `background-size: 100%;`는 width를 맞추기 때문에 밑에 빈공간이 남을 수 있지만, `cover`는 height를 100%로 맞춰서 box를 채움
- `contain` : aspect ratio 유지, image가 box안에 들어오도록 설정(이미지가 작으면 확대함)

Box, image aspect ratio에 따른 size 설정  
box의 ratio > image의 ratio  
![background size ex1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-background-size-ex1.png?raw=true)  
box의 ratio < image의 ratio  
![background size ex2](https://github.com/siriyaoff/MDN-note/blob/master/images/css-background-size-ex2.png?raw=true)

**Positioning the background image**  
The `background-position` property set the position of the background image on the box.  
The top-left-hand corner of the box has coordinate `(0, 0)`(it is also the default `background-position` value).  
The most common `background-position` values take two individual values(a horizontal value followed by a vertical value).  
It can take lengths, percentages, and keywords(`top`, `bottom`, `right`, `left`, `center`).  
`background-position` 은 `background-position-x`, `background-position-y`의 shorthand임에 유의

#### Example
```css
background-position: top center;
background-position: 20px 10%;
background-position: 20px top;
background-position: top 20px right 10px;
```
- lengths, percentages : 하나만 적을 경우 horizontal로 적용되고 vertical은 center로 설정됨
- keywords : `top center`로 적든 `center top`으로 적든 알아서 적용됨(center는 horizontal, vertical에 둘다 적용가능하지만 나머지는 같은 축끼리 쓰면 적용안됨)
- keywords와 lengths or percentages를 섞어서 사용할 수 있음
- `top 20px right 10px`(위에서 20px, 오른쪽에서 10px 떨어지게 위치)와 같이 4-value syntax도 사용 가능

#### Gradient backgrounds
A gradient - when used for a background - acts just like an image and is also set by using the `background-image` property.

#### Example
```css
background-image: linear-gradient(105deg, rgba(0,249,255,1) 39%, rgba(51,56,57,1) 96%);

background-image: radial-gradient(circle, rgba(0,249,255,1) 39%, rgba(51,56,57,1) 96%);
background-size: 100px 100px;
```
- We can set the size of gradients with the `background-size`, and the gradients will be repeated by default.

#### Multiple background images
It is possible to have multiple background images in a single property value, by separating with commas.

#### Example
```css
background-image: url(image1.png), url(image2.png), url(image3.png), url(image4.png);
background-repeat: no-repeat, repeat-x, repeat;
background-position: 10px 20px,  top right;
```
- The last listed image will be at the bottom layer.  
- The other `background-*` properties can also have comma-separated values.
- comma로 구별된 대로 properties가 부여되지만, 수가 맞지 않은 경우 property가 반복됨(위의 경우 position value가 순서대로 반복 -> image3은 `10px 20px;`, image 4는 `top right;`)

#### Background attachment
The `background-attachment` property can controll how the backgrounds scroll when the content scrolls.  
It can take the following values:
- `scroll` : background를 element box에 고정 => element scroll은 background를 움직이지 않음(딸려 올라가지 않음), page scroll은 움직임(딸려 올라감)
- `fixed` : background를 viewport에 고정 => element scroll, page scroll 둘 다 background를 움직이지 않음
- `local` : background를 element content에 고정 => element scroll, page scroll 둘 다 background를 움직임

#### Using the background shorthand property
We can specify backgrounds by the shorthand `background`.  
A few rules to use shorthand values:
- if using multiple backgrounds, separate them by comma
- `background-color`(solid background) may only be specified after the final comma
- the value of `background-size` must be included immediately after `background-position`, separated with the `/` character, such as `center / 80%`

#### Example
```css
.box {
  background:   
    linear-gradient(105deg, rgba(255,255,255,.2) 39%, rgba(51,56,57,1) 96%) center center / 400px 200px no-repeat,
url(big-star.png) center no-repeat, 
    rebeccapurple;
}
```

#### Accessibility considerations with backgrounds
If specifying an image, and text will be placed on top of that image, you should also specify a `background-color`to make the text to be legible whenever the image loaded or not.

Screen readers cannot parse background images, therefore they should be purely decoration; any important content should be part of the HTML page and not contained in a background.

### Borders
Typical usage는 위에서 말한 그대로임

#### Rounded corners
The `border-radius` property gives a box rounding corners.  
Associated longhands : `border-top-left-radius`, `border-top-right-radius`, `border-bottom-right-radius`, `border-bottom-left-radius`.(clockwise)  
Two lengths or percentages can be used as a value, the *horizontal radius* and *vertical radius*(horizontal radius는 border의 width 중 둥글어지는 길이를 나타냄, vertical은 height 중).  
- `border-radius`로 horizontal, vertical까지 설정할 수 없음(값 여러 개 입력하면 longhand에 대한 입력을 들어감, 8개 넣으면 적용안됨)

## Handling different text directions
### What are writing modes?
A writing mode in CSS refers to whether the text is running horizontally or vertically.  
The `writing-mode` property switch from one writing mode to another.  
The three possible values for the writing-mode:
- `horizontal-tb` : top-to-bottom block flow direction, horizontal sentences
- `vertical-rl` : right-to-left block flow direction, vertical sentences
- `vertical-lr` : left-to-right block flow direction, vertical sentences

### Writing modes and block and inline layout
In `writing-mode: horizontal-tb`, sentences flow horizontally and blocks are displayed vertically, and vice versa.  
When we switch the writing mode, the directions of inline, block is changed.  
The directions are also called as **dimensions**.  
The **block dimension** is always the direction blocks are displayed on the page, and the **inline dimension** is always the direction a sentence flows.

|horizontal writing mode|vertical writing mode|
|:---|:---|
|![horizontal writing mode](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Handling_different_text_directions/horizontal-tb.png)|![vertical writing mode](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Handling_different_text_directions/vertical.png)|

#### Direction
Arabic과 같이 horizontal하지만 right-to-left로 읽고 쓰는 언어도 있음 -> 이런 언어들도 있기 때문에 newer CSS layout methods들은 텍스트의 *start*와 *end*도 지정함

### Logical properties and values
A lot of properties are tied to the physical dimensions of the screen, and make most sense when in a horizontal writing mode.  

#### Example
CSS:  
```css
.box {
  width: 150px;
}

.horizontal {
  writing-mode: horizontal-tb;
}

.vertical {
  writing-mode: vertical-rl;
}
```

HTML:  
```html
<div class="wrapper">
  <div class="box horizontal">
    <h2>Heading</h2>
    <p>A paragraph. Demonstrating Writing Modes in CSS.</p>
    <p>These boxes have a width.</p>
  </div>
  <div class="box vertical">
    <h2>Heading</h2>
    <p>A paragraph. Demonstrating Writing Modes in CSS.</p>
    <p>These boxes have a width.</p>
  </div>
</div>
```

|Result:|
|:---|
|![text overflow ex1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-text-overflow-ex1.png?raw=true)|

In the example above, the box with a vertical writing mode still has a width, and this causing the text to overflow.  
It is needed to swap height and width along with the writing mode. For example, when we're in a vertical writing mode we want the box to expand in the block dimension.  
=> CSS developed a set of mapped properties which replace physical properties with **logical**, or **flow relative** versions.
- `inline-size`
	- a property mapped to `width` when in a horizontal writing mode
	- sizes the inline dimension
- `block-size`
	- a property mapped to `height` when in a horizontal writing mode
	- sizes the block dimension

`inline-size: 150px;`를 이용하면 위에서와 같이 vertical writing mode를 이용하더라도 horizontal과 같이 너비 설정이 제대로 적용됨  
![text overflow ex2](https://github.com/siriyaoff/MDN-note/blob/master/images/css-text-overflow-ex2.png?raw=true)

#### Logical margin, border, and padding properties
There are many instances of physical properties, for example, `margin-top`, `padding-left`, and `border-bottom`.  
In the same way for width and height, there are mappings for these properties.
- `*-top` mapped to `*-block-start`
- `*-right` mapped to `*-inline-start`
- `*-bottom` mapped to `*-block-end`
- `*-left` mapped to `*-inline-end`

#### Logical values
There are also logical mappings for values like `top`, `right`, `bottom`, and `left`.  
They are same with the words above.  
※ chrome, edge는 `float` property에 대해 flow relative values 지원 안함, firefox만 하는중

#### Should you use physical or logical properties?
The logical properties and values have only recently been implemented in browsers. Therefore you have to **check how far back the browser support goes** before you use the logical values. For now, you prefer to use the physical versions unless using multiple writing modes. However, most things will transition to the logical versions when we start dealing with layout methods such as flexbox and grid.

## Overflowing content
### What is overflow?
Everything in CSS is a box. Overflow happens when there is too much content to fit in a box.

### CSS tries to avoid "data loss"
If we restrict the width or height of a box, there may be overflow. However CSS does not hide content wherever possible, regardless of overflow. This is because of data loss. The problem with data loss is that you and visitors may not notice.

Instead, CSS overflows in visible ways. Then you or visitors will know that content is overlapping.

CSS assumes that you are managing the potential for overflow. In general, restricting the block dimension is problematic when the box contains text. There may be more text than you expected when designing the site, or the text may be larger.

We can control sizing in ways that are less prone to overflow. However, if a fixed size needed, we can also control how the overflow behaves.

### The overflow property
The `overflow` property instruct the browser how it should behave.  
It can take the following values:
- `visible` : default value
- `hidden` : crop content when it overflows(= hide overflow)
- `scroll` : add scrollbars always(even when it doesn't overflow)
- `auto` : add scrollbars when it overflows(block dimension으로만)

There are also longhand properties `overflow-x`, `overflow-y`
- x or y축만 스크롤바 생김, 잘못 설정하면 스크롤이 아예 안되고 data loss일어남
- shorthand로 쓸 경우 x부터 설정
- 여기서 x, y는 vertical writing mode라도 고정임

If you have a long word in a small box, consider using the `word-break` or `overflow-wrap`.
- [`word-break`](https://developer.mozilla.org/en-US/docs/Web/CSS/word-break) : `normal`, `break-all`, `keep-all`, `break-word` 4개의 value를 가짐
	- `normal` : 긴 단어 보존(overflow), CJK(Chinese, Japanese, Korean)는 box에 맞춤
	- `break-all` : 모든 언어들에 대해 box에 맞춤
	- `keep-all` : 모든 언어들에 대해 그대로 보존
	- `break-word` : `normal`과 비슷, 요새 쓰지 않음
- [`overflow-wrap`](https://developer.mozilla.org/en-US/docs/Web/CSS/overflow-wrap) : `normal`, `anywhere`, `break-word` 3개의 value를 가짐

### Overflow establishes a Block Formatting Context
`overflow` property에 `scroll`, `auto`, `hidden`을 사용하면 그 element에 **Block Formatting Context**(BFC)가 생성됨  
BFC가 생성되면 그 안에 있는 모든 element들은 BFC가 생성된 element의 box안에 속하게 됨(float여도 속함)  
밖에서 BFC가 생성된 element 안으로도 다른 element가 침범할 수 없음

### Unwanted overflow in web design
When developing a site, always keep overflow in mind. Generally ensure that your CSS works in a robust way.

## CSS values and units
Every property used in CSS has a value type defining the set of values that are allowed for that property.

### What is a CSS value?
- CSS specification이나 MDN property pages에서, 각 property에 대해 사용가능한 value type을 `<color>`, `<length>`와 같이 명시해놓음  
- CSS values are also referred to as *data types*
- value types는 property와 구분을 위해서 angle brackets를 사용함(e.g. `color`, `<color>`과 같이), html elements와 헷갈리지 않게 주의!
- If you see `<color>` as valid, you can use all the values in `<color>`(assuming your browser support them)

### Numbers, lengths, and percentages
Numeric value types:

|Data type|Description|Example|
|:---|:---|:---|
|`<integer>`|whole number|`1024` or `-55`|
|`<number>`|decimal number(+fractional componenet)|`0.255`, `128`, `-1.2`|
|`<dimension>`|`<number>` with a unit attached<br>an umbrella category that includes the `<length>`, `<angle>`, `<time>`, and `<resolution>` types|`45deg`, `5s`, `10px`|
|`<percentage>`|fraction of some other value|`50%`|

#### Lengths
There are two types of lengths, relative and absolute.

**Absolute length units**  
These are always the same size.

|Unit|Name|Equivalent to|
|:---|:---|:---|
|`cm`|Centimeters|1`cm` = 38`px`|
|`mm`|Millimeters|1`mm` = 1/10th of 1`cm`|
|`Q`|Quarter-millimeters|1`Q` = 1/40th of 1`cm`|
|`in`|Inches|1`in` = 96`px`|
|`pc`|Picas|1`pc` = 1/6 of 1`in`|
|`pt`|Points|1`pt` = 1/72th of 1`in`|
|`px`|Pixels|1`px` = 1/96th of 1`in`|

The only value that you will commonly use is `px`.

**Relative length units**  
These are relative to something else, perhaps the size of the parent element's font.

|Unit|Relative to|
|:---|:---|
|`em`|Font size of the parent in the case of typographical properties like `font-size`,<br>font size of the element itself in the case of other properties like `width`|
|`ex`|x-height of the element's font|
|`ch`|The advance measure(width) of the glyph "0" of the element's font|
|`rem`|Font size of the root element|
|`lh`|Line height of the element|
|`vw`|1% of the viewport's width|
|`vh`|1% of the viewport's height|
|`vmin`|1% of the viewport's smaller dimension|
|`vmax`|1% of the viewport's larger dimension|

- `ex`는 `em`의 절반
- `rem`은 root element의 font-size 기준, `em`는 parent의 font-size 기준 -> nested element의 경우 `em`으로 글자설정하면 계속 커짐!

#### Percentages
Percentages are always set relative to some other value.  
For example, `font-size: 110%;` sets the font size to 110% of its parent's font size.(similar to `em`)  
- 보통 부모 element의 값을 기준으로함
- `<length>`만 사용가능한 element가 있음(`<length-percentage>`가 사용가능하면 percentage도 사용가능, `<length>`면 percentage는 불가능)

#### Numbers
Some value types accept numbers, without any unit added to them.  
For example, `opacity` property accepts a unitless number. `0`(fully transparent) to `1`(fully opaque).  
`opacity: 0.6;`

※ A number as a value in CSS should not be surrounded in quotes.

### Color
There are many ways to specify color in CSS.  
The standard color system is 24bit, 16.7 million(256 x 256 x 256) colors.

#### Color keywords
simple and understandable  
`rebeccapurple`

#### Hexadecimal RGB values
Each hex value consists of a hash/pound symbol(`#`) followed by six hexadecimal numbers(0 to f)  
`#ffdead`

#### RGB and RGBA values
These are functions.  
`rgb(R, G, B)` : represents RGB channel values by decimal numbers(0 to 255)  
`rgba(R, G, B, a)` : similar to `rgb()` but alpha channel added(0 : fully transparent, 1 : fully opaque)
- property `opaque`는 element 전체의 opacity를 설정하는 반면 `rgba()`의 alpha value는 설정한 색에 대해서만 투명도를 설정함!
- `rgba()`와 `rgb()`, `hsl()`과 `hsla()`은 언제부턴가 서로 완전히 같은 함수로 작동함(rgb에 a 붙여서 사용해도 정상작동) 따라서 아무거나 써도 상관없지만, transparent color가 정의되어있다는 것을 표현하기 위해 rgba를 사용하는 것이 좋음

#### HSL and HSLA values
`hsl(Hue, Saturation, Lightness)` is slightly less well-supported than RGB.  
- Hue(색조)
	- The base of the color
	- [0, 360], representing the angles around a color wheel(`0` : red, `120` : green, `240` : blue)
- Saturation(채도)
	- How saturated is the color?
	- [0, 100] (%), `0%` is no color(shade of grey), `100%` is full color saturation
- Lightness(밝기)
	- How light or bright is the color?
	- [0, 100] (%), `0%` is no light(completely dark), `100%` is full light(completely white)

### Images
The `<image>` value type is used wherever an image is a valid value.  
This can be an **actual image file** pointed to via a `url()` function, or a **gradient**(e.g. `linear-gradient()`).

### Position
The `<position>` value type represents a set of 2D coordinates.  
It can take keywords such as `top`, `left`, `bottom`, `right`, and `center`.  
It aligns items with specific bounds of a 2D box, along with lengths, which represent offsets from the top and left-hand edges of the box.  

- consists of two values - the horizontal position, the vertical position.
- 하나의 축에 대해서만 값을 지정할 경우 나머지 하나는 `center`로 default됨
- `right 40px` : right, 40 from the top

### Strings and identifiers
Keywords(`red`, `black`, ...) are more accurately described as *identifiers*.  
You can use strings(double quotes) when specifying generated content(in pseudo-element).

### Functions
In CSS, functions exist as property values, such as `rgb()`, `hsl()`, `url()`.  
A `calc()` does simple calculations inside CSS.  
e.g. `calc(20% + 100px)`

## Sizing items in CSS
### The natural or intrinsic size of things
- **Intrinsic size** : a size **defined by its content**
- empty `<div>`는 스스로의 크기가 없음  
-> `<div>`만 선언할 경우 하나의 선으로 나타남(block level element이기 때문에 width는 parent element의 width와 같지만 height는 없음  
-> 안에 text를 추가하면 사이즈가 생기고, 이게 `<div>`의 instric size임(안의 content에 의해 결정된 size)

### Setting a specific size
- **Extrinsic size** : a **size given** to an element, by `width` and `height` values
- Because of overflow, fixing the height with lengths or percentages need to be done carefully

#### Using percentages
Percentages resolve against the size of the containing block.

#### Percentage margins and padding
When you set margin and padding in percentages, the value is calculated from the **inline size** of the containing block.
- `margin: 10%; padding: 10%;` : margins, paddings 모두 width의 10%(horizontal writing mode일 때)

### min- and max- sizes
`min-height` property makes the box to be always at least the height.  
A common use of `max-width` is to cause images to scale down if there is not enough space to display them at their intrinsic width while making sure they don't become larger than that width.  

#### Example
CSS:  
```css
.box {
  width: 200px;
}
.minibox {
  width: 50px;
}
.width {
  width: 100%;
}
.max {
  max-width: 100%;
}
```

HTML:  
```html
<div class="wrapper">
  <div class="box"><img src="star.png" alt="star" class="width"></div>
  <div class="box"><img src="star.png" alt="star" class="max"></div>
  <div class="minibox"><img src="star.png" alt="star" class="max"></div>
</div>
```

|Result:|
|:---|
|![max width ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-max-width-ex.png?raw=true)|

- `max-width: 100%`를 이용하면 이미지를 responsive하게 만들면서 크기를 박스 이상으로 커지지 않게 만들 수 있음

### Viewport units
Viewport : the visible area of your page in the browser you are using to view a site

`vw`
- unit for viewport width
- `1vw` is equal to 1% of the viewport width

`vh`
- unit for viewport height
- `1vh` is equal to 1% of the viewport height

Viewport units can be useful in your designs(e.g. hero section: set width to 100vh)
- `box-sizing: border-box`일 경우 alternative box model이 적용되기 때문에 `width: 60%;`, `padding: 10%;`를 적용하면 width는 60% 그대로 남고 height만 증가함

## Images, media, and form elements
### Replaced elements
Certain replaced elements(images, video) have an **aspect ratio** as default.

### Sizing images
`box`라는 `<div>`안에 `<img>`를 넣어놓은 상태  
box에 `width: 100px;`를 적용하고 img를 넣으면 overflow할 수도 있음(이미지가 작은 경우에는 이미지가 늘어나진 않음)
=> img에 `max-width: 100%;`를 적용하면 이미지가 box보다 더 클 경우 box의 너비에 맞춰짐

`object-fit` property
- `object-fit: cover;`를 img에 적용시키면 img가 box를 꽉 채움(aspect ratio를 유지)
- `object-fit: contain;`를 img에 적용시키면 img가 box안에 들어감(aspect ratio를 유지하면서 들어가기 때문에 box에 빈 공간이 남음)

#### Example
CSS:  
```css
.box {
  width: 200px;
  height: 200px;
}

img {
  height: 100%;
  width: 100%;
}

.cover {
  object-fit: cover;
}

.contain {
  object-fit: contain;
}
```

HTML:  
```html
<div class="wrapper">
  <div class="box"><img src="balloons.jpg" alt="balloons" class="cover"></div>
  <div class="box"><img src="balloons.jpg" alt="balloons" class="contain"></div>
</div>
```

|Result:|
|:---|
||![object fit ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-object-fit-ex.PNG?raw=true)|

- img의 `width`, `height`를 둘 다 100%로 설정해놓은 상태라 `object-fit` 속성을 선언해놓지 않으면 box를 채움(`object-fit: fill;`과 같음, img의 aspect ratio를 무시하고 box를 채워버림)

### Replaced elements in layout
In a flex or grid layout, elements are stretched by default to fill the entire area.  
Images will not stretch, and instead will be aligned to the start of the grid area or flex container.  
To force the image to stretch to fill the grid cell it is in,  
```css
img {
  width: 100%;
  height: 100%;
}
```

### Form elements
`<input>`, `<textarea>`, `<fieldset>`, `<legend>` 등을 이용해 form controls를 더할 수 있음

#### Styling text input elements
`<input type="text">`, `<textarea>`와 같은 elements는 다른 것들과 비슷함  
`input[type="text]`와 같이 selector를 선언하여 css를 적용할 수 있음

form elements는 os, browser마다 다르게 렌더링하기 때문에 다양한 환경에서 테스트 필요

#### Inheritance and form elements
In some browsers, form elements do not inherit font styling by default. Therefore if you want to be sure that your form fields use the font defined on the body, or on a parent element, you should add this rule to your CSS.  
```css
button,
input,
select,
textarea {
  font-family: inherit;
  font-size: 100%;
}
```

#### Form elements and box-sizing
Across browsers form elements use different box sizing rules for different widgets.  
For consistency it is a good idea to set margins and padding to `0` on all elements, then add these back in when styling particular controls.  
```css
button,
input,
select,
textarea {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
```

#### Other useful settings
```css
textarea {
  overflow: auto;
}
```

#### Putting it all together into a "reset"
We can wrap up the various properties discussed above into the following "form reset" to provide a consistent base to work from.  
```css
button,
input,
select,
textarea {
  font-family: inherit;
  font-size: 100%;
  box-sizing: border-box;
  padding: 0; margin: 0;
}

textarea {
  overflow: auto;
} 
```

지금은 browsers가 typically consistent하기 때문에 예전만큼 normalizing이 중요하지는 않음  
normalize.css에서 다른 base stylesheet 확인 가능

### Testing your skills
img에 `object-fit` property를 적용할 때 `width`, `height`가 설정되어 있어야 함  
`object-fit`는 width, height가 정해졌을 때 img의 aspect ratio를 기준으로 `cover`, `fill`, `contain`을 설정하는 것임  
`<div>` 안에 `<img>`를 aspect ratio를 유지하면서 div를 채우게 하려면 width, height를 100%로 설정한 다음 `object-fit: cover;`를 적용해야함  
- 둘 다 설정하지 않으면 img의 원래 화질대로 나옴
- width, height 중 하나만 설정해놓으면 aspect ratio에 맞춰서 img의 크기가 정해짐 => `object-fit: cover;`가 적용되지 않음
- img를 nest하는 것과 background로 넣는 것 이렇게 두 가지 방법이 있음
	- img를 nest할 경우 default position이 center
	- background로 넣을 경우 default position이 0 0
	- `object-position`, `background-position` property로 설정 가능

img같은 replaced elements의 `overflow` 관련 property는 overflow를 일으키는 요소에 적용하는게 아니라 부모 요소에 적용해야함  
cf. text의 overflow는 `<p>`같은 element에 직접 적용함

## Styling tables
### A typical HTML table
`scope` attribute, `<caption>`, `<thead>`, `<tfoot>` 등을 이용해서 HTML table markup 가능
=> cramped

### Styling our table
```css
table {
  table-layout: fixed;
  width: 100%;
  border-collapse: collapse;
  border: 3px solid purple;
}

thead th:nth-child(1) {
  width: 30%;
}

thead th:nth-child(2) {
  width: 20%;
}

thead th:nth-child(3) {
  width: 15%;
}

thead th:nth-child(4) {
  width: 35%;
}

th, td {
  padding: 20px;
}
```
- `table`에 `table-layout: fixed;`를 적용하면 첫 번째 row를 기준으로 column width가 고정됨<br>=> subsequent rows에서 width가 맞지 않을 수 있음, `overflow` property를 이용해서 조절해야함<br>cf. `table-layout: auto;`가 default, 자동으로 열 너비 설정함(overflow 발생하지 않게)<br>`fixed`로 설정하면 table headings를 이용해서 열 너비 설정 가능
- `thead th:nth-child(n)` selector를 이용해서 table headings의 width를 설정
- `table`의 width를 100%로 설정, th들은 table의 width를 나눠가짐(30%, 20%, 15%, 35%)
- `table`에 `border-collapse: collapse;`를 사용하면 중복되는 테두리가 하나만 나타남<br>![css-border-collapse-ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-border-collapse-ex.PNG?raw=true)
- `th`, `td`에 padding 추가 => 가독성 증가

#### Some simple typography
```css
html {
  font-family: 'helvetica neue', helvetica, arial, sans-serif;
}

thead th, tfoot th {
  font-family: 'Rock Salt', cursive;
}

th {
  letter-spacing: 2px;
}

td {
  letter-spacing: 1px;
}

tbody td {
  text-align: center;
}

tfoot th {
  text-align: right;
}
```
- `letter-spacing` : 자간

#### Graphics and colors
```css
thead, tfoot {
  background: url(leopardskin.jpg);
  color: white;
  text-shadow: 1px 1px 1px black;
}

thead th, tfoot th, tfoot td {
  background: linear-gradient(to bottom, rgba(0,0,0,0.1), rgba(0,0,0,0.5));
  border: 3px solid purple;
}
```
- `text-shadow: 1px 1px 1px black;` : offset-x, offset-y, blur-radius, color
- multiple backgrounds, linear gradients를 지원하지 않는 browsers를 위해 background를 분리해서 넣음

**Zebra stripping**  
```css
tbody tr:nth-child(odd) {
  background-color: #ff33cc;
}

tbody tr:nth-child(even) {
  background-color: #e495e4;
}

tbody tr {
  background-image: url(noise.png);
}

table {
  background-color: #ff33cc;
}
```
- `nth-child([odd/even])`으로 홀수/짝수 행 선택 가능, formula(`2n-1`, `2n`과 같이)도 인자로 넣을 수 있음
- 맨 마지막 `table`의 background는 `nth-child` pseudo-class selector를 지원하지 않는 browser을 위한 것

#### Styling the caption
- `caption-side: bottom;`을 통해서 caption의 위치 지정 가능

### Table styling quick tips
- Make your table markup as simple as possible, and keep things flexible, e.g. by _using percentages_, so the design is more reponsive.
- Use `table-layout: fixed;`<br>to create a more predictable table layout that allows you to easily _set column widths by setting_ `width` _on their headings_(`<th>`).
- Use `border-collapse: collapse;`<br>to make table elements borders collapse into each other, producing a neater and easier to control look.
- Use `<thead>`, `<tbody>`, and `<tfoot>`<br>to break up your table into logical chunks and provide extra places to apply CSS to, so it is easier to layer styles on top of one another if required.
- Use zebra striping to make alternative rows easier to read.
- Use `text-align`<br>to line up your `<th>` and `<td>` text, to make things neater and easier to follow

### Test your skills
CSS:  
```css
th, td {
  padding: 5px;
}

tr :nth-child(2),
tr :nth-child(3) {
  text-align: right;
}

tr :nth-child(1),
tr :nth-child(4) {
  text-align: left;
}

tfoot tr :nth-child(1) {
  text-align: right;
}

tfoot tr :nth-child(2){
  text-align: left;
}

table {
  border-collapse: collapse;
  border-top: 1px solid #eeeeee;
}

tfoot {
  border-top: 1px solid #eeeeee;
  border-bottom: 1px solid #eeeeee;
}

tbody tr:nth-child(odd) {
  background: #eeeeee;
}

thead {
  vertical-align: top;
}
```

HTML:  
```html
 <table>
  <caption>A summary of the UK's most famous punk bands</caption>
  <thead>
    <tr>
      <th scope="col">Band</th>
      <th scope="col">Year formed</th>
      <th scope="col">No. of Albums</th>
      <th scope="col">Most famous song</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Buzzcocks</th>
      <td>1976</td>
      <td>9</td>
      <td>Ever fallen in love (with someone you shouldn't've)</td>
    </tr>
    <tr>
      <th scope="row">The Clash</th>
      <td>1976</td>
      <td>6</td>
      <td>London Calling</td>
    </tr>
    <tr>
      <th scope="row">The Damned</th>
      <td>1976</td>
      <td>10</td>
      <td>Smash it up</td>
    </tr>
    <tr>
      <th scope="row">Sex Pistols</th>
      <td>1975</td>
      <td>1</td>
      <td>Anarchy in the UK</td>
    </tr>
    <tr>
      <th scope="row">Sham 69</th>
      <td>1976</td>
      <td>13</td>
      <td>If the kids are united</td>
    </tr>
    <tr>
      <th scope="row">Siouxsie and the Banshees</th>
      <td>1976</td>
      <td>11</td>
      <td>Hong Kong Garden</td>
    </tr>
    <tr>
      <th scope="row">Stiff Little Fingers</th>
      <td>1977</td>
      <td>10</td>
      <td>Suspect Device</td>
    </tr>
    <tr>
      <th scope="row">The Stranglers</th>
      <td>1974</td>
      <td>17</td>
      <td>No More Heroes</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <th scope="row" colspan="2">Total albums</th>
      <td colspan="2">77</td>
    </tr>
  </tfoot>
</table>
```

|Result:||
|:---|:---|
|Before|After|
|![css-tables-before](https://github.com/siriyaoff/MDN-note/blob/master/images/css-tables-before.PNG?raw=true)|![css-tables-after](https://github.com/siriyaoff/MDN-note/blob/master/images/css-tables-after.PNG?raw=true)|

- `th, td`에 padding을 줘서 셀 넓힐 수 있음
- `:nth-child(n)`는 혼자 쓰이면 부모 노드에서 n번째 자식,<br>`td:nth-child(n)`과 같이 쓰이면 부모노드에서 td인 자식 중 n번째를 선택
- `vertical-align` property를 사용해서 box에서 text의 세로 위치를 결정할 수 있음(`top`, `middle`, `bottom`)

## Debuging CSS
### How to access browser DevTools
firefox devtools는 grid layouts, flexbox, shapes를 edit할 수 있다

### The DOM versus view source
DOM에는 HTML의 오류들이 수정되어서 렌더링됨(browser에 의해)
(+ browser가 모든 HTML을 normalize하고, DOM에는 JavaScript에 의한 변경점도 모두 적용됨)

View Source는 DevTools에 의해 지원되는, 서버에 저장된 HTML source code를 보여주는 것임  
(+ HTML tree도 같이 보여줌, display되지 않은 elements까지 볼 수 있음)

### Inspecting the applied CSS
Rules view에서 element에 적용된 모든 CSS를 볼 수 있음(inherited 포함)

shorthand properties를 longhand properties로 확장할 수 있음

toggle하여 rule을 적용하거나 제외할 수 있음

### Editing values
CSS를 볼 뿐만 아니라 propertie values를 수정 가능함

### Adding a new property
closing curly brace를 클릭하면 new declaration 삽입 가능

### Understanding the box model
Layout view에서는 element의 크기를 자세히 볼 수 있음

`box-sizing`에 따라 box의 크기를 계산해서 표시해줌(`box-sizing`, `display` 등의 box model properties를 포함해서)

### Solving specificity issues
more specific selector가 존재하는 경우 css를 수정해도 적용이 안됨  
DevTools에서 하나의 element에 대해 어떤 value가 적용되고 있는지 알 수 있음(specificity 순으로 나열됨)

### Debugging problems in CSS
Few steps to solve problems:
1. Take a step back from the problem
2. Do you have valid HTML and CSS?
	- use validator
3. Is the property and value supported by the browser you are testing in?
	- DevTools will generally highlight unsupported properties and values in some way.
4. Is something else overriding your CSS?
	- use DevTools to find overriding rules.
5. Make a reduced test case of the problem
	reduced test case : code example that demonstrates the problem in the simplest possible way, with unrelated surrounding content and styling removed.
	
	To create a reduced test case:
	1. If your markup is dynamically generated, make a static version of the output that shows the problem.
	2. 이슈와 관련 없는 JavaScript 제거
	3. 이슈와 관련 없는 HTML 제거(main element까지도)
	4. 이슈와 관련 없는 CSS 제거
	
	reduced test case를 만들면 문제의 원인이나 트리거 등을 발견할 수 있음 + 도움을 요청할 때 다른 사람이 문제를 더 쉽게 파악 가능

## Organizing your CSS
### Tips to keep your CSS tidy
#### Does your project have a coding style guide?
#### Keep it consistent
#### Formatting readable CSS
#### Comment your CSS
- 코드에서 사용하지 않는 문자열을 comment의 index로 사용 가능(`||`와 같이)

```css
/* || General styles */

...

/* || Utilities */

...

/* || Sitewide */

...
```

#### Create logical sections in your stylesheet
위 코드처럼 logical section을 만들어놓으면 코드의 가독성이 증가함

`/* || General styles */`
- elements들에 대한 default styling

`/* || UTILITIES */`
- nobullets같은 utility classes

`/* || Sitewide */`
- main-nav, logo같은 basic page layout, header, navigation styling

`/* || Store pages */`
- 나머지 css

=> 바꿔야 하는 부분을 쉽게 찾을 수 있음

#### Avoid overly-specific selectors
#### Break large stylesheets into multiple smaller ones
you can link to multiple stylesheets from one page.

### Other tools that can help
#### CSS methodologies
이미 만들어진 methodologies를 사용하면 협업할 때 편함

**OOCSS**  
Object Oriented CSS  
basic idea of OOCSS : **to separate your CSS into reusable objects**  
`media`와 같이 하나의 class를 정의해 common CSS를 적음  
=> 이후 다른 클래스들을 선언해 specific한 CSS 적음  
=> `media` 클래스는 모든 component에 들어가는 클래스

**BEM**  
Block Element Modifier  
Block : stand-alone entity e.g. button, menu, logo  
Element : e.g. list item, title that is tied to the block it is in  
Modifier : flag on a block or element that changes the styling or behavior  
extensive use of dashes and underscores in the CSS classes가 특징임

#### Example
```html
<form class="form form--theme-xmas form--simple">
  <input class="form__input" type="text" />
  <input
    class="form__submit form__submit--disabled"
    type="submit" />
</form>
```  

**Other common systems**  
다른 것들도 많음(SMACSS, ITCSS, ACSS 등등)  
이런 system을 쓰면 좋은 점은 가이드가 많아 쉽게 작성 가능하다는 것이고,  
나쁜 점은 처음 볼 때 너무 복잡하게 보인다는 것임(특히 작은 프로젝트에서)

#### Build systems for CSS
Pre-processor runs over your raw files and turns them into a stylesheet  
Post-processor takes your finished stylesheet and optimizes it

pre and post-processing을 지원해야 사용 가능(대부분의 IDE 지원)  
Sass : the most popular pre-processor  
변수 선언, component stylesheets 때문에 많이 쓰임

**Defining variables**  
지금은 CSS에도 custom properties를 이용해서 변수를 선언 가능  
Sass에서는 `$`를 prefix로 붙여서 변수 선언 가능  

#### Example
```css
$base-color: #c6538c;

.alert {
  border: 1px solid $base-color;
}
```

**Compiling component stylesheets**  
`foundation/_code.scss`, `foundation/_lists.scss`, `foundation/_footer.scss`, `foundation/_links.scss`가 `foundation` 디렉토리 안에 있다고 가정하면  
```css
// foundation/_index.sass
@use 'code'
@use 'lists'
@use 'footer'
@use 'links'
```  
처럼 index를 만들고  
```css
// style.sass
@use 'foundation'
```  
처럼 `foundation` 디렉토리와 동일한 경로에서는 `foundation` 디렉토리 전체를 링크 가능

#### Post-processing for optimization
stylesheets의 크기를 줄이는 등의 최적화를 해줌

## Assessment06-Fundamental-CSS-comprehension
- `line-height` property : 줄의 높이 설정(`line-height`가 `font-size`보다 클 경우 글자는 자동으로 vertically center로 배치됨, `vertical-align`은 inline element에 대해서만 사용 가능)

p에서 line height가 font size보다 클 때 vertical position 조정은 어떻게 하지?  
=> 할 필요가 없음(line-height, padding으로 조정 가능)

## Assessment07-Creating-fancy-letterheaded-paper
- background를 넣을 때 fallback을 위에 넣는 이유 : 같은 property에 대해서는 cascading rule이 적용되어서 가장 아래에 적힌 것이 적용되기 때문
- `filter: drop-shadow(3px 3px 3px black);`를 이용<br>`filter`를 지원하지 않는 브라우저에 대해 `border-radius: 64px; box-shadow: 3px 3px 3px black;`를 사용해서 비슷하게 만들 수 있음
	- 하지만 박스를 원 형태로 만들어서 그림자를 넣는 것이기 때문에 자연스럽지 않음

## Assessment08-A-cool-looking-box
- `background`는 모든 background를 바꿔버리고, `background-color`, `background-image`는 기존 background에 각각의 value를 추가함<br>(background, background-image, background-color 순서로 layer가 정의되어 있는 듯, 앞이 가장 위의 layer)
- default font size : `16px`
- `<p>`의 경우 `margin: auto;`를 넣으면 자동으로 center로 위치가 맞춰짐
- `box-shadow`는 `inset`이 적용된 value를 먼저 적는게 더 가독성이 좋음
- `line-height`의 기본 단위는 `em`임

## Advanced styling effects
### Box shadows
`box-shadow`는 IE9+, Edge등에서도 지원됨  
older IE versions에서는 지원안되기 때문에 shadow 없이도 legible한지 테스트해야함

#### A simple box shadow
`box-shadow: [inset] [horizontal offset] [vertical offset] [blur radius] [spread radius] [base color];`
- offset은 negative value 가능
- `inset`은 생략 가능(keyword가 적혀있을 때만 inset이 적용됨)

#### Multiple box shadows
- comma로 separate해서 여러 개의 shadow를 넣을 수 있음

#### Other box shadow features
- `inset`을 적용하면 박스의 안쪽에 그림자 넣을 수 있음
	- inset을 적용하지 않고 offset에 음수 넣은 shadow는 box 아래의 layer에 있어서 box가 덮어버림
	- `text-shadow`에는 `inset` keyword가 없음
- pseudo-class와 함께 사용하면 클릭시 효과를 넣을 수 있음(`:focus`, `:hover`, `:active` 등)
- `[blur radius]` 뒤에 `[spread radius]`를 넣을 수 있음, 넣은 만큼 shadow를 더 넓혀줌(shadow의 width, height에 spread radius만큼 더함)

### Filters
`filter` property의 value
- `drop-shadow()`
- `blur([blur radius])`
- `grayscale(<percentage>)`
- `contrast(<percentage>)` : 퍼센트 만큼 대조
- `invert(<percentage>)` : 퍼센트 만큼 반전
- `huerotate([angle])` : hue값을 `[angle]`만큼 수정함

※ filter의 option 중 몇 개는 css features와 비슷한 효과를 줌  
e.g.  
`drop-shadow`는 `box-shadow`, `text-shadow`와 비슷함  
그러나 border가 dashed인 `<p>`가 있으면 `drop-shadow`는 그림자가 점선으로 나타나지만,  
`box-shadow`는 그림자가 실선으로 나타남

### Blend modes
blend mode는 `background-blend-mode`, `mix-blend-mode` 두 가지로 지원됨  
※ blend mode는 최신 기능이라 edge에서는 지원 안됨

#### background-blend-mode
`background-blend-mode: multiply;`가 적용되면 background가 여러 개 있을 때 최종 결과는 포토샵으로 섞은 것처럼 나옴  
아래 그림의 왼쪽이 이미지와 초록색 배경을 적용한 것, 오른쪽이 blend mode 적용시킨 것  
![css-background-blend-mode](https://github.com/siriyaoff/MDN-note/blob/master/images/css-background-blend-mode.PNG?raw=true)

#### mix-blend-mode
`background-blend-mode`와 같은 효과지만, `<div>`와 같은 elements가 blend됨  
blend mode가 적용된 element는 다른 element와 겹쳐지면 blend됨

### CSS shapes
- `shape-outside`로 이미지가 실제론 직사각형이어도 한글에서 글에 둘러싸이는 것처럼 만들 수 있음
- floated elements에 대해서만 적용 가능함

#### Example
CSS:  
```css
img {
  float: left;
  shape-outside: circle(50%);
}
```

HTML:  
```html
<div class="wrapper">
  <img src="round-balloon.png" alt="balloon">
  <p>One November night in the year 1782, so the story runs, two brothers sat over their winter fire in the little French town of Annonay, watching the grey smoke-wreaths from the hearth curl up the wide chimney. Their names were Stephen and Joseph Montgolfier, they were papermakers by trade, and were noted as possessing thoughtful minds and a deep interest in all scientific knowledge and new discovery. Before that night—a memorable night, as it was to prove—hundreds of millions of people had watched the rising smoke-wreaths of their fires without drawing any special inspiration from the fact.</p>
</div>
```

|Result:|
|:---|
|![css-shape-outside](https://github.com/siriyaoff/MDN-note/blob/master/images/css-shape-outside.PNG?raw=true)|

- `circle()`은 shape를 만드는 함수 중 하나임(<a href="https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Shapes/Overview_of_CSS_Shapes" target="_blank">필요하면 더 공부하기</a>)
- `circle(<percentage>)`은 이미지의 중심에서부터 `<percentage>*이미지의 width`만큼 원을 그려서 shape으로 활용하는 듯

### -webkit-background-clip: text
#### Example
CSS:  
```css
h2 {
  width: 250px;
  height: 250px;
  text-align: center;
  line-height: 250px;
  font-size: 75px;
  display: inline-block;
  background: url(colorful-heart.png) no-repeat center;
}

.text-clip {
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
```

HTML:  
```html
<h2>WOW</h2>

<h2 class="text-clip">WOW</h2>  
```

|Result:|
|:---|
|![css-webkit-background-clip](https://github.com/siriyaoff/MDN-note/blob/master/images/css-webkit-background-clip.PNG?raw=true)|

- Non-Webkit/Chrome-based browsers도 `-webkit-` vendor prefix를 붙여서 properties를 사용해야 함
	- 너무 많이 쓰여서 표준이 아니지만 다른 브라우저도 이 기능을 구현한 결과임
	- danger of using non-standard and/or prefixed CSS features


# Styling text
## Fundamental text and font styling
### What is involved in styling text in CSS?
The CSS properties used to style text generally fall into two categories
- Font styles : properties that affect the font(font 종류, 크기, bold, italic 등)
- Text layout styles : properties that affect layout features(spacing, text alignment 등)

**Note**: 하나의 element 안에 있는 text들은 one single entity로 CSS의 영향을 받음  subsection을 선택하기 위해선 pseudo-element(`::first-letter`, `::selection` 등)을 사용해야 함

### Fonts
#### Color
Use `color` property

#### Font families
Use `font-family`  
글꼴이 지원되지 않으면 default font를 사용함

**Web safe fonts**  
generally available한 font들

|Name|Generic type|Notes|
|:---|:---|:---|
|Arial|sans-serif|*Helvetica*이 alternative로 사용하기 좋음(둘의 모양이 비슷함, *Arial*이 더 범용성있음)|
|Courier New|monospace|preferred alternative : *Courier*(더 오래된 버전)|
|Georgia|serif||
|Times New Roman|serif|preferred alternative : *Times*(더 오래된 버전)|
|Trebuchet MS|sans-serif|mobile OSes에서는 widely available하지 않음|
|Verdana|sans-serif||

**Default fonts**  
CSS defines five generic names for fonts : `serif`, `sans-serif`, `monospace`, `cursive`, `fantasy`  
이 글꼴들은 브라우저, OS에 따라서 실제 사용되는 font face가 다를 수 있음!  
특히 `cursive`와 `fantasy`는 사용할 때 주의해야함(특이한 글꼴이라서 많이 다를 수 있음)

|Term|Definition|Example|
|:---|:---|:---|
|`serif`|Fonts that have serifs(the flourishes and other small details you see at the ends of the strokes in some typefaces)|<span style="font-family:serif;">My big red elephant</span>|
|`sans-serif`|Fonts that don't have serifs|<span style="font-family:sans-serif;">My big red elephant</span>|
|`monospace`|Fonts where every character has the same width, typically used in code listings|<span style="font-family:monospace;">My big red elephant</span>|
|`cursive`|Fonts that are intended to emulate handwriting, with flowing, connected strokes|<span style="font-family:cursive;">My big red elephant</span>|
|`fantasy`|Fonts that are intended to be decorative|<span style="font-family:fantasy;">My big red elephant</span>|

**Font stacks**  
Supply a font stack so that the browser has multiple fonts it can choose from.  
e.g. `font-family: "Trebuchet MS", Verdana, sans-serif;`  
브라우저가 font를 지원하지 않는 것을 대비해서 마지막에 suitable generic font를 추가해놓는게 좋음  

**Note**: font name이 한 단어보다 많을 경우 double quotes로 감싸야 함

#### Font size
Use `font-size`  
`font-size`는 `px`, `em`, `rem` 등 많은 unit들을 사용 가능  
기본적으로 parent element로부터 inherit됨(16px가 root element의 default size임)  
`em`은 parent element의 크기가 기준이기 때문에 container elements에 대해서는 `font-size` 설정을 피하는게 나음

#### Font style, font weight, text transform, and text decoration
Four common properties to alter the visual weight/emphasis of text:
- `font-style` : Use to turn *italic* text on and off<br>possible values:
	- `normal`
	- `italic` : set the text to use the *italic version* of the font<br>(if not available, it will simulate italics with oblique instead)
	- `oblique` : set the text to use a simulated version of an italic font(*slanting* the normal version)
- `font-weight` : Set boldness of the text<br>values available:
	- `normal`, `bold`
	- `lighter`, `bolder` : calculate with parent element's boldness
	- `100` - `900` : numeric boldness
- `text-transform` : Set font to be transformed<br>values include:
	- `none`
	- `uppercase`, `lowercase`
	- `capitalize`
	- `full-width` : Transform all glyphs to be written inside a fixed-width square(similar to monospace font)
- `text-decoration` : Set text decorations(underline ...)<br>available values:
	- `none`
	- `underline`
	- `overline` : <span style="text-decoration:overline;">Gives the text an overline</span>
	- `line-through` : ~~취소선~~
	
	multiple value 입력 가능  
	`text-decoration`은 `text-decoration-line`, `-style`, `-color`의 shorthand임

#### Text drop shadows
Use `text-shadow`  
*CSS building blocks*에서 설명한대로 `text-shadow: [x-offset] [y-offset] [blur radius] [color];`의 포맷을 가짐(`inset`, `spread radius`는 없음)  

**Multiple shadows**  
shadow 여러 개 가능

### Text layout
#### Text alignment
Use `text-align`
- `left`
- `right`
- `center`
- `justify` : Make the text spread out<br>이걸 사용할 때는 긴 단어는 `-`을 이용해서 나눠야 하는 것을 고려해야함

#### Line height
Use `line-height` to set the height of each line of text  
숫자만 넣으면 font size에 곱해져서 계산됨  
`1.5`-`2`가 보통

#### Letter and word spacing
Use `letter-spacing` and `word-spacing` to set the spacing between letters and words  
e.g. `letter-spacing: 4px;`

#### Other properties worth looking at
<a href="https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Fundamentals#other_properties_worth_looking_at" target="_blank">다른 properties로 많음</a>

### Font shorthand
`font`를 shorthand로 사용할 때 `font-style`, `font-variant`, `font-weight`, `font-stretch`, `font-size`, `line-height`, `font-family` 순서로 작성되어야 함  
`font-size`, `font-family` 두 개만 required임  
`font-size`, `line-height` 사이에는 `/`를 사용해야함(둘 다 length and size units가 들어가기 때문)  
e.g. `font: italic normal bold normal 3em/1.5 Helvetica, Arial, sans-serif;`

## Styling lists
### A simple list example
Styling defaults:
- `<ul>`, `<ol>` elements의 top, bottom `margin` : `1em(16px)`, `padding-left` : `40px`
- `<li>`의 spacing은 default가 없음
- `<dl>`의 top, bottom `margin` : `1em(16px)`
- `<dd>`의 `margin-left` : `40px`
- `<p>`의 top, bottom `margin` : `1em(16px)`

### Handling list spacing
list가 surrounding elements와 같은 horizontal, vertical spacing을 가지도록 여백을 조절해야함  
`line-height`, `font-size`를 조절해서 가능함

### List-specific styles
general spacing techuiques for lists(`<ul>`, `<ol>`)
- `list-style-type` : Set the type of bullets
- `list-style-position` : Set whether the bullets appear inside or outside the list items
- `list-style-image` : Allow you to use a custom image for the bullet

#### Bullet styles
Use `list-style-type`  
values available:
- for `<ol>` : `upper-roman`, `lower-roman`, `decimal`, `upper-alpha`, `lower-alpha`, `none`
- for `<ul>` : `<string>`(e.g. `'-'`), `disc`, `circle`, `square`, `none`

#### Bullet position
Use `list-style-position`  
values available:
- `outside` : default, bullets가 list item의 바깥에 배치됨
- `inside` : bullets가 list item의 안에 배치됨

#### Using a custom bullet image
Use `list-style-image`  
Use `url()` to link the image  
근데 이 property는 bullet의 position, size 등을 조절하기 어려움  
오히려 `<li>`에 `background`를 이용하는게 더 편함

#### Example
CSS:  
```css
ul {
  padding-left: 2rem;
  list-style-type: none;
}

ul li {
  padding-left: 2rem;
  background-image: url(star.svg);
  background-position: 0 0;
  background-size: 1.6rem 1.6rem;
  background-repeat: no-repeat;
}
```
- `<ul>`의 `padding-left` `40px`를 `ul`, `ul li`에 `20px`씩 나눔<br>∵ `<ul>`의 list item이 `<ol>`, `<dl>`과 같은 여백을 가지면서 background로 listmarker를 넣기 위함(`ul li`에 `padding-left`가 없으면 background가 `<li>`의 본문과 겹쳐버림
- `list-style-type`을 `none`으로 설정<br>∵ background로 넣기 위함

#### list-style shorthand
`list-style`에 `list-style-type`, `list-style-image`, `list-style-position`을 한꺼번에 쓸 수 있음  
default : `disc`, `none`, `outside`  
순서는 상관없음  
만약 `type`, `image`가 둘 다 명시된 경우 type이 fallback으로 사용됨

#### Example
```css
ul {
  list-style-type: square;
  list-style-image: url(example.png);
  list-style-position: inside;
}
```

is equal to 

```css
ul {
  list-style: square url(example.png) inside;
}
```

### Conrolling list counting
ordered list의 list marker index를 바꾸는 방법

#### start
`start` attribute로 시작지점 설정  
e.g. `<ol start="4">`

#### reversed
`reversed` attribute로 증가할지 감소할지 설정  
e.g. `<ol start="4" reversed>` => 4, 3, 2, 1, 0, -1, ... 순으로 index

#### value
`value` attribute로 list marker를 직접 지정  
다른 attributes와 다르게 `<li>`에 넣어야 함  
non-number `list-style-type`을 사용하고 있으면 적용되지 않음  
value를 지정하면 다음 `<li>`도 영향을 받음  
e.g. `<li value="2">`로 설정해놓으면 다음 li는 marker가 3이 됨

## Styling links
### Let's look at some link
#### Link states
different pseudo-classes:
- `:link` : a link which has a destination
- `:visited`
- `:hover`
- `:focus` : a link when it has been focused(e.g. tab같은 걸로 focus받았을 때)
- `:active` : a link when it is being activated(e.g. clicked on)

#### Default styles
- links are underlined
- Unvisited links are blue
- Visited links are purple
- Hovering a link makes the mouse pointer change to a little hand icon
- Focused links have an outline around them(tab키로 페이지의 링크들을 focus할 수 있음)
- Active links are red

※ `#`을 dummy link로 사용 가능  
e.g. `<a href="#">links</a>`

이 default styles는 1990년대 초기 브라우저들과 거의 동일함(혼동을 유발하지 않기 위해)  
최소한 다음과 같은 양식은 있어야 함
- Use underlining or highlight for links
- Make them react in some way when hovered/focused, and in a slightly different way when activated

`cursor` property를 사용해서 마우스 커서 조절 가능

#### Styling some links
```css
a {
}

a:link {
}

a:visited {
}

a:focus {
}

a:hover {
}

a:active {
}
```
위의 순서(LVFHA)대로 ruleset을 정의하는게 좋음(activated면 hover이기도 하기 때문)  

※ underlining은 `border-bottom`, `text-decoration`을 이용해서 넣을 수 있는데,<br>`border-bottom`이 더 밑쪽에 줄이 그어짐, y, g같은 글자의 꼬리가 줄에 안닿여서 더 좋음  
`border-bottom: 1px solid;`같이 색을 지정하지 않으면 `color`과 같은 색으로 설정됨

### Including icons on links
```css
a[href*="http"] {
  background: url('https://mdn.mozillademos.org/files/12982/external-link-52.png') no-repeat 100% 0;
  background-size: 16px 16px;
  padding-right: 19px;
}
```
- `background` shorthand로 img 집어넣음
- icon이 글자보다 더 커서 잘릴 경우를 대비해서 `background-size`를 이용해서 이미지를 resize해줌<br>(IE 9 이후의 버전에서만 지원됨, 이전의 브라우저들에 대해서는 resizing한 이미지를 참조해줘야함)
- `padding-right`를 넣어서 icon이 들어갈 공간 확보
- external link는 `http`가 링크에 포함되어있음 => `a[href*="http"]` selector 이용<br>내부 링크는 relative link를 이용하면 됨

### Styling links as buttons
`<li>`에 `display: inline;`을 적용하여 navigation bar를 구현할 수 있음

#### Example
CSS:  
```css
body,html {
  margin: 0;
  font-family: sans-serif;
}

ul {
  padding: 0;
  width: 100%;
}

li {
  display: inline;
}

a {
  outline: none;
  text-decoration: none;
  display: inline-block;
  width: 19.5%;
  margin-right: 0.625%;
  text-align: center;
  line-height: 3;
  color: black;
}

li:last-child a {
  margin-right: 0;
}

a:link, a:visited, a:focus {
  background: yellow;
}

a:hover {
  background: orange;
}

a:active {
  background: red;
  color: white;
}
```

HTML:  
```html
<ul>
  <li><a href="#">Home</a></li><li><a href="#">Pizza</a></li><li><a href="#">Music</a></li><li><a href="#">Wombats</a></li><li><a href="#">Finland</a></li>
</ul>
```
- navigation bar 이외에 `<ul>` 등의 다른 element에 의한 padding, margin을 다 없앰
- HTML에서 모든 `<li>`를 같은 줄에 적음<br>∵ inline elements가 다른 줄에 적히면 사이에 space가 생길 수 있음
- `<a>`에 `display: inline-block;`을 적용해서 inline element지만 sizing이 가능하도록 만듦
- 마지막 `<a>`의 margin-right는 여백이 되기 때문에 `li:last-child a`를 이용해서 없애줌
- `<a>` 대신 `<li>`를 수정해서 nav bar를 만들 수도 있음
- `outline: none;`은 링크가 탭으로 active될 경우 생기는 테두리를 없애줌

## Web fonts
### Font families recap
web safe font를 가지는 font stack을 사용하면 각 font마다 test해야하기 때문에 overhead 발생

### Web fonts
Web fonts를 사용하면 download해야 하는 font files를 지정할 수 있음  
CSS의 가장 윗부분에 `@font-face` block을 정의해야 `@font-face`의 font family를 사용 가능  


#### Example
CSS:  
```css
@font-face {
  font-family: "myFont";
  src: url("myFont.woff2");
}
```

HTML:  
```html
html {
  font-family: "myFont", "Bitstream Vera Serif", serif;
}
```

- WOFF/WOFF2(Web Open Font Format 1/2)은 웬만한 브라우저들이 다 지원함
- WOFF2는 TTF, OTF를 둘 다 지원함
	- TTF(True Type Font) : 일반적인 형식
	- OTF(Open Type Font) : 비교적 최근에 나옴
- font files를 나열한 순서도 중요함(위에서부터 확인함 => 첫 번째가 가장 범용성이 높은 format이어야 함)
- legacy browser를 사용하는 경우 EOT, TTF, SVG webfonts를 준비해야 함

### Active learning: A web font example
Three types of sites to obtain fonts:
- Free font distributor : e.g. Font Squirrel
- Paid font distributor : e.g. fonts.com
- Online font service : e.g. google fonts

#### Generating the required code
Font squirrel의 webfont generator에 font들을 올리고 legacy browser를 지원해야 하는 경우 SVG, EOT, TTF도 선택하고 download kit  
font file의 크기가 큰 경우 ttf를 woff2, svg 등으로 바꿔야 함

#### Implementing the code in your demo
1. 다운받은 webfonts kit을 웹페이지와 같은 경로에 저장(압축 풀고 `fonts`와 같이 이름 바꿈)
2. `stylesheet.css`의 내용을 내 css 파일의 가장 위에 넣음
3. `@font-face`에서 url 수정
4. `@font-face`에 정의된 `font-family`를 사용 가능

### Using an online font service
How to use google fonts:
1. font들 찾아서 맨 밑에 XOR버튼 누름
2. 다 선택한 다음 HTML code를 내 page header에 붙여넣기
3. 밑에 CSS 코드처럼 font 사용 가능

### @font-face in more detail
```css
@font-face {
  font-family: 'zantrokeregular';
  src: url('zantroke-webfont.woff2') format('woff2'),
       url('zantroke-webfont.woff') format('woff');
  font-weight: normal;
  font-style: normal;
}
```
- `font-family` : specifies font name
- `src` : specifies paths to the font files to be imported, `format('woff2')`는 optional
- `font-weight`/`font-style` : specifies boldness, style(italic ...)<br>같은 font를 boldness 별로 여러 개 import하고 있다면 `font-weight`를 적어야 boldness별로 적용 가능

### Variable fonts
Variable fonts allow many different variations of a typeface(weight, style ...) into a single file(OTF와 비슷)

## Assessment09-Typesetting-a-community-school-homepage
CSS:  
```css
/* General setup */
@import url('https://fonts.googleapis.com/css2?family=Krona+One&family=Open+Sans:ital,wght@0,300;0,600;1,300&display=swap');

* {
  box-sizing: border-box;
}

body {
  margin: 0 auto;
  min-width: 1000px;
  max-width: 1400px;
}

/* Layout */

section {
  float: left;
  width: 50%;
}

aside {
  float: left;
  width: 30%;
}

nav {
  float: left;
  width: 20%;
}

footer {
  clear: both;
}

header, section, aside, nav, footer {
  padding: 20px;
}

/* header and footer */

header, footer {
  border-top: 5px solid #a66;
  border-bottom: 5px solid #a66;
}

/* WRITE YOUR CODE BELOW HERE */

html {
  font-size: 10px;
}

body {
  font-family: 'Open Sans', sans-serif;
  line-height: 1.6em;
  letter-spacing: 1px;
  word-spacing: 2px;
}

h1, h2 {
  font-family: 'Krona One', sans-serif;
  letter-spacing: 3px;
}

h1 {
  font-size: 2em;
  text-align: center;
}

h2 {
  font-size: 1.5em;
}

section h2+p {
  text-indent: 20px;
}

a:link, a:visited, a:focus, a:hover {
  color: #a66;
}

a:hover, a:focus {
  text-decoration: none;
}

a {
  outline: none;
}

a:active {
  outline: 1px solid #a66;
}

a[href*='http'] {
  padding-right: 15px;
  background: url("https://mdn.mozillademos.org/files/12982/external-link-52.png") no-repeat 100%;
  background-size: 10px 10px;
}

li {
  line-height: 1.6em;
}

ul, ol {
  margin: 16px 0px;
}

ul {
  list-style-type: circle;
}

ol {
  list-style-type: lower-alpha;
}

nav ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

nav ul li {
  padding: 10px 0;
}

nav li a {
  display: inline-block;
  border: 1px solid #b77;
  width: 100%;
  height: 5rem;
  line-height: 5rem;
  font-size: 1.2rem;
  text-align: center;
  text-decoration: none;
}

nav li a:hover {
  background-color: #fba;
}
```

HTML:  
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>St Huxley's Community College</title>
    <link href="style.css" type="text/css" rel="stylesheet">
  </head>
  <body>

  <header>
    <h1>St Huxley's Community College</h1>
  </header>

  <section>
      <h2>Brave new world</h2>

      <p>It's a brave new world out there. Our children are being put in increasing more competitive situations, both during recreation, and as they start to move into the adult world of <a href="https://en.wikipedia.org/wiki/Examination">examinations</a>, <a href="https://en.wikipedia.org/wiki/Jobs">jobs</a>, <a href="https://en.wikipedia.org/wiki/Career">careers</a>, and other life choices. Having the wrong mindset, becoming <a href="https://en.wikipedia.org/wiki/Emotion">too emotional</a>, or making the wrong choices can contribute to them experiencing difficulty in taking their rightful place in today's ideal society.</p>

      <p>As concerned parents, guardians or carers, you will no doubt want to give your children the best possible start in life — and you've come to the right place.</p>

      <h2>The best start in life</h2>

      <p>At St. Huxley's, we pride ourselves in not only giving our students a top quality education, but also giving them the societal and emotional intelligence they need to win big in the coming utopia. We not only excel at subjects such as genetics, data mining, and chemistry, but we also include compulsory lessons in:</p>

      <ul>
        <li>Emotional control</li>
        <li>Judgement</li>
        <li>Assertion</li>
        <li>Focus and resolve</li>
      </ul>

      <p>If you are interested, then you next steps will likely be to:</p>
      
      <ol>
        <li><a href="#">Call us</a> for more information</li>
        <li><a href="#">Ask for a brochure</a>, which includes signup form</li>
        <li><a href="#">Book a visit</a>!</li>
      </ol>
  </section>

  <aside>

    <h2>Top course choices</h2>

    <ul>
      <li><a href="#">Genetic engineering</a></li>
      <li><a href="#">Genetic mutation</a></li>
      <li><a href="#">Organic Chemistry</a></li>
      <li><a href="#">Pharmaceuticals</a></li>
      <li><a href="#">Biochemistry with behaviour</a></li>
      <li><a href="#">Pure biochemistry</a></li>
      <li><a href="#">Data mining</a></li>
      <li><a href="#">Computer security</a></li>
      <li><a href="#">Bioinformatics</a></li>
      <li><a href="#">Cybernetics</a></li>
    </ul>

    <p><a href="#">See more</a></p>

  </aside>

  <nav>

    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">Finding us</a></li>
      <li><a href="#">Courses</a></li>
      <li><a href="#">Staff</a></li>
      <li><a href="#">Media</a></li>
      <li><a href="#">Prospectus</a></li>
    </ul>

  </nav>

  <footer>

    <p>&copy; 2016 St Huxley's Community College</p>

  </footer>

  </body>
</html>
```

- url의 parameter에 quotes를 넣는건 optional(안쓰든, single, double을 쓰든)
- background-position은 horizontal, vertical 순임<br>`padding`, `margin`은 vertical, horizontal 순!
- `box-sizing` : `content-box`(standard), `border-box`(alternative)<br>`display` : `inline-block`, ...
- `display: inline-block;`을 적용하고 width, height를 선언할 경우, 모두 border까지 포함한 크기로 계산됨(`box-sizing: border-box;`와 동일)
	- 이 과제에서는 inline-block 안에 `height`, `line-height`를 같이 썼는데, 사실 `height`는 높이를 꼭 `5rem`으로 맞춰야 할 필요가 없으면 사용하지 않아도 됨


# CSS layout
## Introduction to CSS layout
The page layout techniques in this module:
- Normal flow
- `display` property
	- `block`, `inline`, `inline-block`와 같은 value들은 normal flow에서 element의 layout을 결정
	- `grid`, `flexbox`와 같은 value들은 entire layout method를 바꿈(`grid`나 `flexbox`가 적용된 element 안의 elements들의 layout을 결정)
- Flexbox
- Grid
- Floats
	- `float: left;`와 같은 속성을 적용시키면 block level elements가 다른 element의 왼쪽에 떠있게(wrapped)할 수 있음
- Positioning
	- `position` property를 이용
	- `static`, `fixed`, `absolute` 등의 value를 가짐
	- box의 위치를 다른 box 안에서 지정하게 해줌
- Table layout
	- `display: table;`와 같은 property를 통해 적용시킬 수 있음
	- non-table elements를 HTML table과 같이 styling하기 위해 만듦
- Multiple-column layout
	- block content를 여러 column으로 나타낼 수 있게 해줌

No technique is designed to be used in isolation.

### Normal flow
Normal flow : browser가 default로 사용하는 layout
HTML code의 순서대로 나타남  
- block elements : 이전 순서의 element 아래에 다른 줄로 나타나는 elements
- inline elements : 이전 순서의 element 옆에 같은 줄로 나타나는 elements

=> block direction : block element가 배치되는 방향(writing mode에 따라 결정됨)

The methods that can change how elements are laid out in CSS:
- `display` property
- Floats
- `position` property
- Table layout
- Multi-column layout

### The display property
page layout은 `display` property를 적용하는 것으로부터 시작됨  
예를 들어 `<p>`의 경우 `display: block;`가 적용되어있기 때문에 block element로 layout되고, `<a>`의 경우 `display: inline;`이 적용되어있기 때문에 inline element로 layout됨

이러한 default display behavior를 바꿀 수도 있음(`display`에 값을 직접 지정함으로써)  
=> HTML elements의 semantic meaning을 직접 지정할 수 있음

`display: flex;`, `display: grid;`와 같은, `display` property를 선언하고 추가적으로 layout을 수정할 수 있는 layout methods도 존재

### Flexbox
Flexbox(Flexible Box) : 1차원으로 elements를 편하게 layout하기 위해 만들어짐  
`display: flex;`를 parent element에 적용  
=> parent element를 flexbox, child elements를 flex item으로 layout

#### Example
CSS:  
```css
.wrapper {
  display: flex;
}
```

HTML:  
```html
<div class="wrapper">
  <div class="box1">One</div>
  <div class="box2">Two</div>
  <div class="box3">Three</div>
</div>
```

|Result:|
|:---|
|![css-flexbox-ex1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-flexbox-ex1.PNG?raw=true)|

- flexbox의 `flex-direction` property에 `row`가 initial value로 들어가있기 때문에 위와 같이 row로 layout됨
- flexbox의 `align-items` property에 `stretch`가 initial value로 들어가있기 때문에 item 중 height가 가장 큰 것에 맞춰짐
	- `flex-direction: row;`이기 때문에 height만 신경쓰면 됨(width는 flex item 각자 값 그대로 들어감)

CSS:  
```css
.wrapper {
    display: flex;
}

.wrapper > div {
    flex: 1;
}
```

HTML:  
```html
<div class="wrapper">
  <div class="box1">One</div>
  <div class="box2">Two</div>
  <div class="box3">Three</div>
</div>
```

|Result:|
|:---|
|![css-flexbox-ex2](https://github.com/siriyaoff/MDN-note/blob/master/images/css-flexbox-ex2.PNG?raw=true)|

- flex items에 적용하는 property도 있음!
- `flex: 1;`을 flex item에 적용하면 공간이 채워지도록 확대/축소할 수 있음
	- 여러 item에 적용하면 적용된 item들끼리 공간이 채워지도록 조절됨

### Grid Layout
Grid : 2차원으로 elements를 layout하기 위해 만들어짐  
`display: grid;`를 parent element에 적용

#### Example
CSS:  
```css
.wrapper {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 100px 100px;
    grid-gap: 10px;
}
```

HTML:  
```html
<div class="wrapper">
    <div class="box1">One</div>
    <div class="box2">Two</div>
    <div class="box3">Three</div>
    <div class="box4">Four</div>
    <div class="box5">Five</div>
    <div class="box6">Six</div>
</div>
```

|Result:|
|:---|
|![css-grid-ex1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-grid-ex1.PNG?raw=true)|

- `grid-template-rows`, `grid-template-columns` properties를 사용해서 행, 열 개수 정의

CSS:  
```css
.wrapper {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 100px 100px;
    grid-gap: 10px;
}

.box1 {
    grid-column: 2 / 4;
    grid-row: 1;
}

.box2 {
    grid-column: 1;
    grid-row: 1 / 3;
}

.box3 {
    grid-row: 2;
    grid-column: 3;
}
```

HTML:  
```html
<div class="wrapper">
    <div class="box1">One</div>
    <div class="box2">Two</div>
    <div class="box3">Three</div>
</div>
```

|Result:|
|:---|
|![css-grid-ex2](https://github.com/siriyaoff/MDN-note/blob/master/images/css-grid-ex2.PNG?raw=true)|

- `grid-column`, `grid-row`를 이용해서 element가 차지할 영역을 지정할 수 있음<br>`start/end`로 지정, 좌표는 1부터 시작

### Floats
하나의 element를 float하면 normal flow에서 제외되고, surrounding content도 같이 float됨  
possible values:
- `left`, `right`
- `none`
- `inherit`

#### Example
CSS:  
```css
.box {
    float: left;
    width: 150px;
    height: 150px;
    margin-right: 30px;
}
```

HTML:  
```html
<h1>Simple float example</h1>

<div class="box">Float</div>

<p> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla luctus aliquam dolor, eu lacinia lorem placerat vulputate. Duis felis orci, pulvinar id metus ut, rutrum luctus orci. Cras porttitor imperdiet nunc, at ultricies tellus laoreet sit amet. Sed auctor cursus massa at porta. Integer ligula ipsum, tristique sit amet orci vel, viverra egestas ligula. Curabitur vehicula tellus neque, ac ornare ex malesuada et. In vitae convallis lacus. Aliquam erat volutpat. Suspendisse ac imperdiet turpis. Aenean finibus sollicitudin eros pharetra congue. Duis ornare egestas augue ut luctus. Proin blandit quam nec lacus varius commodo et a urna. Ut id ornare felis, eget fermentum sapien.</p>

```

|Result:|
|:---|
|![css-float-ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-float-ex.PNG?raw=true)|

### Positioning techniques
Positioning isn't a method for creating your main page layouts, it is more about managing and fine-tuning the position of specific items on the page.  
`position` property를 이용해서 layout patterns를 만들 수 있음  
five types of positioning:
- **Static positioning** : default
	- normal position에 넣음
- **Relative positioning**
	- normal position과 relative하게 position을 지정
	- 다른 elements를 overlap하게 지정 가능
- **Absolute positioning**
	- element를 완전히 normal flow에서 제외시킴(다른 layer에 있는 것처럼)
	- `<html>` element의 모서리를 기준으로 position을 지정
	- 자유로운 위치 조정이 필요하거나 복잡한 layout 효과를 만드는데 유용
- **Fixed positioning**
	- browser viewport를 기준으로 position 지정(=> 페이지가 스크롤되어도 고정)
	- nav 같이 항상 같은 위치에 있는 것 같은 효과를 만들 때 유용
- **Sticky positioning**
	- defined offset(viewport)에 도달하면 `fixed`, 이전까지는 `static`인 positioning method

#### Simple positioning example
공통적으로 아래 코드를 이용  
`positioned` class를 이용해서 `position` property의 value를 하나씩 살펴볼 예정

CSS:  
```css
body {
  width: 500px;
  margin: 0 auto;
}

p {
    background-color: rgb(207,232,220);
    border: 2px solid rgb(79,185,227);
    padding: 10px;
    margin: 10px;
    border-radius: 5px;
}
```

HTML:  
```html
<h1>Positioning</h1>

<p>I am a basic block level element.</p>
<p class="positioned">I am a basic block level element.</p>
<p>I am a basic block level element.</p>
```

|Result:|
|:---|
|![css-position-static](https://github.com/siriyaoff/MDN-note/blob/master/images/css-position-static.PNG?raw=true)|

#### Relative positioning
Relative positioning을 사용하면
- icon과 같은 것을 text label과 맞추기 위해 원래 위치보다 살짝 아래로 이동시킬 수 있음

CSS:  
```css
.positioned {
  position: relative;
  background: rgba(255,84,104,.3);
  border: 2px solid rgb(255,84,104);
  top: 30px;
  left: 30px;
}
```

|Result:|
|:---|
|![css-position-relative](https://github.com/siriyaoff/MDN-note/blob/master/images/css-position-relative.PNG?raw=true)|

- `top`, `left` properties를 이용해서 위치를 지정해줘야 함
- element의 원래 위치가 빈 상태로 유지됨(normal flow에 남아있음)

#### Absolute positioning
containing block의 모서리를 기준으로 위치를 지정함

CSS:  
```css
.positioned {
    position: absolute;
    background: rgba(255,84,104,.3);
    border: 2px solid rgb(255,84,104);
    top: 30px;
    left: 30px;
}
```

|Result:|
|:---|
|![css-position-absolute](https://github.com/siriyaoff/MDN-note/blob/master/images/css-position-absolute.PNG?raw=true)|

- `top`, `left` properties를 이용해서 위치를 지정하는 것은 relative와 비슷하지만, 기준이 다름
	- 이 예시에서는 page의 top, left가 기준
	- 기준을 바꿀 수도 있음
- element의 원래 위치는 유지되지 않음(normal flow에서 제외됨)

#### Fixed positioning
Fixed positioning을 사용하면
- top button과 같은 스크롤해도 유지되는 요소 만들 수 있음

CSS:  
```css
.positioned {
    position: fixed;
    top: 30px;
    left: 30px;
}
```

HTML:  
```html
<h1>Fixed positioning</h1>

<div class="positioned">Fixed</div>

<p>Paragraph 1.</p>
<p>Paragraph 2.</p>
<p>Paragraph 3.</p>
```

|Result:|
|:---|
|![css-position-fixed1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-position-fixed1.PNG?raw=true)|
|![css-position-fixed2](https://github.com/siriyaoff/MDN-note/blob/master/images/css-position-fixed2.PNG?raw=true)|

- absolute와 마찬가지로 document normal flow에서 제외시킴
- viewport에 relative하게 위치를 지정하기 때문에 스크롤되어도 계속 유지됨

#### Sticky positioning
element가 viewport의 offset에 도달하기 전까지는 `static`, 도달해서 걸리면 `sticky`로 바뀜

CSS:  
```css
.positioned {
  position: sticky;
  top: 30px;
  left: 30px;
}
```

|Result:|
|:---|
|![css-position-sticky1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-position-sticky1.PNG?raw=true)|
|![css-position-sticky2](https://github.com/siriyaoff/MDN-note/blob/master/images/css-position-sticky2.PNG?raw=true)|

- offset을 hit하기 전까지는 `static`이기 때문에 normal flow에 남아있음(`fixed`로 바뀐 후에도)

### Table layout
CSS가 표준화되기 이전에는 page 자체를 table로 만들었음  
=> inflexible, heavy on markup, difficult to debug, semantically wrong

table에 관한 CSS properties는 table이 아닌 elements에도 적용가능함  
=> described as *using CSS tables*

`display`에 `table`, `table-row`, `table-cell`, `table-caption` 등의 값을 넣어서 구현

#### Example
CSS:  
```css
html {
  font-family: sans-serif;
}

form {
  display: table;
  margin: 0 auto;
}

form div {
  display: table-row;
}

form label, form input {
  display: table-cell;
  margin-bottom: 10px;
}

form label {
  width: 200px;
  padding-right: 5%;
  text-align: right;
}

form input {
  width: 300px;
}

form p {
  display: table-caption;
  caption-side: bottom;
  width: 300px;
  color: #999;
  font-style: italic;
}
```

HTML:  
```html
<form>
  <p>First of all, tell us your name and age.</p>
  <div>
    <label for="fname">First name:</label>
    <input type="text" id="fname">
  </div>
  <div>
    <label for="lname">Last name:</label>
    <input type="text" id="lname">
  </div>
  <div>
    <label for="age">Age:</label>
    <input type="text" id="age">
  </div>
</form>
```

|Result:|
|:---|
|![css-table-ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-table-ex.PNG?raw=true)|

- 표 안에 넣은 것 같이 정렬됨
- `table-caption`의 경우 `caption-side: bottom;`을 이용해서 위치 조정 가능

### Multi-column layout
Multi-column은 `column-count`, `column-width` 등의 properties로 구현 가능
- `column-count` : 열 개수를 지정
- `column-width` : 열 너비를 지정해서 viewport에서 가능한한 많은 열 배치

#### Example
CSS:  
```css
.container {
  column-width: 200px;
}
```

HTML:  
```html
<div class="container">
  <h1>Multi-column layout</h1>
  
  <p>Paragraph 1.</p>
  <p>Paragraph 2.</p>
</div>
```

|Result:|
|:---|
|![css-multi-column-ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-multi-column-ex.PNG?raw=true)|

## Normal Flow
CSS를 적용하지 않았을 때 normal flow가 default로 적용됨

### How are elements laid out by default?
box model : element의 content를 먼저 배치하고, padding, border, margin을 붙임

#### block level element의 경우
content가 parent element의 inline space를 모두 채우고, content를 수용하기 위해 block dimension 방향(block flow direction)으로 확장함  
- block flow direction은 parent의 writing mode에 의해 결정됨(initial: horizontal-tb)<br>=> 기본적으로 vertically laid out됨

#### inline element의 경우
content의 size만큼 공간을 차지함  
- inline element는 width, height를 설정할 수 없음<br>=> 수정하기 위해선 `display: block;` or `display: inline-block;`을 사용해야 함
- 기본적으로 같은 줄에 laid out, overflowing text or elements는 new line으로 내려감

#### Margin collapsing
adjacent elements가 둘 다 margin이 있고, 두 margin이 만난다면, 큰 것 하나만 적용되고 나머지는 사라짐
- `line-height`는 글자가 가운데 배치되기 때문에 margin collapsing이랑 상관없음

## Flexbox
### Why Flexbox?
예전에는 `float`, `position`과 같은게 reliable cross browser-compatible tool이었음  
아래와 같은 간단한 layout도 간단하게 할 수 없었음
- Vertically centering a block of content inside its parent
- Making all the children of a container take up an equal amount of the available width/height, regardless of how much width/height is availble
- Making all columns in a multiple-column layout adopt the same height even if they contain a different amount of content

Flexbox로는 이걸 쉽게 할 수 있다

### Introducing a simple example
Flexbox를 소개하기 위해 아래 예제를 사용할 예정(`flexbox0.html`, `style.css`)

HTML:  
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Flexbox 0 — starting code</title>
    <link href="style.css" rel="stylesheet" type="text/css">
  </head>
  <body>
    <header>
      <h1>Sample flexbox example</h1>
    </header>

    <section>
      <article>
        <h2>First article</h2>

        <p>Tacos actually microdosing, pour-over semiotics banjo chicharrones retro fanny pack portland everyday carry vinyl typewriter. Tacos PBR&B pork belly, everyday carry ennui pickled sriracha normcore hashtag polaroid single-origin coffee cold-pressed. PBR&B tattooed trust fund twee, leggings salvia iPhone photo booth health goth gastropub hammock.</p>
      </article>

      <article>
        <h2>Second article</h2>

        <p>Tacos actually microdosing, pour-over semiotics banjo chicharrones retro fanny pack portland everyday carry vinyl typewriter. Tacos PBR&B pork belly, everyday carry ennui pickled sriracha normcore hashtag polaroid single-origin coffee cold-pressed. PBR&B tattooed trust fund twee, leggings salvia iPhone photo booth health goth gastropub hammock.</p>
      </article>

      <article>
        <h2>Third article</h2>

        <p>Tacos actually microdosing, pour-over semiotics banjo chicharrones retro fanny pack portland everyday carry vinyl typewriter. Tacos PBR&B pork belly, everyday carry ennui pickled sriracha normcore hashtag polaroid single-origin coffee cold-pressed. PBR&B tattooed trust fund twee, leggings salvia iPhone photo booth health goth gastropub hammock.</p>

        <p>Cray food truck brunch, XOXO +1 keffiyeh pickled chambray waistcoat ennui. Organic small batch paleo 8-bit. Intelligentsia umami wayfarers pickled, asymmetrical kombucha letterpress kitsch leggings cold-pressed squid chartreuse put a bird on it. Listicle pickled man bun cornhole heirloom art party.</p>
      </article>
    </section>
  </body>
</html>
```

CSS:  
```css
html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

header {
  background: purple;
  height: 100px;
}

h1 {
  text-align: center;
  color: white;
  line-height: 100px;
  margin: 0;
}

article {
  padding: 10px;
  margin: 10px;
  background: aqua;
}

/* Add your flexbox CSS below here */
```

|Result:|
|:---|
|![css-flexbox-ex3](https://github.com/siriyaoff/MDN-note/blob/master/images/css-flexbox-ex1.PNG?raw=true)|

### Specifying what elements to lay out as flexible boxes
flex container로 만들 element에 `display: flex;`를 적용시켜서 flex container를 구현  
=> 자동으로 child elements가 flex items가 됨

#### Example
`style.css`에 아래 rule을 추가하고 유지:  
```css
section {
  display: flex;
}
```

|Result:|
|:---|
|![css-flexbox-ex4](https://github.com/siriyaoff/MDN-note/blob/master/images/css-flexbox-ex2.PNG?raw=true)|

- 위 예시의 경우 `<section>`이 flex container, `<article>`이 flex item
- default values에 의해 모든 열들이 같은 열 너비, 높이를 가짐
- flex container는 block-level element와 같이 취급됨
- `display: inline-flex;`를 사용하면 flex items를 inline element같이 취급되게 할 수 있음

### The flex model
![css-flex-model](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox/flex_terms.png)
- **Main axis** : the axis running in the direction the flex items are being laid out.
- **Cross axis** : the axis running perpendicular to the direction the flex items are being laid out.
- **Flex container** : the parent element that has `display: flex;`
- **Flex items** : the items being laid out as flexible boxes inside the flex container
- flex item은 main axis, cross axis를 기준으로 main size, cross size를 가짐

### Columns or rows?
`flex-direction` property를 이용해서 main axis의 위상을 설정할 수 있음  
possible value : `row`, `column`, `row-reverse`, `column-reverse` (default : `row`)  
main axis가 명시된 후 flex item들이 나열되는 방향은 browser's default language의 방향에 따름(rl or lr)

#### Example
`style.css`의 `section` rule에 아래 declaration을 임시로 추가하면:  
```css
flex-direction: column;
```

|Result:|
|:---|
|![css-flexbox-ex5](https://github.com/siriyaoff/MDN-note/blob/master/images/css-flexbox-ex3.PNG?raw=true)|

### Wrapping
flex item의 width or height를 고정하면 item이 많을 때 flex container를 overflow함(flex item을 임시로 추가함)  
![css-flexbox-ex6](https://github.com/siriyaoff/MDN-note/blob/master/images/css-flexbox-ex4.PNG?raw=true)
- `<h1>`은 vw의 100%를 차지하는 듯
- flex item들이 overflow해서 flex container의 영역 밖으로 배치됨
- CSS에 flex item의 width를 고정하는 rule을 넣지 않았지만 최소 width같은게 있는 듯

`style.css`의 `section` rule에 아래 declaration을 임시로 추가하면:  
```css
flex-wrap: wrap;
```

`style.css`의 `article` rule에 아래 declaration을 임시로 추가하면:  
```css
flex: 200px;
```

|Result:|
|:---|
|![css-flexbox-ex7](https://github.com/siriyaoff/MDN-note/blob/master/images/css-flexbox-ex5.PNG?raw=true)|

- `flex-wrap: warp;`을 flex container에 적용하면 overflow되는 item들을 다음 줄로 내림
- `flex: 200px;`를 flex item에 적용하면 flex item의 최소 main size를 `200px`로 제한함
- flex container의 `flex-direction`이 `row-reverse`일 경우에 여러 줄의 flex item이 있으면 아예 역순으로 나열되는 것이 아니라, 원래 순서대로 나열한 다음에 줄별로 역순으로 바꿈<br>default language의 방향에 따라 reverse가 적용된다는 것을 생각하면됨<br>![css-flexbox-ex8](https://github.com/siriyaoff/MDN-note/blob/master/images/css-flexbox-ex6.PNG?raw=true)

### flex-flow shorthand
`flex-direction`, `flex-wrap` properties를 `flex-flow` shorthand property로 줄여쓸 수 있음

#### Example
```css
flex-direction: row;
flex-wrap: wrap;
```

is equal to

```css
flex-flow: row wrap;
```

### Flexible sizing of flex items
`style.css`에 아래 rule을 임시로 추가:  
```css
article {
  flex: 1 200px;
}

article:nth-of-type(3) {
  flex: 2 200px;
}
```

|Result:|
|:---|
|![css-flexbox-ex9](https://github.com/siriyaoff/MDN-note/blob/master/images/css-flexbox-ex7.PNG?raw=true)|

- `flex: 1 200px;`에서
	- 첫 번째 값 `1`은 proportion unit으로, 각 list item의 main size의 비율을 정함
	- 두 번째 값 `200px`는 위에서와 같은 최소 main size임
- 최소 main size가 정의되어 있으면 각각의 flex item에 그만큼씩 준 다음, proportion unit에 따라서 남은 공간을 분배한다고 생각하면 됨
- flex item도 기본적으로 content box일 듯
- browser window를 조절해도 layout이 유지됨 => flexibility, responsiveness ↑

### flex: shorthand versus longhand
`flex` property의 longhand properties 3개:
- `flex-grow` : main size의 비율을 정하는 unitless proportion value(위 `flex: 1 200px;`의 `1`)
- `flex-shrink` : overflow가 일어날 때 각 list item들이 줄어드는 비율을 정하는 unitless proportion value(클 수록 더 많이 줄어듬)
- `flex-basis` : 최소 main size(위 `flex: 1 200px;`의 `200px`)

웬만하면 longhand는 사용하지 않는게 좋음(shorthand가 더 가독성이 좋음)

### Horizontal and vertical alignment
아래 예제를 사용할 예정(`flex-align0.html`, `style.css`)

HTML:  
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Flexbox align 0 — starting code</title>
    <link href="style.css" rel="stylesheet" type="text/css">
  </head>
  <body>
    <div>
      <button>Smile</button>
      <button>Laugh</button>
      <button>Wink</button>
      <button>Shrug</button>
      <button>Blush</button>
    </div>
  </body>
</html>
```

CSS:  
```css
html {
  font-family: sans-serif;
}

body {
  width: 70%;
  max-width: 960px;
  margin: 20px auto;
}

button {
  font-size: 18px;
  line-height: 1.5;
  width: 15%;
}

div {
  height: 100px;
  border: 1px solid black;
}

/* Add your flexbox CSS below here */
```

|Result:|
|:---|
|![css-flexbox-align-ex1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-flexbox-align-ex1.PNG?raw=true)|

`style.css`에 아래 rule을 추가:  
```css
div {
  display: flex;
  align-items: center;
  justify-content: space-around;
}

button:first-child { /* 이 rule은 예시를 본 후 지움 */
  align-self: flex-end;
}
```

|Result:|
|:---|
|![css-flexbox-align-ex2](https://github.com/siriyaoff/MDN-note/blob/master/images/css-flexbox-align-ex2.PNG?raw=true)|

- `<button>`의 `width`가 `15%`로 설정되어있기 때문에 공간을 다 차지하지 않음
	- `30%`로 설정하면 overflow하지 않고 공간을 다 채우기만 함
	- `width`를 설정하지 않으면 공간을 다 차지함
- `align-items` property : cross axis를 기준으로 flex item을 제어함<br>Possible values:
	- `stretch` : default 값<br>cross start쪽으로 flex items를 붙이고 cross axis 방향으로 flex item을 scale<br>만약 parent가 fixed length를 가지지 않으면 flex items 중 가장 긴(cross axis 기준) 값에 맞춤
	- `center` : flex item의 intrinsic dimension을 유지하지만 cross axis 기준 가운데로 정렬시킴
	- `flex-start`, `flex-end` : 각각 cross start, end쪽으로 flex items를 붙임
	- `baseline` : cross start로 붙이고 flex items의 content(text)의 밑을 일정하게 맞춤
- `align-items`는 `align-self` property로 override 가능(개별의 flex item에 적용시킬 때 사용)
- `justify-content` property : main axis를 기준으로 flex item을 제어함<br>Values available:
	- `flex-start` : default 값<br>main start로 붙임
	- `flex-end` : main end로 붙임
	- `center` : main axis 기준 가운데로 정렬(flex item의 intrinsic dimension 유지)
	- `space-around` : main axis를 따라서 container안에서 flex items가 균동하게 분포됨(첫 번째와 마지막 item이 container와 붙은 쪽의 여백은 flex items 사이의 여백의 반으로 처리됨)
	- `space-between` : main axis를 따라서 container안에서 flex items가 균동하게 분포됨(첫 번째와 마지막 item이 container와 붙은 쪽의 여백은 없어짐 = 첫 번째와 마지막 item은 container와 딱 붙어있음)
- 즉, `align-items`, `justify-content` properties는 flex container의 flow direction을 알아야 사용 가능

![css-flexbox-align-justify](https://github.com/siriyaoff/MDN-note/blob/master/images/css-flexbox-align-justify.PNG?raw=true)

### Ordering flex items
Source order(HTML에서 순서)를 건드리지 않고 flex items의 layout order를 바꾸는 것도 가능함  
flex item에 `order` property를 적용해서 순서를 정함  
accessibility가 떨어질 수 있음

#### Example
`style.css`에 아래 rule을 추가:  
```css
button:first-child {
  order: 1;
}
```

|Result:|
|:---|
|![css-flexbox-order](https://github.com/siriyaoff/MDN-note/blob/master/images/css-flexbox-order.PNG?raw=true)|

- `order`의 default value : `0`
- 값이 클수록 우선순위가 떨어짐
- 값이 같다면 source order를 따름
- 값에 `-1`를 넣을 수도 있음(=> default인 `0`보다 작으므로 가장 먼저 나타남)

### Nested flex boxes
Flex boxes를 nesting하는 것도 가능함  
이때까지 나온 예제들을 다 합해보면

HTML:  
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Complex flexbox example</title>
    <link href="style.css" rel="stylesheet" type="text/css">
  </head>
  <body>
    <header>
      <h1>Complex flexbox example</h1>
    </header>

    <section>
      <article>
        <h2>First article</h2>

        <p>Tacos actually microdosing, pour-over semiotics banjo chicharrones retro fanny pack portland everyday carry vinyl typewriter. Tacos PBR&B pork belly, everyday carry ennui pickled sriracha normcore hashtag polaroid single-origin coffee cold-pressed. PBR&B tattooed trust fund twee, leggings salvia iPhone photo booth health goth gastropub hammock.</p>
      </article>

      <article>
        <h2>Second article</h2>

        <p>Tacos actually microdosing, pour-over semiotics banjo chicharrones retro fanny pack portland everyday carry vinyl typewriter. Tacos PBR&B pork belly, everyday carry ennui pickled sriracha normcore hashtag polaroid single-origin coffee cold-pressed. PBR&B tattooed trust fund twee, leggings salvia iPhone photo booth health goth gastropub hammock.</p>
      </article>

      <article>
        <div>
          <button>Smile</button>
          <button>Laugh</button>
          <button>Wink</button>
          <button>Shrug</button>
          <button>Blush</button>
        </div>
        <div>
          <p>Tacos actually microdosing, pour-over semiotics banjo chicharrones retro fanny pack portland everyday carry vinyl typewriter. Tacos PBR&B pork belly, everyday carry ennui pickled sriracha normcore hashtag polaroid single-origin coffee cold-pressed. PBR&B tattooed trust fund twee, leggings salvia iPhone photo booth health goth gastropub hammock.</p>
        </div>
        <div>
          <p>Cray food truck brunch, XOXO +1 keffiyeh pickled chambray waistcoat ennui. Organic small batch paleo 8-bit. Intelligentsia umami wayfarers pickled, asymmetrical kombucha letterpress kitsch leggings cold-pressed squid chartreuse put a bird on it. Listicle pickled man bun cornhole heirloom art party.</p>
        </div>
      </article>
    </section>
  </body>
</html>
```

CSS:  
```css
html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

header {
  background: purple;
  height: 100px;
}

h1 {
  text-align: center;
  color: white;
  line-height: 100px;
  margin: 0;
}

article {
  padding: 10px;
  margin: 10px;
  background: aqua;
}

/* Add your flexbox CSS below here */

section {
  display: flex;
}

article {
  flex: 1 200px;
}

article:nth-of-type(3) {
  flex: 3 200px;
  display: flex;
  flex-flow: column;
}

article:nth-of-type(3) div:first-child {
  flex: 1 100px;
  display: flex;
  flex-flow: row wrap;
  align-items: center;
  justify-content: space-around;
}

button {
  flex: 1 auto;
  margin: 5px;
  font-size: 18px;
  line-height: 1.5;
}
```

|Result:|
|:---|
|![css-flexbox-nesting](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox/flexbox-example7.png)|

- flexbox로 지정되는 element는 모두 block element이기 때문에 HTML에서 table, list를 nest하는 것과 비슷함
- flex container 관련 properties:
	- `display`
	- `flex-flow`(`flex-direction` `flex-wrap`)
	- `align-items` : cross axis 기준
	- `justify-content` : main axis 기준
	- `align-content` (여러 줄로 펼쳐졌을 때)
- flex item 관련 properties:
	- `flex`(`flex-grow` `flex-shrink` `flex-basis`)
	- `align-self`
	- `order`
	- `z-index` : grid에서의 설명 참고

### Cross-browser compatibility
IE는 IE11+에서만 flex를 지원함!  
flex같은 layout method는 지원되지 않으면 웹사이트를 아예 unusable하게 만들어버리기 때문에 주의

## Grids
### What is grid layout?
Grid : two-dimensional layout system for the web

![css-grid-model](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Grids/grid.png)
- **column**, **row**, **gutter**로 이루어짐

### Creating your grid in CSS
- `grid-area`로 element별 alias를 만들어두면 `grid-template-areas`를 이용해서 그걸로 바로 layout을 짤 수 있음
- `grid-gap`으로 gutter 설정 가능
- `grid-template-rows`, `grid-template-columns`로 row, column 별로 sizing 가능

#### Defining a grid
아래 예제를 사용(`0-stargint-point.html`, `style.css`)  
HTML:  
```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>CSS Grid starting point</title>
    <link href="style.css" rel="stylesheet" type="text/css">
</head>

<body>
    <h1>Simple grid example</h1>

    <div class="container">
        <div>One</div>
        <div>Two</div>
        <div>Three</div>
        <div>Four</div>
        <div>Five</div>
        <div>Six</div>
        <div>Seven</div>
    </div>

</body>

</html>
```

CSS:  
```css
body {
  width: 90%;
  max-width: 900px;
  margin: 2em auto;
  font: .9em/1.2 Arial, Helvetica, sans-serif;
}

.container > div {
  border-radius: 5px;
  padding: 10px;
  background-color: rgb(207,232,220);
  border: 2px solid rgb(79,185,227);
}
```

|Result:|
|:---|
|![css-grid-ex3](https://github.com/siriyaoff/MDN-note/blob/master/images/css-grid-ex3.PNG?raw=true)|

`style.css`에 아래 rule을 추가:  
```css
.container {
  display: grid;
  grid-template-columns: 200px 200px 200px;
}
```

|Result:|
|:---|
|![css-grid-ex4](https://github.com/siriyaoff/MDN-note/blob/master/images/css-grid-ex4.PNG?raw=true)|

- `display: grid;`를 적용해서 grid layout 사용
	- single column grid가 default로 적용됨
- `grid-template-columns` property를 사용해서 columns와 너비를 정의

#### Flexible grids with the fr unit
Use `fr` unit to flexibly size grid rows and columns  
`fr` represents *one* fraction of the available space in the grid container  
=> `flex-grow`의 proportional value와 비슷하게, grid container의 남은 공간을 `fr`끼리 나눠가짐

#### Example
`style.css`의 `.container` rule을 변경:  
```css
.container {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
}
```

|Result:|
|:---|
|![css-grid-ex5](https://github.com/siriyaoff/MDN-note/blob/master/images/css-grid-ex5.PNG?raw=true)|

- `grid-template-rows`(`-columns`)에 `fr`과 fixed length를 섞어서 사용할 수 있음
	- fixed length에 공간을 분배한 다음 남은 공간을 `fr`들이 가져감
	- grid items 중 하나가 공간을 많이 차지할 경우 `fr`이 나눠가질 공간이 없어짐

#### Gaps between tracks
`column-gap`, `row-gap`, `gap` properties를 사용해서 gutter 설정 가능

#### Example
`style.css`의 `.container` rule을 변경:  
```css
.container {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
  gap: 20px;
}
```

|Result:|
|:---|
|![css-grid-ex5](https://github.com/siriyaoff/MDN-note/blob/master/images/css-grid-ex5.PNG?raw=true)|

- `gap`에는 `fr` unit 사용 불가

> `*gap*` properties는 `grid-` prefix가 붙어 있었지만 수정됨(다른 layout methods에서도 gap을 사용하기 위해)  
> 하지만 prefixed version이 유지되기 때문에 bulletproof하게 만들려면 둘 다 추가하면 됨(`grid-gap`, `gap`)

#### Repeating track listings
`repeat` function을 이용해서 반복되는 설정을 선언 가능  
두 번째 parameter는 track listing으로, 여러 값이 들어갈 수 있음
e.g. `repeat(3, 1fr 2fr)` is equal to `1fr 2fr 1fr 2fr 1fr 2fr`

#### The implicit and explicit grid
- Explicit grid : `grid-template-columns`, `grid-template-rows`를 이용해서 생성된 grid
- Implicit grid : explicit grid로 선언되지 않았을 때 자동으로 생성됨
	- `auto`로 sizing됨 : content를 채울 만큼 커짐
	- `grid-auto-rows`, `grid-auto-columns`를 사용해서 implicit grid에 size를 선언 가능<br>implicit grid는 몇 개로 선언될 지 모르기 때문에 size를 한 번에 정의해야 함

#### Example
`style.css`의 `.container` rule을 변경:  
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 100px;
  gap: 20px;
}
```

|Result:|
|:---|
|![css-grid-ex7](https://github.com/siriyaoff/MDN-note/blob/master/images/css-grid-ex7.PNG?raw=true)|

- explicit grid, implicit grid을 둘 다 사용할 수 있음

#### Example
```css
.container {
  grid-template-columns: 50px;
  grid-auto-columns: 1fr 2fr;
}
```

위와 같이 선언하면 column line number 1만 `50px`로 고정되고 나머지 column들은 `1fr 2fr`의 패턴으로 반복됨

이 때 implicit columns를 만드는 item 다음 item부터 영역을 지정해놓지 않으면, 자동으로 grid에 순서대로 들어감(`grid-auto-flow`에 따라서 배치됨)

#### `grid-auto-flow`
items가 배치되는 방법을 정의함  
possible values:
- `row` : item의 순서대로 row를 하나씩 채워나감(item을 넣을 수 없으면 다음 row로 이동)
- `column` : item의 순서대로 column을 하나씩 채워나감(item을 넣을 수 없으면 다음 column로 이동)
- `dense` : item의 순서 상관없이 빈틈이 없게 채움
- `row dense` : item의 순서 상관없이 빈틈이 없게 채우는데 row가 우선적으로 채워짐
- `column dense` : item의 순서 상관없이 빈틈이 없게 채우는데 column이 우선적으로 채워짐

#### The minmax() function
`minmax()` function을 이용해서 min, max size 지정 가능  
`auto`를 이용하면 max가 content에 맞춰지게 설정 가능  
e.g. `grid-auto-rows: minmax(100px, auto);`  
![css-grid-ex8](https://github.com/siriyaoff/MDN-note/blob/master/images/css-grid-ex8.PNG?raw=true)|

※ row/column이 늘어나는 것은 다른 item에도 영향을 줌

#### As many columns as will fit
가능한 많은 열을 만들고 싶을 때  
`grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));`  
와 같이 사용 가능

#### Example
`style.css`의 `.container` rule을 변경:  
```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  grid-auto-rows: minmax(100px, auto);
  gap: 20px;
}
```

|Result:|
|:---|
|![css-grid-ex9](https://github.com/siriyaoff/MDN-note/blob/master/images/css-grid-ex9.PNG?raw=true)|
|![css-grid-ex10](https://github.com/siriyaoff/MDN-note/blob/master/images/css-grid-ex10.PNG?raw=true)|

- flex에서 flex items의 width를 지정하지 않았을 때 늘어나는 것과 비슷
- column은 너비가 200px인 col을 최대로 만든 다음, 남는 공간은 균등하게 분배
- row는 최소 100px, 각 row별로 필요한 만큼 늘어남
- `auto-fill` : items의 총 너비가 container의 너비보다 작을 경우 공간을 남김
- `auto-fit` : items의 총 너비가 container의 너비보다 작을 경우 공간을 채움(items가 늘어남)

### Line-based placement
grid의 line은 1에서 시작하고, writing mode에 의해서 방향이 결정됨  
영어는 lr => 1 ... n, 아랍어는 rl => n ... 1

`grid-column-start`, `grid-column-end`, `grid-row-start`, `grid-row-end` properties를 이용해서 item을 원하는 영역에 배치 가능  
`grid-column`, `grid-row` shorthand properties 사용 가능  
(`/`를 이용해서 구분)

#### Example
CSS:  
```css
header {
  grid-column: 1 / 3;
  grid-row: 1;
}

article {
  grid-column: 2;
  grid-row: 2;
}

aside {
  grid-column: 1;
  grid-row: 2;
}

footer {
  grid-column: 1 / 3;
  grid-row: 3;
}
```

|Result:|
|:---|
|![css-grid-ex11](https://github.com/siriyaoff/MDN-note/blob/master/images/css-grid-ex11.PNG?raw=true)|

- `-1`과 같이 음수도 사용 가능(끝에서부터 count됨)
- `grid-row: 1;`과 같이 row를 선언할 수도 있음<br>=> 하나의 row만 차지한다는 뜻임(⇔ `grid-row: 1 / 2;`)
- `span`을 이용할 수도 있음<br>e.g. `1 / span 2` is equal to `1 / 3`

### Positioning with grid-template-areas
`grid-template-areas` property를 이용해서 items를 배치할 수 있음

#### Example
CSS:  
```css
.container {
  display: grid;
  grid-template-areas:
      "header header"
      "sidebar content"
      "footer footer";
  grid-template-columns: 1fr 3fr;
  gap: 20px;
}

header {
  grid-area: header;
}

article {
  grid-area: content;
}

aside {
  grid-area: sidebar;
}

footer {
  grid-area: footer;
}
```

|Result:|
|:---|
|Line-based placement와 같음|

- line number를 사용하지 않고 배치 가능
- `grid-area`로 각 item들의 alias를 줘야 함
- `grid-template-areas`로 item들을 배치
- grid의 모든 cell이 채워져야 함
	- span을 하기 위해선 span할 영역을 모두 채움
	- cell을 빈칸으로 남기기 위해선 `.` 사용
- 영역들은 모두 직사각형임, L-shaped area 불가능
- areas는 다른 위치에 반복될 수 없음(떨어진 두 영역을 차지할 수 없음)

### A CSS Grid, grid framework
Grid frameworks는 12-16 column grids임

#### Example
CSS:  
```css
.container {
  display: grid;
  grid-template-columns: repeat(12, minmax(0,1fr));
  grid-gap: 20px;
}

header {
  grid-column: 1 / 13;
  grid-row: 1;
}

article {
  grid-column: 4 / 13;
  grid-row: 2;
}

aside {
  grid-column: 1 / 4;
  grid-row: 2;
}

footer {
  grid-column: 1 / 13;
  grid-row: 3;
}
```

|Result:|
|:---|
|![css-grid-ex12](https://github.com/siriyaoff/MDN-note/blob/master/images/css-grid-ex12.PNG?raw=true)|

- line-based placement를 지정하지 않으면 각각의 item들은 column 하나씩을 차지함(row는 implicit grid이기 때문에 자동으로 한 줄만 생성됨)
- `grid-template-*`의 `fr`으로 비율을 설정할 수도 있지만 위와 같이 frameworks를 이용해서 비율을 설정할 수도 있음

### Grid 정렬
Flex에서와 비슷함

#### `align-items`
grid cells 내에서 item을 column 방향으로 정렬  
container에 적용  
possible values:
- `stretch`
- `start`, `end`
- `center`

#### `justify-items`
grid cells 내에서 item을 row 방향으로 정렬  
container에 적용  
possible values:
- `stretch`
- `start`, `end`
- `center`

#### `align-content`
grid container 내에서 items를 column 방향으로 정렬  
container에 적용  
possible values:
- `stretch`
- `start`, `end`
- `center`
- `space-between`, `space-around`, `space-evenly`

#### `justify-content`
grid container 내에서 items를 row 방향으로 정렬  
container에 적용  
possible values:
- `stretch`
- `start`, `end`
- `center`
- `space-between`, `space-around`, `space-evenly`

#### `align-self`
item을 column 방향으로 정렬  
item에 적용  
possible values:
- `stretch`
- `start`, `end`
- `center`

#### `justify-self`
item을 row 방향으로 정렬  
item에 적용  
possible values:
- `stretch`
- `start`, `end`
- `center`

#### shorthands
- `place-items` : `align-items` `justify-items` 순서로 작성
- `place-content` : `align-content` `justify-content` 순서로 작성
- `place-self` : `align-self` `justify-self` 순서로 작성

※ 각 property의 예시는 [여기](https://studiomeal.com/archives/533) 참고  
flex와 다르게 `justify-items`가 추가됨(2차원이기 때문에)

### Grid order
flex와 마찬가지로 `order` property를 이용해서 우선순위 정의  

### z-index
`z-index` property를 이용해서 z축으로 정렬할 수도 있음  
value가 클수록 item이 위로 올라옴  
grid item에 적용  
default value : `0`

### Properties
Grid container 관련 properties:
- `display`
- `gap`(`row-gap` `column-gap`)
- `grid-template-areas` : alias로 영역 지정
- `grid-template-rows`
- `grid-template-columns`
- `grid-auto-rows`
- `grid-auto-columns`
- `grid-auto-flow` : implicit grid에 대해 item이 채워지는 방식 정의
- `place-items`(`align-items` `justify-items`)
	- `align-items`(grid cell 내에서 vertical 정렬)
	- `justify-items`(grid cell 내에서 horizontal 정렬)
- `place-content`(`align-content` `justify-content`)
	- `align-content`(items 전체의 vertical 정렬)
	- `justify-content`(items 전체의 horizontal 정렬)

Grid item 관련 properties:
- `grid-area` : item의 alias 지정
- `grid-column`
- `grid-row`
- `align-self` : item의 `align-items` overriding
- `justify-self` : item의 `justify-items` overriding
- `order` : 나열되는 순서 설정
- `z-index` : z축으로 우선순위 설정

## Floats
### The background of floats
`float`로 처음에는 image만 띄우다가 다른 요소들도 float할 수 있다는 것을 깨닫고 용도가 다양해짐  
나중에는 아예 web site layout을 float로 구성함  
최근에는 더 나은 layout techniques가 나왔기 때문에 float를 사용한 layout은 이제 *legacy technique*로 취급됨  
이 article에서는 site layout이 아닌 proper uses를 살펴볼 예정

### A simple float example
아래 예제를 이용할 예정:  
HTML:  
```html
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="utf-8">
    <title>My test page</title>
    <link href="style.css" rel="stylesheet" type="text/css">
  </head>
  <body>
<h1>Simple float example</h1>

<div class="box">Float</div>

<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla luctus aliquam dolor, eu lacinia lorem placerat vulputate. Duis felis orci, pulvinar id metus ut, rutrum luctus orci. Cras porttitor imperdiet nunc, at ultricies tellus laoreet sit amet. </p>

<p>Sed auctor cursus massa at porta. Integer ligula ipsum, tristique sit amet orci vel, viverra egestas ligula. Curabitur vehicula tellus neque, ac ornare ex malesuada et. In vitae convallis lacus. Aliquam erat volutpat. Suspendisse ac imperdiet turpis. Aenean finibus sollicitudin eros pharetra congue. Duis ornare egestas augue ut luctus. Proin blandit quam nec lacus varius commodo et a urna. Ut id ornare felis, eget fermentum sapien.</p>

<p>Nam vulputate diam nec tempor bibendum. Donec luctus augue eget malesuada ultrices. Phasellus turpis est, posuere sit amet dapibus ut, facilisis sed est. Nam id risus quis ante semper consectetur eget aliquam lorem. Vivamus tristique elit dolor, sed pretium metus suscipit vel. Mauris ultricies lectus sed lobortis finibus. Vivamus eu urna eget velit cursus viverra quis vestibulum sem. Aliquam tincidunt eget purus in interdum. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.</p>
  </body>
</html>
```

CSS:  
```css
body {
  width: 90%;
  max-width: 900px;
  margin: 0 auto;
  font: .9em/1.2 Arial, Helvetica, sans-serif
}

.box {
  float: left;
  margin-right: 15px;
  width: 150px;
  height: 100px;
  border-radius: 5px;
  background-color: rgb(207,232,220);
  padding: 1em;
}
```

|Result:|
|:---|
|![css-float-ex1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-float-ex1.PNG?raw=true)|

- float가 적용된 element(`.box`)는 normal flow에서 제외되고 parent container의 왼쪽에 배치됨
- normal layout flow에서 `.box` 뒤에 오는 element는 `.box`를 감쌈(`.box`보다 윗쪽은 제외)
- floated item과 다른 element 사이에 여백을 추가하려면 floated item의 margin을 조절해야 함
	- 위의 예제에서 `<p>`의 padding을 조절해도 floated와의 여백은 그대로임<br>∵ `.box`가 normal flow에서 제외되어서 `<p>`들은 `.box` 밑에서 layout되기 때문
	- 첫 번째 `<p>`의 영역을 표시해보면 아래와 같음<br>![css-float-ex2](https://github.com/siriyaoff/MDN-note/blob/master/images/css-float-ex2.PNG?raw=true)
	- line box와 관련있음(line box : each line을 감싸는 box, containing block과는 다름)
- `display: inline-block;`을 적용한 것과 비슷한 효과임

### Clearing floats
`clear` property를 이용해서 following elements가 float를 wrap하는 것을 멈출 수 있음  
possible values:
- `left` : 왼쪽에 floated item이 없게 배치됨
- `right` : 오른쪽에 floated item이 없게 배치됨
- `both` : 양쪽에 floated item이 없게 배치됨

#### Example
두 번째 `<p>`에 아래 CSS 추가:  
```css
.cleared {
  clear: left;
}
```

|Result:|
|:---|
|![css-float-ex3](https://github.com/siriyaoff/MDN-note/blob/master/images/css-float-ex3.PNG?raw=true)|

- clearing이라는 keyword의 의미는 normal flow에서 제외된 상태인 float를 다시 인식시킨다 정도로 생각하면 될 듯

### Clearing boxes wrapped around a float
float와 첫 번째 문단을 `<div class="wrapper">`로 감싸고 `.cleared` rule 지운 다음 아래 css 추가:  
HTML:  
```html
...
<div class="wrapper">
  <div class="box">Float</div>

  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla luctus aliquam dolor, eu lacinia lorem placerat vulputate.</p>
</div>
...
```

CSS:  
```css
.wrapper {
  background-color: rgb(79,185,227);
  padding: 10px;
  color: #fff;
}
```

|Result:|
|:---|
|![css-float-ex4](https://github.com/siriyaoff/MDN-note/blob/master/images/css-float-ex4.PNG?raw=true)|

- float가 normal flow에서 제외되었기 때문에 box가 제대로 감싸지 못함
	- following element를 clear해도 해결되지 않음
	- 3가지 solution이 존재

#### The clearfix hack
clearfix hack : generated content를 wrapping box뒤에 삽입해서 clear both 추가하는 방법  
```css
.wrapper::after {
  content: "";
  clear: both;
  display: block;
}
```

|Result:|
|:---|
|![css-float-ex5](https://github.com/siriyaoff/MDN-note/blob/master/images/css-float-ex5.PNG?raw=true)|

- wrapper 뒤에 element를 삽입하고 `clear: both`를 추가한 것과 같음

#### Using overflow
`overflow: auto;`를 사용해서 해결할 수도 있음(default: `visible`)  
`overflow: auto;`에 의해 BFC가 생성되어서 clear됨  
보통 해결되지만, `overflow` 사용으로 인해 unwanted scrollbars or clipped shadows가 생길 수 있음

`.wrapper`을 아래 css로 변경:  
```css
.wrapper {
  background-color: rgb(79,185,227);
  padding: 10px;
  color: #fff;
  overflow: auto;
}
```

결과는 clearfix hack을 사용했을 때와 같음

#### display: flow-root
modern way of solving this problem  
`display: flow-root;`를 `overflow: auto;` 대신 사용하면 됨  
원리는 BFC를 생성하는 것으로 위 방법들과 동일함

결과는 clearfix hack과 같음

## Positioning
### Introducing positioning
The whole idea of positioning is to allow us to override the basic document flow behavior, to produce interesting effects.

`position` property를 사용해서 구현

아래 예제를 사용할 예정:  
HTML:  
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Basic document flow</title>

  </head>
  <body>
    <h1>Basic document flow</h1>

    <p>I am a basic block level element. My adjacent block level elements sit on new lines below me.</p>

    <p>By default we span 100% of the width of our parent element, and our height is as tall as our child content. Our total width and height is our content + padding + border width/height.</p>

    <p>We are separated by our margins. Because of margin collapsing, we are separated by the width of one of our margins, not both.</p>

    <p>inline elements <span>like this one</span> and <span>this one</span> sit on the same line as one another, and adjacent text nodes, if there is space on the same line. Overflowing inline elements <span>wrap onto a new line if possible — like this one containing text</span>, or just go on to a new line if not, much like this image will do: <img src="https://github.com/mdn/learning-area/blob/master/css/css-layout/positioning/long.jpg?raw=true"></p>

  </body>
</html>

```

CSS:  
```css
body {
  width: 500px;
  margin: 0 auto;
}

p {
  background: aqua;
  border: 3px solid blue;
  padding: 10px;
  margin: 10px;
}

span {
  background: red;
  border: 1px solid black;
}
```

|Result:|
|:---|
|![css-position-ex1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-position-ex1.PNG?raw=true)|

### Static positioning
`position: static;`을 사용해서 구현  
`position` property의 default value  
element를 normal flow에서의 위치에 배치

#### Example
두 번째 p에 `positioned` class 추가하고 rule 선언:  
HTML:  
```html
<p class="positioned">...</p>
```

CSS:  
```css
.positioned {
  position: static;
  background: yellow;
}
```

|Result:|
|:---|
|![css-position-ex2](https://github.com/siriyaoff/MDN-note/blob/master/images/css-position-ex2.PNG?raw=true)|

- static positioning이 default behavior이기 때문에 위치는 변화없음

### Relative positioning
`relative` value 이용  
element가 normal flow에 의해 배치된 다음 `top`, `bottom`, `left`, `right` properties 이용해서 final position을 수정 가능  

#### Introducing top, bottom, left, and right
위에 4개의 properties(`top`, `bottom`, `left`, `right`)는 positioned element를 옮기기 위해 `position`과 함께 사용됨

#### Example
`.positioned` rule을 변경:  
```css
.positioned {
  position: relative;
  top: 30px;
  left: 30px;
  background: yellow;
}
```

|Result:|
|:---|
|![css-position-ex3](https://github.com/siriyaoff/MDN-note/blob/master/images/css-position-ex3.PNG?raw=true)|

- `top`, `bottom`, `left`, `right`의 value로 pixels, mm, rems, % 등의 unit들이 가능함
- `top: 30px;`는 위에 30px만큼 거리를 띄운다고 생각하면 될 듯

### Absolute positioning
absolute positioned element는 normal document layout flow에서 제외되고, 자신만의 layer에 배치되어 다른 elements와 간섭하지 않음  
absolute positioning에서는 `top`, `bottom`, `left`, `right`가 normal flow에서의 relative position 기준이 아니라 containing block을 기준으로 거리를 벌림

#### Example
`.positioned` rule을 변경:  
```css
position: absolute;
```

|Result:|
|:---|
|![css-position-ex4](https://github.com/siriyaoff/MDN-note/blob/master/images/css-position-ex4.PNG?raw=true)|

- `top`, `bottom`, `left`, `right`, `margin` 모두 `0`으로 설정하면 화면을 가득 채움<br>=>`margin`이 적용됨(margin collapsing은 일어나지 않음)

#### Positioning contexts
`position`의 value에 따라서 containing block을 구하는 방법:
1. `position` : `static`, `relative`, `sticky`
	- the *content box* of the nearest ancestor element that is either a **block container** or **establishes a formatting context**
2. `position` : `absolute`
	- the *padding box* of the nearest ancestor element that has a `position` value other than `static`(e.g. `relative`, `sticky`, `fixed`, `absolute`)
3. `position` : `fixed`
	- the viewport or the page area
4. `position` : `fixed`, `absolute`의 경우 다른 기준도 있음

**Initial containing block** : the containing block in which the root element(`<html>`) resides
- Initial containing block에 relative할 경우 `<html>` element 밖에 display됨(relative to initial viewport)

위 예시에서는 absolute positioned element가 `<body>`안에 nested되어 있지만, final layout에서는 relative to the page area  
**positioning context** : which element the absolutely positioned element is positioned relative to
- absolutely positioned element의 ancestors 중 하나에 positioning을 설정해서 바꿀 수 있음
- element가 nesting하고 있는 elements에만 relative하게 position할 수 있음

`<body>`에 declaration 추가:  
```css
`position: relative;`
```

|Result:|
|:---|
|![css-position-ex5](https://github.com/siriyaoff/MDN-note/blob/master/images/css-position-ex5.PNG?raw=true)|

- `<body>`에 relative positioning을 적용해서 `.positioned`의 containing block이 `<body>`로 변경됨

#### Introducing z-index
아래 CSS를 추가:  
```css
p:nth-of-type(1) {
  position: absolute;
  background: lime;
  top: 10px;
  right: 30px;
}
```

|Result:|
|:---|
|![css-position-ex6](https://github.com/siriyaoff/MDN-note/blob/master/images/css-position-ex6.PNG?raw=true)|

- 더 나중에 position된 `.positioned`가 더 앞으로 나옴
- `z-index` property를 사용해서 stack 순서를 바꿀 수 있음
	- 숫자가 높을수록 더 앞에 쌓임
	- default value : 0
	- unitless index value만 대입 가능

### Fixed positioning
Fixed positioning은 absolute와 동일하게 작동하지만, 기준이 다름
- 보통 viewport에 relative함
- ancestor 중에 `transform` property를 이용해서 회전하는 등의 조건을 충족하는 element가 있으면 그 element의 padding box에 relative함

#### Example
`p:nth-of-type(1)`, `.positioned` rule 지우고 아래 CSS를 추가:  
```css
body {
  width: 500px;
  height: 1400px;
  margin: 0 auto;
}

h1 {
  position: fixed;
  top: 0;
  width: 500px;
  margin-top: 0;
  background: white;
  padding: 10px;
}
```

|Result:|
|:---|
|![css-position-ex7](https://github.com/siriyaoff/MDN-note/blob/master/images/css-position-ex7.PNG?raw=true)|

- `<h1>`이 viewport 위쪽에 고정되지만, 첫 번째 `<p>`가 가려짐
	- fixed positioning도 element를 normal flow에서 제외시키기 때문
	- 첫 번째 `<p>`에 top margin을 줘서 해결

### Sticky positioning
relative와 fixed position을 혼합한 상태임  
=> 특정한 threshold(e.g. viewport의 top에서 10px)까지 스크롤 전에는 relatively positioned, 그 다음부터는 fixed

아래 CSS처럼 적용 가능함:  
```css
.positioned {
  position: sticky;
  top: 30px;
  left: 30px;
}
```

- `top`, `left` 등의 property로 threshold 정함(이 element가 threshold 위치에 도달하면 fixed로 바뀜)
- `<dt>`와 같은 element에 적용시켜서 엑셀의 틀고정과 같은 효과를 만들 수 있음

## Multiple-column layout
### A basic example
열 나누기는 `column-count`, `column-width` properties를 사용해서 구현함
- `column-count`
	- value : unitless
	- 지정한 값 만큼 column을 만듦(viewport를 변화시켜도 열 개수 일정)<br>e.g. `column-count: 3;`
- `column-width`
	- value : 길이 관련 unit들
	- grid에서 `grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));`를 사용하는 것과 비슷함<br>최소 width가 설정한 값이 되고, 나머지가 있으면 column끼리 분배함<br>e.g. `column-width: 200px;`

### Styling the columns
multicol로 생성된 columns는 개별로 styling할 수 없음  
i.e. 한 열만 넓게 하거나 배경을 바꾸는 등의 작업 불가

아래 properties를 사용해서 전체적인 styling 가능
- `column-gap` : 열 사이의 gap 설정
	- `20px`로 설정하면 열 사이에 간격은 `20px`임(`40px`가 아님)
- `column-rule` : 열 사이에 구분선 설정
	- `column-rule-color` `column-rule-style` `column-rule-width`의 shorthand property임
	- `border` property와 비슷하게 설정

#### Example
```css
.container {
  column-width: 200px;
  column-gap: 20px;
  column-rule: 4px dotted rgb(79, 185, 227);
}
```

|Result:|
|:---|
|![css-multicol-ex1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-multicol-ex1.PNG?raw=true)|

### Spanning columns
`column-span` property를 사용해서 element가 열들을 가로질러 span하게 만들 수 있음  
span하는 범위를 설정할 수 없음  
values available:
- `none` : default, span하지 않음
- `all` : 모든 열을 가로질러 span함

#### Example
![css-multicol-ex2](https://github.com/siriyaoff/MDN-note/blob/master/images/css-multicol-ex2.PNG?raw=true)

### Columns and fragmentation
multicol을 사용하면 content가 쪼개져서 columns에 들어가는데, 그 과정에서 아래와 같이 content의 가독성이 떨어질 수 있음  
![css-multicol-ex3](https://github.com/siriyaoff/MDN-note/blob/master/images/css-multicol-ex3.PNG?raw=true)

이런 현상을 `break-inside: avoid;` declaration을 사용해서 없앨 수 있음  
`break-inside` property를 적용하면 내부 content의 break를 제어함  
=> 끊기지 않아야 할 content가 들어있는 container에 적용해야 함

older version인 `page-break-inside`도 추가해서 browser support를 높일 수 있음

![css-multicol-ex4](https://github.com/siriyaoff/MDN-note/blob/master/images/css-multicol-ex4.PNG?raw=true)
- content가 잘리지 않은 채 layout됨

### Test your skills
- `column-gap`은 `column-rule`의 두께까지 고려해서 계산해야 함(rule이 `5px`이고 rule과 column 사이 공간을 `10px`로 설정하고 싶다면 gap을 `25px`로 줘야함
- `::before`, `::after` 등의 pseudo-element를 선언하고 `border-bottom` property를 이용해서 글자를 둘러싸는 선을 만들 수 있음<br>![css-multicol-ex5](https://github.com/siriyaoff/MDN-note/blob/master/images/css-multicol-ex5.PNG?raw=true)

## Responsive design
screen의 크기가 다양해지면서 하나의 layout으로는 모든 screen을 지원할 수 없게 됨  
스크린의 너비, 해상도 등에 따라 layout을 결정하는 *Responsive Web Design*(RWD)가 나타남

### Historic website layouts
예전에는 website를 설계할 때 두 가지 선택지가 있었음
- *liquid* site, browser window에 따라서 늘리거나 줄일 수 있음
- *fixed width* site, 사이즈가 완전히 고정됨

좁은 스크린에서 liquid site는 가독성이 떨어지고, fixed width site는 가로로 스크롤바가 생김  
fixed width site는 너무 넓은 스크린에서는 너무 많은 여백이 생김

mobile web이 상용화되면서 다른 URL(*m.asdf.com* 같은)을 이용하는 페이지들이 많아짐  
=> 두 가지 버전을 계속 관리해야 했음  
(+ 모바일 기기가 성능이 좋아지면서 데스크탑 버전에서 지원되는 기능을 모바일에서 사용하지 못하는 것에 불만이 생김)

### Flexible layout before responsive design
- Resolution dependent layout, 2004, Cameron Adams
	- 화면 해상도를 알아내기 위해 JavaScript를 필요로 했고, 알맞은 CSS가 요구되었음
- Designing CSS Layouts for the Flexible Web, 2008, Zoe Mickley Gillenwater
	- liquid와 fixed 사이의 flexible site를 개발하기 위한 방법들 공식화

### Responsive design
The term *Responsive design* was coined by Ethan Marcotte in 2010 and described the use of three techniques in combination
1. the idea of fluid grids
	- grid의 너비에 `%` 사용
2. the idea of fluid images
	- `max-width: 100%;`를 적용시켜서 구현
	- containing column에 따라서 크기가 맞춰지지만, 이미지가 커질 경우 pixelate됨
3. media query
	- screen size에 따라 layout을 다르게 적용(Cameron Adams는 JS를 필요로 했지만 media query는 CSS만 필요)

=> Responsive web design은 별도의 기술이 아님  
디바이스에 *respond*할 수 있는 layout을 만드는데 사용되는 web design 또는 그 결과물들로의 접근법을 나타냄  
(it is a term used to describe an approach to web design or a set of best practices, used to create a layout that can respond to the device being used to view the content)  
Marcotte의 정의는 flexible grids(using floats) + media queries였음  

10년 후인 지금은 기본적으로 responsive 개념이 사용됨  
Modern CSS layout methods are inherently responsive

### Media Queries
반응형 디자인은 media query 덕분에 구현될 수 있었음  
Media Queries는 user's screen에 관한 조건에 따라서 CSS를 선택적으로 적용할 수 있게 해줌

#### Example
```css
@media screen and (min-width: 800px) {
  .container {
    margin: 1em 2em;
  }
}
```
- 위 media query는 page를 표시하는게 screen이고, viewport가 `800px` 이상일 경우에만 `.container` rule을 적용함
- media query가 선언되고 layout이 바뀌는 지점을 breakpoint라고 함
- common approach using media queries
	- single-column layout for narrow screen devices
	- multi-column layout for larger screens
	
	위와 같은 디자인은 **mobile first** design이라고 불림

### Flexible grids
Responsive sites는 breakpoints에 따라서 layout이 바뀌는 것뿐만 아니라 flexible grids 안에 설계됨  
Flexible grid를 사용하면 breakpoint를 설정하고 breakpoint마다 적절하게 design을 바꾸면 됨  
grid라는 단어를 쓰지만 CSS Grid를 사용하는게 아니라 media query, `float`를 이용해서 grid를 만듦

초기 responsive design에서는 float만 사용해서 layout을 구성함  
elements에게 percentage width(`target / context * 100%`)를 부여해서 flexible floated layout을 구현  
(100%를 넘지 않도록 유의해야 함)

현재까지도 이런 방식을 사용하는 websites가 많음

### Modern layout technologies
Modern layout methods such as Multiple-column layout, Flexbox, and Grid are responsive by default. They all assume that you are trying to create a flexible grid and give you easier ways to do so.

#### Multicol
The oldest of these layout methods

#### Flexbox
#### CSS grid
`fr` unit allows the distribution of available space across grid tracks

flexbox는 열마다 flex를 이용해서 너비를 분배해야 하지만 grid는 container에서 너비를 분배하기 때문에 더 간단함

### Responsive images
The simplest approach to responsive images was as described in Marcotte's early articles on responsive design.  
기본적으로 가장 큰 해상도의 이미지를 구하고 줄여나가기 때문에 아래 rule을 통해 responsive image를 구현할 수 있음(아직까지 사용함)

```css
img {
  max-width: 100%;
}
```

이 approach의 단점
- 이미지가 원래 크기보다 많이 축소될 수 있고, 이는 네트워크 낭비로 이어짐
- scaling만 가능하기 때문에 screen에 따라서 이미지가 달라지거나 aspect ratio를 바꿀 수 없음

`<img>`의 `srcset`, `sizes` attributes를 이용한 approach로 위 단점을 보완 가능함  
srcset, sizes로 media query 같은 효과를 낼 수 있음 + srcset으로 화질이 다른 원본들을 지정해 pixelate되는 것도 어느 정도 해소됨

*art direct* image로도 해결 가능  
`<picture>`, `<source>`를 이용하면 viewport width 별로 사진을 다르게 설정 가능(art collection)

### Responsive typography
화면에 따라서 글자 크기를 조절하는 것  
media query를 이용

#### Example
```css
h1 {
  font-size: 2rem;
}

@media (min-width: 1200px) {
  h1 {
    font-size: 4rem;
  }
}
```

- media query를 이용해서 page layout 뿐만 아니라 가독성을 높이기 위해 다른 것들도 바꿀 수 있음

#### Using viewport units for responsive typography
viewport unit `vw`를 responsive typography에 사용할 수 있음  
`1vw` = 1% of viewport width  
=> 항상 viewport의 크기에 영향을 받기 때문에 `vw`로 글자 크기를 지정하면 안됨  
(∵ page zoom을 해도 글자 크기가 항상 똑같아짐)

`calc()` function을 사용해서 화면 크기에 비례하는 글자 크기를 지정하는게 좋음!  
e.g. `font-size: calc(1.5rem + 3vw);`

이런 식으로 글자 크기를 지정하면 위와 같이 media query를 쓰는 번거로움을 줄일 수 있음

### The viewport meta tag
```html
<meta name="viewport" content="width=device-width,initial-scale=1">
```

위 meta tag는 mobile browser일 때
- viewport width를 device width로 설정하고
- document scale을 100%로 맞춰서

모바일에 최적화되게 webpage를 보여주기 위한 것임  
∵ 초기에 아이폰이 출시되었을 때 모바일 버전을 지원하지 않는 웹사이트가 많아서 viewport width를 960px 등으로 속여서 사이트를 받고 렌더링을 한 다음 축소된 버전을 보여줌

이런 이유로 media queries가 mobile browser에서는 의도한 대로 작동하지 않을 수 있기 때문에,  
`<meta>` tag로 viewport width를 알아내고 알맞게 layout된 페이지를 로드하게 함  
따라서 항상 `<head>` 안에 `<meta>` tag를 넣어야 함!

보통 위의 태그를 많이 사용하지만 다른 options도 존재함:
- `initial-scale` : Sets the initial zoom of the page
- `height` : Sets a specific height for the viewport
- `minimum-scale` : Sets the minimum zoom level
- `maximum-scale` : Sets the maximum zoom level
- `user-scalable` : Prevents zooming if set to `no`

`minimum-scale`, `maxmum-scale`, `user-scalable: no;`의 사용에 주의해야함!  
(accessibility를 위해서)

> viewport meta tag를 대체하기 위해 `@viewport`라는 CSS @ rule이 설계되었지만, 현재는 잘 사용하지 않음

## Beginner's guide to media queries
### Media Query Basics
The simplest media query syntax:  
```css
@media media-type and (media-feature-rule) {
  /* CSS rules go here */
}
```

- `media-type` : 인쇄용, 스크린 등 어떤 용도로 사용되는지
- `media-feature-rule` : 아래 CSS를 적용하기 위해 만족해야 하는 조건

#### Media types
The possible types of media:
- `all` : default
- `print`
- `screen`
- `speech`

#### Example
```css
@media print {
    body {
        font-size: 12pt;
    }
}
```

- page가 인쇄될 때만 `body`의 글자 크기를 `12pt`로 설정함(브라우저에서 페이지가 로드될 때는 적용되지 않음)

#### Media feature rules
feature rules에 사용될 수 있는 media features:
- `width`, `min-width`, `max-width`
- `height`, `min-height`, `max-height`
- `orientation`<br>possible values:
	- `landscape` : landscape orientation, 모바일에서 가로모드, 데스크탑은 기본적으로 landscape임
	- `portrait` : 모바일에서 세로모드
- `hover`<br>possible values:
	- `hover` : 사용자가 pointing이 가능한 device를 사용하고 있음(touchscreen, keyboard navigation 등은 hover가 되지 않음)
	
	hovering이 불가능한 환경의 경우 interactive features를 기본으로 넣는 등의 설정이 가능  
	Level 4 specification이기 때문에 브라우저 지원을 잘 봐야함
- `pointer`<br>possible values:
	- `none` : no pointing device(or voice commands)
	- `fine` : mouse or trackpad, 사용자가 작은 영역을 잘 가리킬 수 있음
	- `coarse` : finger on a touchscreen
	
	사용자가 touchscreen을 사용하면 hit area를 더 늘리는 등의 개선이 가능함

### More complex media queries
#### "and" logic in media queries
Use `and`  
```css
@media screen and (min-width: 600px) and (orientation: landscape) {
    body {
        color: blue;
    }
}
```

#### "or" logic in media queries
Use `,`  
```css
@media screen and (min-width: 600px), screen and (orientation: landscape) {
    body {
        color: blue;
    }
}
```

- `,`로 구분된 쿼리들을 individual media query로 인식함

#### "not" logic in media queries
Use `not` operator  
entire media query를 부정함  
```css
@media not all and (orientation: landscape) {
    body {
        color: blue;
    }
}
```

- media type도 무조건 써야하기 때문에 not을 가장 먼저 붙임
- `,`로 구분될 경우 `not`이 붙어있는 query에만 영향을 줌

### How to choose breakpoints
현재는 screen의 종횡비와 해상도가 너무 다양하기 때문에 content가 깨지는 시점을 breakpoint로 잡는 게 좋음  
e.g. line-length가 너무 길어지거나 sidebar가 뭉개짐, 가독성이 떨어짐

따라서 device의 정확한 스펙에 관련 없이 모든 screen 범위에 대해 지정하면 됨  
media query가 구분되는 점을 breakpoints라고 함

Firefox DevTools에서는 viewport를 편리하게 조절할 수 있음  
![css-firefox-viewport](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Media_queries/rwd-mode.png)

### Active learning: mobile first responsive design
Two approaches to a responsive design:
- **start with the widest view, add breakpoints** as the viewport becomes smaller
- **start with the smallest view, add layout** as the viewport becomes larger

두 번째 접근법은 *mobile first responsive design*이라 불리는 자주 사용되는 접근 방식임

가장 작은 device에서의 layout은 주로 single column of content임  
=> small devices의 경우 많은 layout이 필요하지 않음  

#### Walkthrough: a simple mobile-first layout
아래 코드를 예제로 사용:  
HTML:  
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Media Queries: a simple mobile first design, step 1</title>
    <meta name="viewport" content="width=device-width">
    <link href="style.css" rel="stylesheet" type="text/css">
  </head>

  <body>
    <div class="wrapper">
      <header>
        <nav>
          <ul>
            <li><a href="">About</a></li>
            <li><a href="">Contact</a></li>
            <li><a href="">Meet the team</a></li>
            <li><a href="">Blog</a></li>
          </ul>
        </nav>
      </header>
      <main>
        <article>
          <div class="content">
            <h1>Veggies!</h1>
            <p>
              Veggies es bonus vobis, proinde vos postulo essum magis kohlrabi
              welsh onion daikon amaranth tatsoi tomatillo melon azuki bean
              garlic.
            </p>

            <p>
              Gumbo beet greens corn soko endive gumbo gourd. Parsley shallot
              courgette tatsoi pea sprouts fava bean collard greens dandelion
              okra wakame tomato. Dandelion cucumber earthnut pea peanut soko
              zucchini.
            </p>

            <p>
              Turnip greens yarrow ricebean rutabaga endive cauliflower sea
              lettuce kohlrabi amaranth water spinach avocado daikon napa
              cabbage asparagus winter purslane kale. Celery potato scallion
              desert raisin horseradish spinach carrot soko. Lotus root water
              spinach fennel kombu maize bamboo shoot green bean swiss chard
              seakale pumpkin onion chickpea gram corn pea. Brussels sprout
              coriander water chestnut gourd swiss chard wakame kohlrabi
              beetroot carrot watercress. Corn amaranth salsify bunya nuts nori
              azuki bean chickweed potato bell pepper artichoke.
            </p>

            <p>
              Nori grape silver beet broccoli kombu beet greens fava bean potato
              quandong celery. Bunya nuts black-eyed pea prairie turnip leek
              lentil turnip greens parsnip. Sea lettuce lettuce water chestnut
              eggplant winter purslane fennel azuki bean earthnut pea sierra
              leone bologi leek soko chicory celtuce parsley jícama salsify.
            </p>
          </div>
          <aside class="related">
            <p>
              All these veggies are brought to you by the
              <a href="https://veggieipsum.com/">Veggie Ipsum generator</a>.
            </p>
          </aside>
        </article>

        <aside class="sidebar">
          <h2>External vegetable-based links</h2>
          <ul>
            <li>
              <a
                href="https://www.thekitchn.com/how-to-cook-broccoli-5-ways-167323"
                >How to cook broccoli</a
              >
            </li>
            <li>
              <a href="https://www.bbcgoodfood.com/glossary/swiss-chard"
                >Swiss Chard</a
              >
            </li>
            <li>
              <a
                href="https://www.bbcgoodfood.com/recipes/collection/christmas-parsnip"
                >Christmas Parsnip Recipes</a
              >
            </li>
          </ul>
        </aside>
      </main>

      <footer><p>&copy;2019</p></footer>
    </div>
  </body>
</html>
```

CSS:  
```css
* {
  box-sizing: border-box;
}

body {
  width: 90%;
  margin: 2em auto;
  font: 1em/1.3 Arial, Helvetica, sans-serif;
}

a:link,
a:visited {
  color: #333;
}

nav ul,
aside ul {
  list-style: none;
  padding: 0;
}

nav a:link,
nav a:visited {
  background-color: rgba(207, 232, 220, 0.2);
  border: 2px solid rgb(79, 185, 227);
  text-decoration: none;
  display: block;
  padding: 10px;
  color: #333;
  font-weight: bold;
}

nav a:hover {
  background-color: rgba(207, 232, 220, 0.7);
}

.related {
  background-color: rgba(79, 185, 227, 0.3);
  border: 1px solid rgb(79, 185, 227);
  padding: 10px;
}

.sidebar {
  background-color: rgba(207, 232, 220, 0.5);
  padding: 10px;
}

article {
  margin-bottom: 1em;
}
```

|Result:|
|:---|
|![css-responsive-ex1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-responsive-ex1.PNG?raw=true)|

- 페이지의 가독성을 높이는 순서로 소스를 작성해야 함

아래 CSS를 추가:  
```css
@media screen and (min-width: 40em) {
    article {
        display: grid;
        grid-template-columns: 3fr 1fr;
        column-gap: 20px;
    }

    nav ul {
        display: flex;
    }

    nav li {
        flex: 1;
    }
}
```

|Result:|
|:---|
|![css-responsive-ex2](https://github.com/siriyaoff/MDN-note/blob/master/images/css-responsive-ex2.PNG?raw=true)|

- media query를 `em`으로 설정해서, 같은 width라도 글자 크기에 따라서 적용되는 layout이 다르도록 만듦

아래 CSS를 추가:  
```css
@media screen and (min-width: 70em) {
    main {
        display: grid;
        grid-template-columns: 3fr 1fr;
        column-gap: 20px;
    }

    article {
        margin-bottom: 0;
    }

    footer {
        border-top: 1px solid #ccc;
        margin-top: 2em;
    }
}
```

|Result:|
|:---|
|![css-responsive-ex3](https://github.com/siriyaoff/MDN-note/blob/master/images/css-responsive-ex3.PNG?raw=true)|

- 위의 `min-width: 40em`에서는 `<article>`에 grid를 사용해서 main content, related만 묶었지만, 이 media query에서는 `<main>`에 grid를 사용해서 `<article>`의 grid와 sidebar를 묶었음<br>즉, grid(grid(3fr, 1fr), 1fr)으로 이루어짐
- `article`에 `margin-bottom:0;`을 적용하는 이유 : main의 grid에 article의 grid를 nesting하는 형식인데, article에 margin-bottom이 있으면 sidebar와 article의 높이가 달라지기 때문
- `footer`에 `border-top`을 추가해서 `footer`를 확실하게 구분함

### Do you really need a media query?
Flexbox, Grid, and multi-column layout은 media query 없이도 responsive components를 생성함  
따라서 가능하면 media query 대신 이런 layout methods를 사용하는 것이 나음  
예를 들어, width에 따라 column 개수를 추가하고 싶으면 CSS Grid와

`grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));`

를 사용하면 됨

### Test your skills
media query부분만:  
```css
@media screen and (min-width: 40em) {
  header {
    display: flex;
    margin-bottom: 1em;
    justify-content: space-between;
    align-items: center;
  }

  header ul {
    display: flex;
  }

  header a {
    border-top: none;
  }

  main {
    display: grid;
    grid-template-columns: 3fr 1fr;
    column-gap: 1em;
  }

  .cards {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(18em, 1fr));
    grid-gap: 1em;
  }
}
```

|Result:|
|:---|
|![css-responsive-ex4](https://github.com/siriyaoff/MDN-note/blob/master/images/css-responsive-ex4.PNG?raw=true)|

- `.cards`도 flex로 해보려 했는데 좌우 여백 때문에 그냥 grid 사용함(flex도 여러 행일 때 flex item의 `width`를 지정하면 모든 item들의 너비를 같게 할 수 있음)
- **좌우로는 margin-collapsing이 일어나지 않음!!**
- `html`에 대해서 `font-size: calc(1em+1vw);`를 적용했는데 글자 크기에 큰 차이가 없었음

## Legacy layout methods
### Layout and grid systems before CSS Grid Layout
이 article에서는 float, flexbox를 사용해서 grid systems, grid framworks를 만드는 legacy methods를 다룸  
fallback code나 이미 legacy methods를 사용하는 projects를 할 때 도움됨

아래 방법들로 grid를 비슷하게 만들 수는 있지만, CSS Grid Layout이 grid를 만드는 방법과는 같지 않음  
(대부분 items에 크기를 부여하고 줄에 맞춰 배치해서 grid처럼 보이게 하는 방법을 사용함)

### A two column layout
HTML `<body>` 부분:  
```html
<h1>2 column layout example</h1>
<div>
  <h2>First column</h2>
  <p> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla luctus aliquam dolor, eu lacinia lorem placerat vulputate. Duis felis orci, pulvinar id metus ut, rutrum luctus orci. Cras porttitor imperdiet nunc, at ultricies tellus laoreet sit amet. Sed auctor cursus massa at porta. Integer ligula ipsum, tristique sit amet orci vel, viverra egestas ligula. Curabitur vehicula tellus neque, ac ornare ex malesuada et. In vitae convallis lacus. Aliquam erat volutpat. Suspendisse ac imperdiet turpis. Aenean finibus sollicitudin eros pharetra congue. Duis ornare egestas augue ut luctus. Proin blandit quam nec lacus varius commodo et a urna. Ut id ornare felis, eget fermentum sapien.</p>
</div>

<div>
  <h2>Second column</h2>
  <p>Nam vulputate diam nec tempor bibendum. Donec luctus augue eget malesuada ultrices. Phasellus turpis est, posuere sit amet dapibus ut, facilisis sed est. Nam id risus quis ante semper consectetur eget aliquam lorem. Vivamus tristique elit dolor, sed pretium metus suscipit vel. Mauris ultricies lectus sed lobortis finibus. Vivamus eu urna eget velit cursus viverra quis vestibulum sem. Aliquam tincidunt eget purus in interdum. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.</p>
</div>
```

- column을 만들기 위해 outer element가 필요함<br>=> `<div>`, `<article>`, `<section>`, `<aside>` 등 semantically appropriate elements를 이용

CSS:  
```css
body {
  width: 90%;
  max-width: 900px;
  margin: 0 auto;
}

div:nth-of-type(1) {
  width: 48%;
  float: left;
}

div:nth-of-type(2) {
  width: 48%;
  float: right;
}
```

- `body`에 `margin: 0 auto;`를 적용해서 항상 가운데로 오도록 조절
- `nth-of-type()` pseudo-class를 이용해서 너비 지정 후 각각 왼쪽, 오른쪽에 float시킴
- 둘 다 `width: 48%;`로 설정해서 나머지 `4%`는 grid의 gutter처럼 이용함

|Result:|
|:---|
|![css-legacy-ex1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-legacy-ex1.PNG?raw=true)|

- width를 설정할 때 모두 percentage를 사용함<br>=>**liquid layout**(화면 크기가 달라져도 열 너비들이 같은 비율을 유지)<br>=>valuable tool for responsive web design

### Creating simple legacy grid frameworks
`float` property의 특징을 이용한 방법이 주요한 legacy framework임  
(여러 item을 float하면 margin으로 간격이 띄워지기 때문에 grid처럼 보임)  
보통 12 column grid를 많이 사용함(약수가 많기 때문)

#### A simple fixed width grid
HTML의 `<body>` 부분:  
```html
<div class="wrapper">
  <div class="row">
    <div class="col">1</div>
    <div class="col">2</div>
    <div class="col">3</div>
    <div class="col">4</div>
    <div class="col">5</div>
    <div class="col">6</div>
    <div class="col">7</div>
    <div class="col">8</div>
    <div class="col">9</div>
    <div class="col">10</div>
    <div class="col">11</div>
    <div class="col">12</div>
  </div>
  <div class="row">
    <div class="col span1">13</div>
    <div class="col span6">14</div>
    <div class="col span3">15</div>
    <div class="col span2">16</div>
  </div>
</div>
```

CSS:  
```css
* {
  box-sizing: border-box;
}

body {
  width: 980px;
  margin: 0 auto;
}

.wrapper {
  padding-right: 20px;
}

.row {
  clear: both;
}

.col {
  float: left;
  margin-left: 20px;
  width: 60px;
  background: rgb(255, 150, 150);
}

/* Two column widths (120px) plus one gutter width (20px) */
.col.span2 { width: 140px; }
/* Three column widths (180px) plus two gutter widths (40px) */
.col.span3 { width: 220px; }
/* And so on... */
.col.span4 { width: 300px; }
.col.span5 { width: 380px; }
.col.span6 { width: 460px; }
.col.span7 { width: 540px; }
.col.span8 { width: 620px; }
.col.span9 { width: 700px; }
.col.span10 { width: 780px; }
.col.span11 { width: 860px; }
.col.span12 { width: 940px; }
```

|Result:|
|:---|
|![css-legacy-fixed-grid](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Legacy_Layout_Methods/simple-grid-finished.png)|

- `body`의 `980px` 중 `20px`는 `.wrapper`의 `padding-right`로 사용됨
- `.row`로 줄을 바꿔야 하기 때문에 `clear: both;`를 사용해서 다른 float와 간섭하지 않게 만듦
- `.col`으로 grid의 cell 하나하나를 만듦
	- `float`를 이용(`clear` property를 사용하면 행을 바꾸기 편리함)
	- `margin-left: 20px;`로 gutter 설정(`.wrapper`에서 설정한 `padding-right: 20px;`가 있기 때문에 `margin-left`를 사용)
	- `(980-20-12*20)/12=60px`을 열의 너비로 설정
- span하는 layout container을 위해 `.span` 클래스를 정의했음
	- span하는 열 개수에 따라 필요한 너비를 계산해서 overriding함

#### Creating a fluid grid
위의 경우 너비가 고정되어 있어 호환성이 떨어짐  
=> width를 모두 percentages로 설정해서 flexible(fluid) grid를 만들 수 있음

`target / context = result`  
=> `60 / 960 = 0.0625`이므로 `.col`의 width를 `6.25%`로 설정하면 됨

**Updating our grid**  
```css
body {
  width: 90%;
  max-width: 980px;
  margin: 0 auto;
}
```

- `body` rule을 fluid하게 만들기 위해서 `width: 90%;`로 설정하고 최대 너비에 제한을 둠
- `margin`, `padding`, `width` 등의 properties도 percentage로 바꿔주면 됨

#### Easier calculations using the calc() function
`.col.span4`와 같은 rule에서 아래와 같이 사용 가능함  
`width: calc((6.25%*4) + (2.08333333%*3));`

※ IE9 이전에서는 `calc()` 함수가 지원되지 않음

#### Semantic versus "unsemantic" grid systems
위와 같이 layout을 구성하기 위한 클래스 사용으로 content와 markup이 묶이는 것을 CSS class의 unsemantic use라고 함

#### Enabling offset containers in our grid
```css
.offset-by-one {
  margin-left: calc(6.25% + (2.08333333%*2));
}
```

- 위와 같은 class를 선언해서 offset으로 사용할 수 있음(위의 `.offset-by-one`은 왼쪽에 빈 칸을 하나 만드는 것)<br>`<div class="col span5 offset-by-one">14</div>`와 같이 사용 가능

#### Floated grid limitations
float를 이용해서 grid을 만들 때는 아래와 같은 경우를 조심해야 함
- total width가 정확히 계산되었는지
- 가능한 col보다 더 span하는 element를 포함시키지 않았는지(overflow되어버림)
- 한 행에 너무 많은 grid columns를 포함시키면 자동으로 다음줄로 내려가서 grid가 망가짐
- 기본적으로 1차원이기 때문에 세로로 span하는 element를 만들 수 없음
	- older layout methods를 사용하면 정확히 height를 설정하는 방법 이외에는 height를 조절하는게 어려움<br>따라서 content가 특정한 높이라고 보장이 될 때만 inflexible한 grid를 만들 수 있음

### Flexbox grids?
Flexbox-based grid systems도 물론 가능하지만, flexbox 자체가 grid를 위해서 설계되지 않았고 이걸 이용해서 grid를 설계하면 새로운 문제들이 생김  
- flexbox는 항상 items가 container을 가득 채우므로 처음 정한 최대 개수의 col을 사용하지 않으면 남는 부분은 다른 col들에게 자동으로 분배됨
	- 따라서 `.col`안에 `span` classes가 필요함(width를 overriding하기 위해)
- flexbox는 one-dimensional이기 때문에 floated grid처럼 percentages를 계산해서 넣어줘야 함(gap 등을 고려해서)

### Third party grid systems
Bootstrap, Foundation 등이 grid system을 포함한 유명한 frameworks임  
Skeleton을 예로 들면, Skeleton website에서 다운받은 css 파일들을 링크한 후 이미 정의되어있는 classes(`container`, `row`, `one column`, `three columns`, ...)을 사용하는 것임

요즘은 이런 frameworks를 사용하기보다 CSS grid를 사용하는 추세임

## Supporting older browsers
This article explains how to use modern web techniques without locking out users of older technology.

### What is the browser landscape for your site?
webpage의 layout 설계에 대한 접근법을 결정하기 전에, target audience에 대한 조사가 먼저 이행되어야 함  
Statcounter와 같은 사이트에서 location에 따른 사용자들의 분류를 제공해줌  
유저들이 사용하는 browser와 같은 기술적인 측면에서도 분석이 필요함  
(mobile, older browser, accessibility 등)

### What is the support for the features you want to use?
site를 방문하는 browser를 알면 어떤 기술에 대해서도 지원 여부, 대안 제공 가능성 등을 쉽게 알 수 있음  
(MDN browser compatibility, Can I Use 등)

### Support doesn't mean "looks the same"
website가 모든 browsers(phone, desktop, screen reader 등)에서 같을 수는 없음  
모두 지원한다는 것의 의미는 최신 browser에서 잘 보이고 older browsers에서도 기본적으로 사용할 수 있는 content를 제공한다는 것임

basic level of support는 normal flow에서도 content가 의미를 가지는 것을 뜻함  
이걸 위해선 HTML document부터 잘 만들어야 함

아예 plain view를 fallback으로 놔두는 방법도 있음  
fallback을 modern browser에서와 비슷하게 만들기보다 사이트를 더 accessible하게 만들어 많은 유저들을 끌어들이는게 이득임  
CSS에서 fallback 생성을 쉽게 하도록 만들어놓음

### Creating fallbacks in CSS
CSS specifications에는 두 가지 layout methods가 겹쳤을 때 처리 방법도 정의되어 있음  
예를 들어 float가 적용되어 있으면서 CSS Grid item인 element는, CSS Grid가 지원되지 않는 browsers에서는 float가 적용되고, CSS Grid가 지원되면 Grid item으로 처리됨  
즉, CSS Grid가 지원되지 않는 브라우저는 `display: grid`와, 관련된 properties들을 다 무시하기 때문에 float가 적용됨  
float와 관련된 `clear` property는 적용된 item이 grid item이 되면 효과가 없어짐

#### Fallback Methods
**`float` and `clear`**
- `float`와 `clear` properties는 만약 적용된 item이 flex or grid item이 될 경우 효과가 없어짐

**`display: inline-block;`**
- column layout을 구성할 때 사용될 수 있음
- 적용된 item이 flex or grid item이 되면 마찬가지로 inline-block으로 취급되지 않음

**`display: table;`**
- fallback으로 사용될 수 있음
- 적용된 item이 flex or grid item이 될 경우 효과가 없어짐
- 적용되지 않으면 table structure을 위해 생성되던 box들도 다 사라짐

**Multiple-column Layout**
- multi-col(`column-count`, `column-width`)을 fallback으로 사용할 수 있음
- 적용된 item이 grid container가 되면 `column-*` properties는 적용되지 않음

**Flexbox as a Fallback for Grid**
- flexbox가 CSS Grid보다 지원이 잘 되기 때문에 flexbox를 fallback으로 이용할 수 있음
- flex container를 grid container으로 사용할 경우 flex items에게 적용되던 `flex` property는 적용되지 않음

simpler layout based on older and well-supported techniques를 적용한 다음, 대부분의 사용자를 위해 newer CSS를 적용하는 것이 나음  
하지만, 저렇게 서로 간섭을 막을 수 없는 경우도 존재함

#### Example
percentage widths를 floated item에 적용해서 grid처럼 보이게 했을 때임

HTML:  
```html
<div class="wrapper">
  <div class="item">Item One</div>
  <div class="item">Item Two</div>
  <div class="item">Item Three</div>
</div>
```

CSS:  
```css
* {box-sizing: border-box;}

.wrapper {
  background-color: rgb(79,185,227);
  padding: 10px;
  max-width: 400px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}

.item {
  float: left;
  border-radius: 5px;
  background-color: rgb(207,232,220);
  padding: 1em;
  width: 33.333%;
}
```

|Result:|
|:---|
|![css-feature-query-ex1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-feature-query-ex1.PNG?raw=true)|

- floated layout에서 percentage는 container으로부터 계산됨
- Grid에서는 item이 속한 grid area로부터 계산됨<br>=>fallback으로 사용하는 float의 width 설정이 grid가 지원되는 browser에서도 영향을 미쳐 width가 제대로 나오지 않음

### Feature queries
feature queries를 이용해서 browser가 특정한 CSS feature를 지원하는지 테스트할 수 있음  
=> 위에서의 percentage width같은 문제를 해결할 수 있음

#### Example
위 예제에서 아래 feature query만 추가:  
```css
@supports (display: grid) {
  .item {
      width: auto;
  }
}
```

|Result:|
|:---|
|![css-feature-query-ex2](https://github.com/siriyaoff/MDN-note/blob/master/images/css-feature-query-ex2.PNG?raw=true)|

- CSS Grid를 지원하면 `.item`에 `width: auto;`<br>=> width가 제대로 나옴

> ※ CSS Grid를 지원하지 않는 browsers는 feature queries도 지원하지 않음!!  
> 따라서 위에서 설명한 old CSS로 fallback을 만들고 그 위에서 최신 CSS를 사용하는 접근법은 그대로 사용해야 함  
> feature query의 용도는, fallback에서 선언했지만, grid에도 영향을 미치는 rule들을 수정해서 grid가 올바르게 출력되도록 만드는 것임

### Older versions of Flexbox
`-ms-` prefix를 사용하는 IE10과 같은 경우에서 flexbox 지원은 [여기](https://css-tricks.com/old-flexbox-and-new-flexbox/) 참고

### The IE10 and 11 prefixed version of Grid
IE10, 11은 `-ms-` prefix가 붙은 grid를 사용  
얘네는 non-Microsoft browsers에서는 호환되지 않음(CSS Grid와는 다름)  
[Progressive Enhancement in Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/CSS_Grid_and_Progressive_Enhancement)에서 IE버전 grid에 대한 설명을 볼 수 있지만, older IE를 사용하는 유저가 많지 않으면 fallback을 만드는게 더 나음

### Testing older browsers
현재는 대부분의 browser가 flexbox, grid를 지원하기 때문에 older browser 환경을 구하는게 어려울 수도 있음  
Sauce Labs같은 online testing tool을 이용하거나 VM([MS에서도 제공](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/), available for Mac, Windows, Linux)을 설치해서 테스트할 수 있음

## Assessment10-Fundamental-layout-comprehension
|Result:|
|:---|
|![css-layout-assmt](https://github.com/siriyaoff/MDN-note/blob/master/images/css-layout-assmt.PNG?raw=true)|

1. navigation을 한 줄로 표시
	- `display: flex;` 적용
2. navigation에 sticky 속성 부여
	- `position: sticky;` 적용
3. 이미지 float
	- `float: left;` 적용
	- margin 부여해서 text 사이에 여백 만듦
4. `<article>`, `<aside>`를 flexible한 2열 layout으로 구성
	- `display: grid;` 적용
	- `<p>`에 padding을 넣는 것 보다 grid gap으로 여백을 주는게 나음
5. `<aside>`의 사진들을 2열 grid, gap을 1px로 설정
	- `display; grid;` 적용

- 추가로 `<body>`에 responsive typography 적용<br>`font: calc(1rem + 0.2vw) / 1.2 Arial, Helvetica, sans-serif;`