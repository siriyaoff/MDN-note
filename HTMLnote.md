# HTML Basics
- HTML : HyperText Markup Language

- UX : User eXperience

- Google search engine treats a hyphen as a word-separator but does not for an underscore.  
->파일 이름 구분은 -으로

- Basic structure of an website  
web-project -> test-site -> (`Index.html`, `/images`, `/styles`, `/scripts`)
	- `/styles` : CSS codes about text, bgcolor ...
	- `/scripts` : JavaScripts for interactive functions  
※ Windows에서는 path에 `\`를 사용하지만 html에서는 `/` 사용

- tags ∈ elements ∈ DOM(Document Object Model)

- Anatomy of an HTML element
![Anatomy of an HTML element](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics/grumpy-cat-small.png)
	- opening tag는 attribute를 포함할 수도 있음
	- Attribute rules
		- separator : `' '`
		- assignment : `=`
		- value format : `"VALUE"` or `'VALUE'`  
		->`att1="val1" att2="val2"`

- Nesting : to put elements inside other elements
	- `<p> My cat is <strong>very</strong> grumpy.</p>`

- Empty elements(=Void elements)
	- no closing tag, no inner content(does not wrap content to affect it)
	- `<img src="images/firefox-icon.png" alt="My test image">`
	- 정확하게는 child nodes(nested elements, text nodes...)를 가질 수 없는 elements들(closing tag가 없는 element임)

>  but they aren't handy on their own.

- Anatomy of an HTML document  
	```html
	<!DOCTYPE html>
	<html>
		<head>
			<meta charset="utf-8">
			<title>My test page</title>
		</head>
		<body>
			<img src="images/firefox-icon.png" alt="My test image">
		</body>
	</html>
	```
	- `<!DOCTYPE html>` : 파일의 HTML버전을 명시(HTML은 버전별로 지원하는 태그가 다르기 때문에 미리 HTML버전을 명시해서 브라우저가 올바르게 표시하게 만듦)
	- `<html></html>` : wraps all the content on the entire page
		- root element라고도 함
	- `<head></head>` : 브라우저가 표시하는 페이지에는 나타나지 않지만 넣어야 하는 것들(페이지 설명, CSS, keyword ...)을 보관하는 컨테이너
		- `<meta charset="utf-8">` : sets the character set(utf-8을 많이 사용)
		- `<title></title>` : sets the title of page
	- `<body></body>` : includes content shown to visitors
		- `<img src="images/firefox-icon.png" alt="My test image">` : src, alt attributes  
		※ "alt text = descriptive text"  
		-> The Firefox logo: a flaming fox surrounding the Earth.
	
- Essential elements
	- Headings
		- 6 heading levels, <h1>-<h6>
		- `<h1>Main title</h1>` : generally used once per page  
		※ SEO(search Engine Optimization) considers headings as keywords  
		-> Don't skip levels to expose my page
	- Paragraphs
		- `<p>Single paragraph</p>`
	- Lists
		- ordered/unordered lists(`<ol>` / `<ul>`) wrap list items
		- list items are put inside an `<li>`(list item) element
	- Links
		- attribute `href` : put address to link(**h**ypertext **ref**erence)  
		-> Don't omit protocol at the beginning
		- `<a href="https://www.mozilla.org/en-US/about/manifesto/">Mozilla Manifesto</a>`
		

# Introduction to HTML
## Getting started with HTML
- Semantic web : HTML의 버전이 높아지면서 headings, figcaption 등 의미를 가지는 elements가 많아졌는데 이런 것들을 적절하게 사용하는 것
	- SEO가 높아짐, crawler가 페이지 정보를 제대로 파악함
	- 접근성(Accessibility)이 높아짐

- Tags are case-insensitive

- Block-level vs. Inline elements
	- Block-level elements
		- have new line following/followed-by it
		- are usually structural elements on the page(paragraphs, navigation menus, footers ...)
		- wouldn't be nested inside an inline element
	- Inline elements
		- will not cause a new line to appear
		- surround only small parts of the document's content
		- typically used with text

- Boolean attributes
	- can have only one value, which is generally the same as the attribute name
	- `<input type="text" disabled="disabled">`  
	※ shorthand : `<input type="text" disabled>`  
	Always include attribute quotes!

- To use quote marks inside other quote marks of the same type, use HTML entities
	- `<a href='http://www.example.com' title='Isn&apos;t this fun?'>A link to my example.</a>`

- Whitespace in HTML
	- 연속된 공백이나 줄바꿈문자는 HTML parser에 의해 하나의 공백으로 바뀜  
	-> 코드의 Readability를 위해 whitespace 사용(Indentation ...)

- Special characters in HTML
	- `<`, `>`, `"`, `'`, `&` : Character entity 사용!
	
	| Literal character | Character reference equivalent |
	| :--- | :--- |
	| `<` | `&lt;` |
	| `>` | `&gt;` |
	| `"` | `&quot;` |
	| `'` | `&apos;` |
	| `&` | `&amp;` |
	
	- 나머지는 utf-8인코딩이면 그냥 사용해도됨

- Comment
	- `<!-- comment -->`

## Metadata in HTML(in `<head>`)
- `<title>` : metadata that represents the title of the overall HTML document(not the document's content == `<h1>`)

- `<meta>` : element adding metadata to a document
	- charset : `<meta charset="utf-8">`
	- name, content : name에 meta data type, content에 actual meta content 저장
		- meta data type : author, description, keywords ...
		- `<meta name="author" content="siriyaoff">`  
		`<meta name="keywords" content="fill, in, your, keywords, here">` - ignored by search engines because of spammers  
		※ Many `<meta>` features like keywords aren't used any more
	- Properietary creations
		- Open Graph Data(Facebook's)
			- `<meta property="og:image" content="Image address">`  
			- `<meta property="og:description" content="Description">`
			- `<meta property="og:title" content="Title">`
		- Twitter Cards(Twitter's)
			- `<meta name="twitter:title" content="Title">`

- `<link>`
	- favicon, CSS 등을 추가할 수 있음  
	`<link rel="shortcut icon" href="favicon.ico" type="image/x-icon">`  
	`<link rel="stylesheet" href="CSSfile.css">`
	- `rel` : 뒤에 나올 링크가 현재 페이지와 어떤 관련(relation)이 있는지 설명하는 attribute  
	-> SEO에 영향을 줌
	- `type` : 링크된 외부 리소스의 미디어 타입 명시
	- `sizes` : 링크된 외부 리소스의 크기 명시

- `<script>`
	- Javascript를 추가할 수 있음
	`<script src="jsfile.js" defer></script>`
	- 소스파일을 링크할 수도 있지만 tag 사이에 코드를 바로 적을 수도 있음
	- empty element가 아님!!

- `lang` attribute in `<html>` element
	- head 블록에 들어가지 않지만 문서 작성 초기에 해야하는것
	- increases accessibility
	`<html lang="en-US"></html>`로 문서가 사용하는 언어 명시  
	※ `<span lang="ko"></span>`과 같이 특정 구역만 원하는 언어로 지정할 수 있음

## Text fundamentals
- The reasons we have to give structural markup to our content
	- to give headings to users within a few seconds
	- to increase SEO
	- Accessibility
	- to apply CSS, JavaScript effectively

- list : ok to nest one list inside another one
	- CSS 스타일로 마커 변경 가능

- Emphasis and importance
	- emphasis : `<em></em>`
	- strong importance : `<strong></strong>`
	- presentational elements : `<b></b>`, `<i></i>`, `<u></u>`, `<mark></mark>`
		- to write bold, italics, underlined before CSS is fully supported
		- lang과 같은 attribute 사용 가능 -> semantically appropriate하게 사용해야함  
		`The menu was a sea of exotic words like <i lang="uk-latn">vatrushka</i>, <i lang="id">nasi goreng</i> and <i lang="fr">soupe à l'oignon</i>.`  
		`Someday I'll learn how to <u style="text-decoration-line: underline; text-decoration-style: wavy;">spel</u> better.`

## Creating hyperlinks
- `<a>`
	- block-level element까지 link 가능
	- attribute `title` contains additional information about the link( = tooltip)
	- attribute `target` : `target="_blank"` 추가하면 새창에서 열림

- URLs and paths
	- URL(Uniform Resource Locator)s use paths to find files(URL ≠ path)
	- Document fragments : a link to a specific part of an HTML document
		- `id` attribute를 이용해 fragment를 만들 수 있음
		`<h2 id="Mailing_address">Mailing address</h2>`  
		`<a href="#Mailing_address">mailing address</a>`  
		과 같이 사용
	- Absolute URL
		- points to location defined by its absolute location on the web, including protocol and domain name  
		`https://www.example.com/projects/index.html`(디렉토리까지만 적으면 generally index.html을 의미)
		- alwasy point to the same location , no matter where it's used
	- Relative URL
		- points to location that is relative to the file you are linking from
		`project-brief.pdf`(in same directory)

- Clear link wording
	- We need to make our links *accessible* to all readers
	- Don't repeat the URL as part of the link text
	- Don't say "link" or "links to" in the link text
	- Keep your link as short as possible
	- Minimize instances where multiple copies of the same text are liked to different places("click here"s)

- Use relative links wherever possible
	- easier code, more efficient performance(use same server to look up the file in the link)

- Linking to non-HTML resources - leave clear signposts
	- `<a href="large-report.pdf">Download the sales report (PDF, 10MB)</a>`
	- `<a href="https://www.example.com/car-game">Play the car game (requires Flash)</a>`
	- `download` attribute : provide a default save name
		- `<a href="div1timetable.pdf" download="timetable.pdf">Timetable for div.1 (English, US)</a>`

- 모든 페이지들의 링크를 모아서 navigation menu를 만들 수도 있음(모든 페이지에 자신의 링크를 빼고 넣어놓으면 같은 페이지같은 느낌 줌)

- E-mail links
	- `mailto:` URL scheme 사용  
	`<a href="mailto:nowhere@mozilla.org">Send email to nowhere</a>`
	- `mailto:`뒤에 recipient의 메일주소를 생략하면 메일 쓰는 창만 열림 -> *share* 기능
	- recipient 이외에도 mail header fields를 URL에 추가할 수 있음
		- `cc` : Carbon Copy
		- `bcc` : Blind Carbon Copy
		- `subject` : Email subject
		- `body` : Email body  
		- main URL과 field values를 분리할 때는 `?` 사용, field끼리 분리할 때는 `&` 사용, field values끼리 분리할 때는 `;` 사용  
		`"mailto:nowhere@mozilla.org?cc=name2@rapidtables.com&bcc=name3@rapidtables.com;name4@rapidtables.com&subject=The%20subject%20of%20the%20email&body=The%20body%20of%20the%20email"`

## Advanced text formatting
- Description lists(*dictionary list*)
	- `<dl>` : description list, wrap whole list like `<ol>`
	- `<dt>` : description term, wrap each term
	- `<dd>` : description definition, wrap each description
	- It is permitted to have a single term with multiple descriptions
	```html
	<dl>
		<dt>term1</dt>
		<dd>description1</dd>
		<dt>term2</dt>
		<dd>description2</dd>
		<dd>description3</dd>
	</dl>
	```
	is equivalent to
	```
	term1  
		description1
	term2
		description2
		description3
	```

- Quotations
	- Blockquotes
		- `<blockquote>` 이용
		- `cite` attribute로 출처 남길 수 있음
		- will be rendered as indednted paragraph by browser default styling  
		```html
		<p>Here below is a blockquote...</p>
		<blockquote cite="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote">
			<p>The <strong>HTML <code>&lt;blockquote&gt;</code> Element</strong> (or <em>HTML Block
			Quotation Element</em>) indicates that the enclosed text is an extended quotation.</p>
		</blockquote>
		```
	- Inline quotations
		- `<q>` 이용
		- will be rendered as normal text put in quotes by browser default styling
	- Citations
		- `<cite>` 이용
		- italicize 이외의 기능은 없음 -> 인용문에는 quotation elements with `cite` attribute, 출처에는 `<a>`, `<cite>` elements 이용해서 표시해줘야함
		`<p>According to the <q><a href="#blockquote"><cite>MDN blockquote page</cite></a></q>:</p>`

- Abbreviations
	- `<abbr>` 이용
	- `<acronym>`도 있지만 `<abbr>`과 겹쳐서 잘 쓰지 않음
	- `title` attribute의 attribute value가 tooltip으로 표시됨  
	`<p>We use <abbr title="Hypertext Markup Language">HTML</abbr> to structure our web documents.</p>`  
```html
※※ 알쓸신잡(abbreviation, acronym, initialism)
 - abbreviation : any shortend or contracted form of a word or phrase(Rly, ex, ...)
 - acronym : a specific type of abbreviation formed the first letters of a multi-word term(OPEC, THAAD, ...)
 - initialism : a type of acronym but usually pronounced by saying each letter of the acronym(IDK, ATM, ...)
asd
 - 즉 initialism ∈ acronym ∈ abbreviation
```

- Contact details
	- `<address>` 이용
	- namecard느낌, italicize 이외의 기능은 없음
	```html
	<address>
		<p>
			Chris Mills<br>
			Manchester<br>
			The Grim North<br>
			UK
		</p>

		<ul>
			<li>Tel: 01234 567 890</li>
			<li>Email: me@grim-north.co.uk</li>
		</ul>
	</address>
	```

- Superscript and subscript
	- `<sup>`, `<sub>` 이용  
	`<p>If x<sup>2</sup> is 9, x must equal 3 or -3.</p>`

- Representing computer code
	- `<pre>` : For retaining whitespace(preformatted text)
	- `<code>` : For marking up generic pieces of computer code
	- `<var>` : For specially marking up variable names
	- `<kbd>` : For marking up keyboard and any other types of input entered
	- `<samp>` : For marking up the output of a computer program
	- Though they are all same after rendering, they has to be written according to the intentions made
	```html
	<pre><code>var para = document.querySelector('p');

	para.onclick = function() {
		alert('Owww, stop poking me!');
	}</code></pre>

	<p>You shouldn't use presentational elements like <code>&lt;font&gt;</code> and <code>&lt;center&gt;</code>.</p>

	<p>In the above JavaScript example, <var>para</var> represents a paragraph element.</p>

	<p>Select all the text with <kbd>Ctrl</kbd>/<kbd>Cmd</kbd> + <kbd>A</kbd>.</p>

	<pre>$ <kbd>ping mozilla.org</kbd>
	<samp>PING mozilla.org (63.245.215.20): 56 data bytes
	64 bytes from 63.245.215.20: icmp_seq=0 ttl=40 time=158.233 ms</samp></pre>
	```

- Times and dates
	- `<time>` 이용
	- `datetime` attribute로 시간 저장  
	`<time datetime="2016-01-20">20 Jan. 2016</time>`

## Document and website structure
- Basic sections of a document(in the `<body>`)
	- header
		- a big strip across the top with a big heading, logo, and perhaps a tagline
		- stays the same from one webpage to another
	- navigation bar
		- links to the site's main sections
		- represented by menu buttons, links, or tabs
		- remains consistent from one webpage to another
		- considered to be part of the header rather than an individual component(not requirement, two separate is better for accessibility)
	- main content
		- a big area in the center contains most of the unique content of a given webpage
	- sidebar
		- peripheral info, links, quotes, ads, ...
		- contextual to what is contained in the main content
	- footer
		- a strip across the bottom of the page that generally contains copyright notices, contact info
		- sometimes used for SEO purposes, by providing links for quick access to popular content
	- "typical website"

![typical website](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Document_and_website_structure/sample-website.png)

- HTML for structuring content+layout elements in more detail
	- we need to respect semantics and use the right element for the right job
	- `<header>`
		- represents a group of introductory content
		- `<header>` in the `<body>` : global header of a webpage
		- `<header>` in the `<article>` or `<section>` : specific header for that section
	- `<nav>`
		- contains the main navigation functionality for the page
	- `<main>`
		- for content unique to this page
		- only once per page, directly inside `<body>`
		- shouldn't be nested within other elements
	- `<article>`
		- encloses a block of related content(e.g., a single blog post)
	- `<section>`
		- similar to `<article>`
		- grouping a single part of the page that constitutes one single piece of functionality(e.g., a mini map, a set of article headlines and summaries)
		- `<section>`, `<article>`은 서로 포함될 수 있음
	- `<aside>`
		- sidebar, often placed inside `<main>`
		- containes content can provide additional information indirectly related to it(glossary entries, author biography, related links, ...)
	- `<footer>`
		- represents a group of end content for a page
	- Non-semantic wrappers
		- group a set of elements together to affect them all as a single entity with some CSS or JavaScript
		- have to be used preferably with a suitable `class` attribute
		- `<span>`
			- inline non-semantic element  
			`<span class="editor-note">[Editor's note: ...]</span>`
		- `<div>`
			- block level non-semantic element  
			`<div class="shopping-cart">SOME HTML CODES</div>`
			- `<aside>`가 아님(현재 페이지의 main content와 관련되어있지 않고 어느 페이지에서든 볼 수 있어야함, main content가 아니기 때문에 `<section>`에 맞지도 않음)
			- heading을 넣어서 accessibility를 높일 수도 있음
			- Try to reduce usage to the minimum
			- block level element의 경우 background att로 배경 설정 가능
	- Line breaks and horizontal rules
		- `<br>` : creates a line breaks
		- `<hr>` : creates a horizontal rule denotes a thematic change

- Planning a simple website
	1. Note down common things to every page(header(title, logo), footer(contact details, copyright notice, ...))
	2. Draw a rought sketch of structure of each page(blocks)
	3. Brainstorm all the other content
	4. Sort all these content items into groups appropriately(theme, purpose, ...)
	5. Sketch a rought sitemap(Home page, Buy, Specials, Country-specific info, ...)

## Debugging HTML
- HTML is not compiled into a different form before the browser parses it and shows the result(it is interpreted, not compiled)

- Permissive code - HTML itself doesn't suffer from syntax errors because browsers parse it permissively(interpreted even if there are syntax errors)

- HTML codes can be checked in [Markup Validation Service](https://validator.w3.org/){:target="_blank"}

## Assessment01: Marking up a letter
- class, style같은 attribute들은 global attributes로 웬만한 element에는 다 포함되어있다

- list elements는 `<p>` 안에 nested될 수 없다
	- `<p>`는 content model이 phrasing content(=inline elements)기 때문

## Assessment02: Structuring a page of content
- `<header>`는 content model(permitted content)가 flow content이다

- `<header>`과 `<footer>`는 `<body>`안에 포함되지만 용도에 따라 `<main>`에 포함될 수도 아닐수도 있다

- Anatomy of assessment02
	- head : metadata
	- body
		- header : global title, logo, navigation bar
		- main : article, aside
		- footer : copyright, contact info


# Multimedia and embedding
## Images in HTML
- `<img>`
	- att : `src`, `alt`, `width`, `height`
	- hotlink to images on other servers는 하지 않는게 좋음
	- `alt`가 필요한 이유
		- Accessibility
		- misspelling of `src`
		- The browser doesn't support the image type
		- SEO
		- Low data mode
	- image에 링크를 걸 경우 로딩이 안될 때를 대비해 `alt`에 링크를 써놓는게 좋음
	- `width`, `height`
		- `width`, `height`를 써놓았을 때 image 로딩이 느릴 경우 이미지 공간을 미리 확보해놓아 더 빠르게 로드할 수 있음
		- 두 속성으로 이미지의 aspect ratio를 바꿀 수 있지만, 이미지가 왜곡됨  
		-> 이미지 비율을 바꿔야할 경우 CSS를 사용하는게 나음
	- `title`로 tooltip을 추가할 수 있지만, hovering with a mouse가 제한된 유저들(터치스크린 등)은 접근성이 떨어짐  
	-> 차라리 main article text에 포함시키는게 나음
	- image map  
	```html
	<img src="/examples/images/img_imagemap.jpg" alt="진실혹은거짓" usemap="#vending" style="width:320px; height:240px" />
	<map name="vending">
		<area shape="rect" coords="90,60,180,130" alt="거짓"
			href="https://ko.wikipedia.org/wiki/%EA%B1%B0%EC%A7%93%EB%A7%90">
		<area shape="rect" coords="210,200,70,130" alt="진실"
			href="https://ko.wikipedia.org/wiki/%EC%A7%84%EC%8B%A4">
	</map>
	```
		- `<map>`은 하나 이상의 <area>를 가짐, <area>가 버튼과 같은 역할

- `<figure>`, `<figcaption>` : Annotating images
	- provide a semantic container for figures  
	```html
	<figure>
		[FIGURE]
		<figcaption>caption</figcaption>
	</figure>
	```
	- [FIGURE]에는 image, a code snippet, video, equations, table 등이 들어갈 수 있음
	- `alt`와 `figcaption`는 semantic role이 다름

- CSS background images
	- CSS의 `background-image`를 이용  
	```html
	p{
		background-image: url("images/dinosaur.jpg");
	}
	```
	- No semantic meaning at all(It can't have any text equivalents)  
	※ If an image has meaning, in terms of your content, you should use an HTML image. If an image is purely decoration, you should use CSS background images.

## Video and audio content
- `<video>`
	- att : `src`, `controls`, `width`, `height`, `autoplay`, `loop`, `muted`, `preload`, `poster`  
	```html
	<video src="rabbit320.webm" controls>
	  <p>Your browser doesn't support HTML5 video. Here is a <a href="rabbit320.webm">link to the video</a> instead.</p>
	</video>
	```
	- fallback content : A paragraph inside the `<video>` tags(=alternative text)
	- `controls` : boolean attribute, allow users to control video/audio playback
	- Using multiple source formats to improve compatibility
		- container formats : like MP3, MP4, WebM, ...
		- codecs ∈ containers(e.g., WebM : Vorbis/Opus audio codec, VP8/VP9 video codec)  
		※ FLAC과 같은 특이한 경우도 있음(FLAC codec이 FLAC file안에 저장됨)
		- Different browsers support different video and audio formats, different container formats(MP3, MP4, WebM)
		- audio track don't need containers(audio player will play it directly)
		- `<source>`를 이용해서 video URL을 `<video>`안에 element로 넣을 수도 있음  
		```html
		<video controls>
			<source src="rabbit320.mp4" type="video/mp4">
			<source src="rabbit320.webm" type="video/webm">
			<p>fallback content <a href="rabbit320.mp4">here</a></p>
		</video>
		```
		- `<source>`로 URL을 넣으면 browser가 재생가능한 codec을 재생해줌
		- `type`을 추가하지 않으면 브라우저가 하나씩 로딩해서 체크하기 때문에 시간이 오래걸림
	- 나머지 att들은 `<video controls width="400" height="400"	autoplay loop muted preload="auto" poster="poster.png"> ...`와 같이 사용
	- `width`, `height` : aspect ratio와 맞지 않을 경우 Image와 같이 강제로 바꾸진 않고 가로를 채움
	- `autoplay` : makes the audio/video playing right away
	- `loop` : makes the audio/video start playing again whenever it finishes
	- `muted` : set muted as default
	- `poster` : the URL of an image displayed before the video is played
	- `preload` : used for buffering large files
		- "none" : does not buffer the file
		- "auto" : buffers the media file
		- "metadata" : buffers only the metadata for the file

- `<audio>`
	- works just like the `<video>` element
	- differences with `<video>`
		- no `width`, `height`, `poster` attributes(no visual componenet)

- Displaying video text tracks
	- reasons why it is needed
		- for auditory impairments
		- users in noisy environments
		- users in environments where having the audio playing would be a distraction
		- users who don't speak the language of the video
	- `<track>`, WebVTT file format 이용
		- WebVTT(Web Video Text Tracks) : a format for writing text files containing multiple strings of text along with metadata(e.g. subtitles, captions, timed descriptions)  
		```html
		<video controls>
			<source src="example.mp4" type="video/mp4">
			<source src="example.webm" type="video/webm">
			<track kind="subtitles" src="subtitles_es.vtt" srclang="es" label="Spanish">
		</video>
		```
		- `<track>` should be placed within `<audio>` or `<video>` but after all `<source>` elements
		- `kind` : specifies cues' purpose("subtitles", "captions", "descriptions")
		- `srclang` : language subtitles are written in
		- `label` : name of the track, set it to language to help readers

## From object to iframe
- A short history of embedding : `<object>`, `<embed>`(Java Applets, Flash) -> `<iframe>`, `<canvas>`, `<video>`

- `<iframe>`  
	```html
	<iframe src="https://developer.mozilla.org/en-US/docs/Glossary"
			width="100%" height="500" frameborder="0"
			allowfullscreen sandbox>
	  <p>
		<a href="/en-US/docs/Glossary">
		   Fallback link for browsers that don't support iframes
		</a>
	  </p>
	</iframe>
	```
	- att : `src`, `width`, `height`, `frameborder`, `allowfullscreen`, `sandbox`
	- `frameborder` : set a border between this frame and other frames, default : 1
		- can be better achieved using `border : none;` in CSS
	- `sandbox` : requests heightened security settings(need browsers > IE 10)  
	※ It's a good idea to set the iframe's `src` attribute with JavaScript after the main content is doen with loading. This makes your page usable sooner and decreases your official page load time(an important SEO metric)
	- iframe의 id를 선언하고 링크에서 target="ID"로 사용 가능(링크된 문서가 그 frame에서 열림)
		- HTML5 이전에는 `frameset`이 있었지만 이젠 권고하지 않음

- Security concerns
	- clickjacking, Intellectual Property issues, ...  
	-> 'you can never be too cautious'
	- Embed content starts with HTTP for safety
	- Always use the `sandbox` attribute
		- sandbox 밖의 나머지 부분을 조작할 수 없는 컨테이너
		- `sandbox=""`으로 permissions 추가 가능하지만 `allow-scripts`, `allow-same-origin`을 동시에 추가하면 sandbox를 사용하지 않는 것과 같음
	- CSP(content security policy)를 사용할 수도 있다고 함(HTTP headers라는데 사용법은 모르겠음)

- `<embed>` and `<object>`
	- general purpose embedding tools for embedding multiple types of external content, which include plugin technologies(e.g., JavaApplets, Flash, PDF, ...)
	- 이제는 잘 쓰지 않는 content이거나 더 좋음 embedding methods가 생겨서 잘 쓰지 않음
	- attributes는 [MDN 항목 참고](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Other_embedding_technologies#the_%3Cembed%3E_and_%3Cobject%3E_elements){target="_blank"}

## Adding vector graphics to the Web
- Raster images : defined using a grid of pixels(e.g., `.bmp`, `.png`, `.jpg`, `.gif`)

- Vector images : defined using algorithms work out the shapes
	- don't pixelate when zoomed in
	- lighter than raster equivalents

- SVG
	- XML-based language for describing vector images  
	```html
	<svg version="1.1"
		baseProfile="full"
		width="300" height="200"
		xmlns="http://www.w3.org/2000/svg">
		<rect width="100%" height="100%" fill="black" />
		<circle cx="150" cy="100" r="90" fill="blue" />
	</svg>
	```
	- `<rect>`, `<circle>`, `<feColorMatrix>`, `<animate>`, `<mask>`와 같은 features가 있음
	- Inkscape, Illustrator와 같은 vector graphics editor 사용
	- additional advantages
		- text in vector images는 accessible
		- SVG의 each component는 CSS나 JavaScript로 styling 가능
	- disadvantages
		- can getn complicated very quickly, complex SVGs take time to be displayed
		- can be harder to create than raster images
		- not supported in older browsers(supported since IE9)

- Adding SVG to your pages
	- The quick way: `<img>`
		- 다른 format들 넣는 것처럼 넣으면 됨
		- Pros
			- quick, familiar syntax
			- easy to make hyperlink by nesting `<img>`
			- SVG file can ben cached by the browser
		- Cons
			- cannot manipulate the image with JavaScript
			- to control the SVG with CSS, you must include inline CSS
			- cannot restyle the image with CSS pseudoclasses(like `:focus`)
		- Troubleshooting and cross-browser support
			- `<img src="shape.png" alt="alttext" srcset="shape.svg">`
				- only supporting browsers will load the SVG, olders will load the PNG instead
			- use CSS background  
			```html
			background: url("fallback.png") no-repeat center;
			background-image: url("image.svg");
			background-size: contain;
			```
				- older browsers will stick with the PNG, while newer will load the SVG
	- Inlining SVG with `<svg>`
		- Pros
			- possible to assign classes, ids to SVG elements and style them with CSS
			- can wrap it in an `<a>` element
			- saves an HTTP request -> reduce loading time a bit
			- the only approach lets you use CSS interactions(`:focus`) and CSS animations on your SVG image
		- Cons
			- can causes a lot of duplication
			- extra SVG code increases the size of HTML file
			- cannot cache inline SVG
			- include fallback in a `<foreignObject>` element, but browsers that support SVG still download any fallback images
	- embed an SVG with an `<iframe>`
		- definitely not the best method to choose
		- Cons
			- `iframe`s have a fallback mechanism, but browsers only displaly the fallback if they lack support fo `iframe`s altogether
			- unless the SVG and webpage have the same origin, you cannot use JavaScript on your main webpage to manipulate the SVG

## Responsive images
- Why responsive images?
	- Issues arise when you start to view your site on a narrow screen device
		- 사진이 잘리게 되는데 이미지의 중요한 부분을 보여주는 자른 이미지를 보여줘야함(=art direction problem)
		- 작은 모바일 화면에는 큰 해상도의 이미지가 필요없음(=resolution switching problem)

- How to create responsive images
	- CSS arguably has better tools for responsive design than HTML, but we'll be focusing on the HTML `<img>`s
	- Resolution switching: Different sizes
		- `<img>`의 `srcset`, `sizes` attribute 사용
		- each value : comma-separated list  
		```html
		<img srcset="elva-fairy-480w.jpg 480w,
				 elva-fairy-800w.jpg 800w"
			sizes="(max-width: 600px) 480px,
				800px"
			src="elva-fairy-800w.jpg"
			alt="Elva dressed as a fairy">
		```
		- `srcset`
			- `srcset="URL w-descriptor"`
			- w descriptor : the image's intrinsic width in pixels
		- `size`
			- `size="Media-condition width-of-the-slot"`
			- media condition : possible state that the screen can be in  
			(e.g., (max-width:600px) means when the viewport width is 600 pixels or less)  
			※ viewport : `<head>`에 정의(`<meta name="viewport" content=width=device-width">`)
			- the width of the slot : 이미지가 채워질 칸의 width
			- the last slot width : default, no media condition
			- similar to switch statement, be careful for the order of the conditions
		- browser's process to display : find the width of the slot by compare the viewport with the conditions in the `sizes`, load the image referenced in the `srcset` that size >= the slot size
	- Resolution switching: Same size, different resolutions
		- 위 방법에서 w descriptor를 x descriptor로 바꾸고 `sizes`를 없앤 것
		- 대신에 img에 `width: 320px;` 내용의 CSS가 필요함
		- CSS pixel과 페이지에 접근하는 device의 pixel을 비교해서 적절한 이미지 로드함(if the device has a high resolution of two device pixels per CSS pixel or more, 고화질(2x) 로드
		- CSS pixel의 개념을 찾아보고 다시 봐야할듯(CSS pixel은 디바이스에 상관없이 최대 픽셀이 고정인지 잘 모르겠음)
	- Art direction
		- resolution switching을 사용할 경우 화면이 너무 작으면 사진을 제대로 알아보기가 어렵다는 문제점이 있음 -> 사진을 브라우저의 해상도별로 다르게 설정
		- `<picture>`
			- `<img>`와 비슷하게 사용  
			```html
			<picture>
				<source media="(max-width: 799px)" srcset="elva-480w-close-portrait.jpg">
				<source media="(min-width: 800px)" srcset="elva-800w.jpg">
				<img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva">
			</picture>
			```
			- `media` : attribute value=media-condition
			- `srcset` : `<img>`처럼 여러 img를 넣을 수 있지만 필요없음
			- fallback contet를 위해 마지막에 `<img>`를 넣어줘야함
			- `<source>`안에 `media`를 넣었을 경우 `sizes`는 넣으면 안됨(`media` : only in art direction scenarios)
	- The reason not to do this with CSS or JavaScript
		- browser starts to download any images before the main parser has started to load and interpret the page's CSS and JavaScript -> out of order
	- Modern image formats  
	```html
	<picture>
		<source type="image/svg+xml" srcset="pyramid.svg">
		<source type="image/webp" srcset="pyramid.webp">
		<img src="pyramid.png" alt="regular pyramid built from four equilateral triangles">
	</picture>
	```


# HTML Tables
## HTML table basics
- When should you NOT use HTML tables?
	- a lot of people use HTML tables to lay out web pages(one row for header, ...)
	- it was because CSS support across browsers used to be terrible(they are much less nowadays)
	- Using tables for layout rather than CSS layout techniques is a bad idea
		- layout table reduce accessibility for visually impaired users
		- tables produce tag soup
		- tables are not automatically responsive : `<header>`, `<section>`, `<div>`같은 것들은 부모 element의 100%로 너비가 설정되지만 table은 담기는 content에 따라서 너비가 설정되기 때문에 layout으로 쓸 경우 기기별로 너비를 설정해야해서 번거로움

- elements of `<table>`
	- `<tr>` : table row
	- `<td>` : table data(empty cell : `<td>&nbsp;</td>`)
	- `<th>` : table header(works in exactly the same way as a `<td>`)
		- style : bold, centered
		- `scope` attribute로 한번에 묶을 수 있음

- Allowing cells to span multiple rows and columns
	- `<td>`, `<th>`의 `colspan`, `rowspan` attributes 이용  
	e.g. `<th colspan="2">Animals</th>` -> spanning two columns

- Providing common styling to columns
	- an entire column에 대해 스타일을 지정하려면 CSS의 `:nth-child`를 사용하거나 `<td>`, `<th>`에서 일일히 지정해줘야했음 -> `<col>`, `<colgroup>` to define styling information for a column
	- limited to a few properties: `border`, `background`, `width`, `visibility` for other properties, style every `<td>` or `<th>`, or use complex selector  
	- 모든 column이 있어야함, 스타일링이 필요하지 않은 col의 개수가 많을 경우 span을 이용해 한번에 처리 가능(`<col span="2">` 이런 식으로)
	```html
	<table>
		<colgroup>
			<col>
			<col style="background-color: yellow">
		</colgroup>
		<tr>
			<th>Data 1</th>
			<th>Data 2</th>
		</tr>
		<tr>
			<td>Calcutta</td>
			<td>Orange</td>
		</tr>
		<tr>
			<td>Robots</td>
			<td>Jazz</td>
		</tr>
	</table>
	```
	- If we wanted to apply the styling information to both columns, we could just include one `<col>` element with a span attribute on it like `<col style="background-color: yellow" span="2">`
	- `style`에서 `border`의 굵기를 1px로 설정하면 안보임, 최소 2px, solid : 실선  
	e.g. `style="border: 2px solid #000000;"`
	- `table`, `td` 모두 border설정해서 테두리가 겹칠 경우 `border-collapse="collapse"` 넣어서 하나 없앨 수 있음

## HTML table advanced features and accessibility
- Adding a caption to table with `<caption>`
	- nest `<caption>` directly beneath the `<table>` tag  
	```html
	<table>
		<caption>Dinosaurs in the Jurassic period</caption>
		...
	</table>
	```
	- `<table>`의 `summary` 속성도 같은 역할이지만 HTML5에서 잘 쓰이지 않고 페이지에 나타나지 않음

- Adding structure with `<thead>`, `<tfoot>`, and `<tbody>`
	- these don't make the table any more accessible and don't result in any visual enhancement on their own but userful for styling and layout-acting as useful hooks for adding CSS
	- `<thead>`
		- wrap the header part of the table
		- if you're using `<col>`/`<colgroup>`, `<thead>` should come just below those
	- `<tfoot>`
		- wrap the footer part of the table
	- `<tbody>`
		- wrap the other parts of the table
		- always included in every table(if you don't specify it, browser would add it for you)
	- `<thead>`, `<tfoot>`은 자동으로 안의 내용이 위/밑에 위치하게됨
	- header가 하나의 열일 경우 `<col>`을 이용해 스타일링

- Nesting tables
	- `<td>`안에 그냥 집어넣으면 됨, 근데 nesting하면 table이 여러 개가 되니까 id를 사용하는게 나음(`<td id="nested">`이런 식으로))
	- 최선은 nesting table을 사용하지 않는 것

- Tables for visually impaired users
	- Using column and row headers(`<th>`)
	- The `scope` attribute
		- `<th>`에 대해 header for row인지 column인지 정의함  
		e.g. `<th scope="row">Haircut</th>`
		- `row`, `col` 이외에도 `colgroup`, `rowgroup`도 value에 넣을 수 있음(col/row가 span되어있을 경우 사용)
	- The id and headers attributes
		- 헤더인 `<th>`에 `id="asdf"` attribute 추가, 그 헤더에 속하는 `<td>`에 `headers="asdf"` 추가
		- 여러 header에 속할 수도 있는데 이때 id는 space로 구분
	- usually `scope` approach is enough for most tables


# HTML 입력양식
- `<form>`
	- 사용자로부터 입력을 받아서 서버로 보낼 때 사용  
	```html
	<form action="form-handler URL" method="get|post">
	...
	</form>
	```
	- `action`
		- value : form-handler(입력받은 데이터를 처리할 서버 상의 스크립트 파일)의 URL
	- `method`
		- value : `get` or `post`
		- `get` : URL에 data를 추가하여 전달하는 방식, 주소에 데이터가 그대로 나타남(쿼리 등의 크기가 작은 중요도가 낮은 정보를 보낼 때 사용)
		- `post` : data를 별도로 첨부해서 보냄(데이터 크기 제한 없고 보안, 활용도가 `get`보다 높음)
	- content : flow content(`<form>` 제외)
		- `<input>`, `<select>`, `<textarea>`, `<button>` 등
	- 접근성을 위해서 각 element만들 때 `id` 추가하고 `<label for="ID">...</label>` 이용하기!

- `<input>`
	- `type` : 입력받을 데이터의 종류
		- `type`에 따라 att가 추가될 수 있음(아래는 여러 가지 type들)
		- text : `<input type="text" name="search">`
		- password : `<input type="password" name="password">`
		- radio button : `<input type="radio" name="lecture" value="html" checked> HTML`
			- 같은 그룹은 같은 `name`을 가지고 있어야함
			- `checked`로 미리 선택되어있는 항목 지정
		- checkbox : `<input type="checkbox" name="lecture" value="cpp" disabled>`
			- radio button과 비슷
		- file : `<input type="file" name="upload_file" accept="image/*">`
			- `accept`를 이용해서 파일 종류/확장자 명시
		- submit : `<input type="submit" value="전송">`
			- form-handler로 데이터를 전송하는 버튼
	- `name` : 서버로 데이터가 전송될 때 데이터의 label
	- `value` : input field가 있는 type에 대해 initial value 설정
	- `disabled` : input field를 사용할 수 없도록 설정
	- `readonly` : 사용자가 input field를 볼 수는 있지만 수정 불가능, submit을 누르면 `disabled`와는 다르게 initial value가 서버로 전송됨
	- `maxlength` : input field에 입력할 수 있는 문자의 max length 설정(e.g., `maxlength="10"`)
	- `size` : input field의 크기 설정(`size="30"`)

- drop-down list(`<select>`)
	- `selected`로 미리 선택되어있는 항목 지정  
	```html
	<select name="fruit">
		<option value="apple"> 사과
		<option value="orange" selected> 귤
		<option value="strawberry"> 딸기
		<option value="peach"> 복숭아
	</select>
	```

- textarea(`<textarea>`)
	- `rows`, `cols`로 크기 설정 가능  
	```html
	<textarea name="message" rows="5" cols="30">
    	여기에 적으세요.
	</textarea>
	```

- button(`<button>`)
	- `onclick`으로 클릭시 작업 설정  
	```html
	<button type="button" onclick="alert('버튼을 클릭하셨군요!')">
    	버튼을 눌러주세요.
	</button>
	```

- `<fieldset>`
	- `<form>`안에 여러 type의 데이터를 입력받을 때 이것들을 하나로 묶어주는 element
	- `<legend>`로 자신에 대한 설명 표시  
	```html
	<form action="/examples/media/request.php">
		<fieldset>
			<legend>입력 양식</legend>
			이름 : <br>
			<input type="text" name="username"><br>
			이메일 : <br>
			<input type="text" name="email"><br><br>
			<input type="submit" value="전송">
		</fieldset>
	</form>
	```
