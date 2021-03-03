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
> Let's use: Cascading Style Sheets

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
**Example**  
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

Result:  
![Inheritance ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-inheritance-ex1.PNG?raw=true)
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

**Example**  
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

Result:  
![universal property ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-universal-property-ex1.PNG?raw=true)
- `a { color: red;}`를 추가하면 맨 위 링크만 빨간색으로 변함(다른 것들은 `' '` combinator, class selector로 specificity가 더 높은 rule이 적용되어있기 때문)

#### Resetting all property values
The CSS shorthand property `all` represents all properties. So we can use it usefully when we debug. If we apply `all: unset;` declaration, all rules applied will be initialized except the inherited properties.

**Example**
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

Result:  
![all property ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-all-property-ex1.PNG?raw=true)
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
1. **Thousands** : 1 if declaration is inside a `sylte` attribute(= **inline styles**) -> No selectors, so always specificity=1000
2. **Hundreds** : 1 for each **ID selector** contained inside the overall selector
3. **Tens** : 1 for each **class selector**, **attribute selector**, or **pseudo-class** contained inside the overall selector
4. **Ones** : 1 for each **element selector** or **pseudo-element** contained inside the overall selector

**Note**: The universal selector(`*`), combinators(`+`, `>`, `~`, `' '`), and negation pseudo-class(`:not`) have no effect on specificity

**Example**  
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

**Example**  
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

Result:  
![css important ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-important-ex1.PNG?raw=true)

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

**Example**  
```css
.box::before {
  content: "This should show before the other content.";
}
```
- `.box` 클래스가 적용된 element 전에 `content`의 property value가 표시됨
- ""을 `content`의 value로 넣고 `display: block;`을 적용해서 도형같은걸 넣을 수도 있음
- 텍스트를 value로 넣어도 브라우저에서 그 텍스트 선택 불가(~~가끔 리스트 마커가 드래그되지 않을 때가 있었는데 이렇게 추가한듯~~ 리스트 마커는 `li`의 `list-style-type`으로 조정!)

### Combinators
The combinators combine other selectors in order to target elements within our documents.

#### Descendant combinator
The descendant combinator(`' '`) combines two selectors(`A B`) such that `B` is selected if `B` has `A` as its ancestor.  
Selectors that utilize a descendant combinator are called *descendant selectors*.

**Example**  
`body article p` selects `<p>` inside `<article>` which is inside `<body>`.

#### Child combinator
The child combinator(`>`) combines two selectors(`A < B`) such that `B` is selected if `B` is a direct children of `A`.  
Descendant elements further down don't match.  
The following selects paragraphs that are direct children of `<article>` elements using the child combinator(`>`):  
```css

article > p {}

```  
※ Descendant combinator `' '` selects all the descendants while child combinator(`>`) selects direct children.

#### Adjacent sibling combinator
The adjacent sibling selector(+) is placed between two CSS selectors(`A + B`). It matches only those elements matched by the `B` that are the next sibling element of the `A`.  
A common use case is to do something with a paragraph that follows a heading, such as *abstract*.

**Example**  
`h1 + p` selects paragraphs after `<h1>`

#### General sibling combinator
The general sibling combinator(`~`) combines two selectors(`A ~ B`). It selects all the B that are siblings of A, even not directly adjacent.

**Example**  
`p ~ img` selects all `<img>` elements that come anywhere **after** `<p>` elements.

#### Using combinators
> Take care however when creating big lists of selectors that select very specific parts of your document. It will be hard to reuse the CSS rules as you have made the selector very specific to the location of that element in the markup.
>
> It is often better to create a simple class and apply that to the element in question. That said, your knowledge of combinators will come in very useful if you need to get to something in your document and are unable to access the HTML, perhaps due to it being generated by a CMS.

## The box model
### Block and inline boxes
In CSS, there are broadly two types of boxes - **block boxes** and **inline boxes**. These characteristics refer to how the box behaves in terms of page flow, and in relation to other boxes on the page:

**Block box**
- The box will break onto a new line.
- The box will extend in the inline direction to fill the space available in its container.
- The `width` and `height` properties are respected.
- Padding, margin and border will cause other elements to be pushed away from the box.

By default, headings and `<p>` use `block` as their outer display type.

**Inline box**
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

Result:  
![display type ex1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-display-type-ex1.png?raw=true)

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

Result:  
![display type ex2](https://github.com/siriyaoff/MDN-note/blob/master/images/css-display-type-ex2.png?raw=true)

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

**Example**  
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

Result:  
![standard box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model/standard-box-model.png)

The space taken up by the box using the standard box model will be 410px(350+25+25+5+5) * 210px(150+25+25+5+5).  
**Note**: The margin is not counted towards the actual size of the box. It affects only the space outside the box. The box's area stops at the border.(보여지는 박스의 크기는 border까지임)

#### The alternative CSS box model
In the alternative box model, `width` is the width of the visible box(width to the border). Therefore the content area width is `width` miuns the width for the padding and border.  

**Example**  
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

**Example**  
```css
border: 1px groove grey;
border-top: 1px double grey;
border-style: dashed ridge none dotted;
border-right-width: 2px;
border-bottom-color: blue;
```
- 방향이 포함된 properties에서는 모양을 shorthand로 사용할 수 있고, 모양이 포함될 경우 방향을 shorthand로 사용할 수 있음
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

**Example**  
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

Result:  
![inline box ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-inline-box-ex.png?raw=true)

### Using display: inline-block
`inline-block` is a middle ground between `inline` and `block`.
- The `width` and `height` properties are respected
- `padding`, `margin`, and `border` will cause other elements to be pushed away from the box  
=> avoid the overlapping like above, but inline

**Example**  
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

Result:  
![inline block ex](https://github.com/siriyaoff/MDN-note/blob/master/images/css-inline-block-ex.png?raw=true)
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

**Example**  
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

**Example**
```css
background-image: linear-gradient(105deg, rgba(0,249,255,1) 39%, rgba(51,56,57,1) 96%);

background-image: radial-gradient(circle, rgba(0,249,255,1) 39%, rgba(51,56,57,1) 96%);
background-size: 100px 100px;
```
- We can set the size of gradients with the `background-size`, and the gradients will be repeated by default.

#### Multiple background images
It is possible to have multiple background images in a single property value, by separating with commas.

**Example**  
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

**Example**  
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
**Example**  
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

Result:  
![text overflow ex1](https://github.com/siriyaoff/MDN-note/blob/master/images/css-text-overflow-ex1.png?raw=true)

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
	- `normal` : 긴 단어 보존, 원래 줄바꿈 보존, 다른 언어들은 box에 맞춤
	- `break-all` : 원래 줄바꿈 무시, 단어 길이 상관없이 box의 끝에 도달했을 때만 줄바꿈
	- `keep-all` : 오버플로우 상관없이 원래 텍스트 그대로 보존
	- `break-word` : 긴 단어 보존, 단어를 단위로 box에 맞춤
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
//https://webdesign.tutsplus.com/ko/articles/7-css-units-you-might-not-know-about--cms-22573
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