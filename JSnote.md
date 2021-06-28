Part 1: The JavaScript language(21.05.24 ~)
# An introduction
## An Introduction to JavaScript
### What is JavaScript?
JavaScript : 웹페이지에 생동감을 불어넣기 위해 만들어진 *프로그래밍 언어*  
Script : JS로 작성한 프로그램(HTML안에서도 작성 가능 => 웹페이지가 로딩될 때 자동으로 실행됨)
- script는 plain text로 작성 및 컴파일 없이 실행 가능
- Java와는 매우 다른 언어임!

> 원래 JS는 LiveScript였지만, Java의 인기에 편승하기 위해 JavaScript로 이름을 바꿈  
> 현재는 ECMAScript라는 고유한 Specification을 가진, JAVA와 아무런 관련이 없는 언어임

JS는 브라우저뿐만 아니라 서버 등 JavaScript engine이 있는 모든 디바이스에서 동작함  
browser에는 JavaScript virtual machine이라는 embedded engine이 있음  
다양한 엔진들:
- V8 : Chrome, Opera
- SpiderMonkey : Firefox
- Chakra, Trident : IE
- ChakraCore : Edge
- SquirrelFish : Safari

"a feature X is supported by V8"과 같이 엔진으로 지원 여부를 알려주기도 하므로 엔진 이름들을 기억해놓는 게 좋음

대략적인 엔진의 작동 방식:
1. script을 파싱(parse)함
2. 기계어로 컴파일(compile)함
3. 기계어를 실행함  
각 단계별로 최적화를 실행하고, 코드를 실행하면서 분석한 데이터를 바탕으로 다시 최적화를 하기도 함

### What can in-browser JavaScript do?
최신의 JavaScript는 안전한 프로그래밍 언어임  
(메모리나 CPU에 대해 low-level access(직접적인 조작)를 허용하지 않음, 이런 기능을 필요로 하지 않는 브라우저라는 환경에서 만들어진 것이기 때문)

JavaScript의 capability는 실행되는 환경에 따라 달라짐  
예를 들어, Node.js에서는 임의의 파일에 대한 수정, 네트워크 요청 등을 수행하는 함수를 지원함  

In-browser JS에서는 아래의 예시와 같이 웹페이지 조작에 관한 모든 것들을 할 수 있음:
- 페이지에 HTML 추가, HTML 또는 스타일 수정
- 유저의 행동에 반응(마우스 클릭, 움직임, 키 눌림 등)
- 원격 서버에 요청, 파일 업로드/다운로드(AJAX, COMET)
- cookies 조작, 유저에게 메시지 및 질문
- client(local storage)에 데이터 저장

### What CAN'T in-browser JavaScript do?
브라우저에서는 *보안을 위해* JS의 기능에 제한을 걸어둠  
아래와 같은 제한들이 있음  
- 브라우저 상의 JS에서는 하드 디스크에 있는 파일을 실행, 복사, 수정할 때 제한될 수 있음  
	∵ 운영체제에서 지원하는 기능을 직접 사용하지 못함
	
	모던 브라우저에서는 `<input>` 태그를 통해 파일을 선택하는 등 특정한 상황에서 접근이 허용됨  
	JS가 활성화된 페이지라도 카메라, 마이크 같은 디바이스를 사용하기 위해선 사용자의 명시적인 허가가 필요함
- 기본적으로 탭/창들은 서로 알 수 없지만, 한 페이지의 JS를 이용해서 새 페이지를 열 때와 같이 예외가 존재함  
	위와 같은 예시도 site, domain, protocol, port 등이 다르면 서로 접근 불가(Same Origin Policy라고 함)  
	e.g. `A.com`에서 연 탭은 주소가 `B.com`인 탭의 정보를 가져올 수 없음
	
	Same Origin Policy를 우회하기 위해선, 위처럼 Origin이 같아야 할 뿐만 아니라 두 페이지가 데이터 교환에 동의하고 관련된 JS를 포함하고 있어야 함(나중에 tutorial에서 할 예정)
- JS를 이용하면 현재 페이지의 서버와 쉽게 통신이 가능함  
	하지만 다른 사이트나 domain으로부터의 수신은 불가능함  
	가능하다 해도, 상대편의 명시적인 동의(HTTP headers에서의)가 필요함

위와 같은 제한은 JS가 브라우저가 아닌 다른 환경(서버 등)에서 실행될 때는 존재하지 않음  
모던 브라우저에서는 plugin/extensions를 이용해서 권한 확장을 요청하기도 함

### What makes JavaScript unique?
JS의 대표적인 장점 3가지:
- Full integration with HTML/CSS
- Simple things are done simply
- Support by all major browsers and enabled by default

JS는 위 3가지를 가진 유일한 browser technology임  
따라서 브라우저 인터페이스를 만들 때 많이 사용되고, 서버나 앱을 만들 때도 사용되기도 함

### Languages "over" JavaScript
JS의 문법만으로는 다양한 기능을 지원하지 못함  
=> 최근에 browser에서 실행되기 전에 JS로 transpile되는 언어들이 생겨남

최신 툴들을 이용하면 transpilation을 빠르게 수행 가능(다른 언어로 쓰여 있는 코드를 자동으로 변환해줌)

JS로 transpilation이 가능한 언어들의 예시:
- CoffeeScript : 'syntatic sugar' for JS  
	- shorter syntax를 도입, 코드 가독성 ↑
	- Ruby와 함께 사용됨
- TypeScript : 'strict data typing'
	- by Microsoft
- Flow
	- TypeScript와 다른 방법으로 data typing을 추가함
	- by Facebook
- Dart
	- app과 같은 브라우저 환경이 아닌 곳에서 돌아가는 엔진으로 실행됨
		독자적인 언어지만, JS로 transpile될 수 있음
	- by Google
- Brython : Python transpiler to JS
- Kotlin
	- browser나 Node에서 실행 가능한 최신 언어임

## Manuals and specifications
### Specification
ECMA-262 specification에 의해 JS가 정의됨  
거의 표준이 된 최신 기능(stage 3라고 불림)을 알기 위해선 [여기](https://github.com/tc39/proposals)를 보면 됨  
browser에서의 기능들은 뒤에 챕터에서 다룰 예정

### Manuals
- MDN JS Reference가 가장 설명이 잘 되어있음

### Compatibility tables
JS는 개발중인 언어기 때문에 새로운 기능들이 정기적으로 추가됨  
엔진, 브라우저 기준으로 지원 여부를 보기 위해선 아래 사이트들을 확인하면 됨:
- [http://caniuse.com](http://caniuse.com) : 기능 별로 지원 여부가 표로 정리되어 있음
- [https://kangax.github.io/compat-table](https://kangax.github.io/compat-table) : 언어 별로 지원 여부가 정리되어 있음

## Code editors
크게 IDE, lightweight editor 두 종류가 있음

### IDE
IDE(Integrated Development Environment) : 전체 프로젝트를 운영하는데 사용되는 기능을 가진, 통합 개발 환경  
프로젝트 로드, autocompletion, version management system, testing environment 등의 프로젝트 단위 기능 제공  
VS Code, WebStorm 등이 있음  
※ Visual Studio는 VS Code와 다르게 Windows에서만 실행 가능하고 .NET platform, JS에 잘 맞음

### Lightweight editors
IDE보다 제공하는 기능이 적지만 빠르고 편리함  
주로 하나의 파일을 즉시 편집하기 위해 사용  
- IDE : 프로젝트 단위로 작동 => 로딩할 때 시간이 좀 걸림
- Lightweight editors : 한 파일만 필요하기 때문에 훨씬 빠름

사실 많은 lightweight editor에 directory-level syntax analyzers, autocompleters와 같은 기능을 지원하는 plugin이 존재하기 때문에 IDE와 분명한 차이점은 없음

Lightweight editors의 예시:
- Atom, VS Code, Sublime Text, Notepad++(Windows에서만 가능), Vim, Emacs

### Let's not argue
다른 훌륭한 editor도 많고, 프로젝트, 개인적인 성향에 따라 평가가 다름

## Developer console
script의 에러를 고치기 위해서 developer tools가 browsers에 내장되어 있음  
Chrome, Firefox가 developer tools가 잘 되어 있어서 개발할 때 많이 사용됨  
에러가 browser-specific한 경우도 존재함

Developer tools를 이용하면 에러 확인, 코드 실행, 변수 확인 등의 여러 기능을 사용할 수 있음

### Google Chrome
`F12`, `Cmd + Opt + J`(Mac)으로 호출 가능  
script error가 상단에 표시됨  
`Shift + Enter`로 여러 줄 입력 가능

### Firefox, Edge, and others
대부분 `F12`로 개발자 도구를 열 수 있음  

### Safari
Safari에서는 Advanced 안에 "Develop menu"를 먼저 활성화 해야 함  
이후 `Cmd + Opt + C`로 console을 키고 Develop를 사용 가능


# JavaScript Fundamentals
## Hello, world!
`alert`는 browser-specific command임  
Node.js와 같은 서버 환경에서는 `node my.js`와 같은 command로 script 실행 가능

### The "script" tag
HTML 문서 안에는 `<script>` tag를 이용해서 어디든 JS program을 삽입할 수 있음

#### Example
```html
<script>
  alert('Hello, world!');
</script>
```

- `Hello, world!`라는 메시지를 띄움
- `<script>` 태그가 처리될 때 자동으로 실행됨

### Modern markup
지금은 잘 쓰지 않지만 `<script>` 태그에 attributes가 있음
- `type` attribute
	- `type="text/javascript"`가 HTML4에서는 필수였지만, 현재는 아님
	- 최신의 HTML에서는 `type`의 의미를 아예 바꿔서 JS module을 사용할 때 씀
- `language` attribute
	- script의 언어를 명시하지만, 현재는 JS가 default로 설정되어 있어서 안써도 됨

아주 옛날에는 `<script>`를 아래와 같이 사용함  
```html
<script type="tet/javascript"><!--
  ...
//--></script>
```

- JS code를 처리하지 못하는 browsers에 대해서 코드를 숨기기 위해 사용
- 최근 15년 동안에는 이런 이슈가 없었음
	=> 현재는 사용하지 않음

### External scripts
`src` attribute를 이용해서 script files를 넣을 수도 있음

#### Example
```html
<script src="/path/to/script.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.11/lodash.js"></script>
```

- absolute path, relative path, URL 등을 value로 사용할 수 있음
- 여러 파일을 넣기 위해선 `<script>` 태그를 반복해서 사용해야 함

> 간단한 script만 HTML에 넣고 크기가 큰 script는 파일로 참조하는게 나음!  
> 파일로 참조하면 browser의 cache에 저장되기 때문에, 여러 페이지에서 같은 script를 사용하는 상황에서 script를 한 번만 다운로드하고 cache에서 불러옴, 트래픽 ↓

※ `src` attribute가 선언되어 있으면 script content는 무시됨  
따라서 외부 script 하나를 참조하고 HTML 내부에 script 하나를 넣어야 하면 `<script>` 태그를 두 번 사용해야 함  
e.g.  
```html
<script src="file.js"></script>
<script>
  alert(1);
</script>
```
 

## Code structure
### Statements
```javascript
alert('Hello'); alert("World");
```

- string에 대해서 single quotes, double quotes, backtick 모두 사용 가능함

### Semicolons
JS는 line break를 implicit semicolon으로 인식함!(automatic semicolon insertion에 의해)  
따라서 아래의 코드도 정상적으로 작동함:  
```javascript
alert('Hello')
alert('World')
```

하지만 모든 line break가 semicolon으로 interpet되는 건 아님  
e.g.  
```javascript
alert(3+
1
+2)
```

- `6`이 출력됨
- statement가 완전하지 않기 때문에 semicolon을 넣지 않음

#### Example
```javascript
alert("Hello")

[1, 2].forEach(alert);
```

- 예상되는 결과는 `Hello`, `1`, `2`를 순서대로 출력하는 것이지만, 실제로는 세미콜론이 첫 번째 줄의 끝에 삽입되지 않기 때문에 `Hello`까지만 나옴

웬만하면 세미콜론을 넣는게 나음

### Comments
One-line comments : `// Comments`  
Multiline comments : `/* comments */`  
multiline comments의 경우 중첩될 수 없음

대부분 `Ctrl + /`, `Ctrl + Shift + /`로 단축키가 지정되어 있음

주석은 대부분 production server로 publish되기 전에 지워짐

## The modern mode, "use strict"
전에는 호환성 문제가 없어 JS가 업데이트 되어도 이전의 코드를 수정할 필요가 없었음  
하지만 2009년 ECMAScript 5(ES5)에서 기능을 추가하면서 기존의 것을 수정함  
=> 오래된 코드들의 동작을 위해서 수정된 내용들은 기본적으로 반영되지 않은 채로 남겨놓음  
`"use strict"`를 이용해서 변경된 내용을 활성화 해줘야 함

### "use strict"
`"use strict"`도 큰따옴표, 작은따옴표 상관없음  
e.g.  
```javascript
"use strict";
// this code works the modern way
...
```
- 함수 안에서 사용하면 그 함수에서만 strict mode가 적용됨
- 보통 코드의 맨 윗부분에 적어놓음
	- 중간에 적어놓으면 무시되기 때문에 맨 위에 적거나 적지 않거나 둘 중 하나임
- 한 번 적용하면 다시 해제할 수 없음

### Browser console
browser console에서는 strict mode를 바로 적용하면 페이지 전체에 영향을 미침  
아래와 같이 console에서 입력할 내용에만 적용하는게 나음  
```javascript
'use strict'; <Shift + Enter for a newline>
// codes
<Enter to run>
```

오래된 브라우저에서는 아래와 같이 wrapper를 이용해야 함  
```javascript
(function() {
  'use strict';
  
  // codes
})()
```

### Should we "use strict"?
최신의 JS는 class와 module을 지원함  
class, module은 자동으로 strict mode를 활성화시키기 때문에 이것들을 사용하면 `'use strict'`를 코드 안에 쓰지 않아도 됨

이후의 챕터들에서 다양한 기능들에 대해 strict와 old modes에서의 차이점을 알아볼 예정임(수가 적고 웬만하면 strict모드가 더 나음)  
앞으로의 예제들은 모두 strict mode라고 가정함

## Variables
### A variable
변수 : 이름을 가진 저장 공간  
`let` keyword를 이용해서 변수 선언 가능  

#### Example
```javascript
let message='Hello';

alert(message);
```
- `let` 빼고는 cpp와 비슷함
- 오래된 코드에서는 `let` 대신 `var`을 사용함

**multiline styles**  
```javascript
let user='John, age=25, message='Hello';

let user='John';
let age=25;
let message='Hello';

let user='John',
  age=25,
  message='Hello';

let user='John'
  , age=25
  , message='Hello';
```
- JS도 스페이스 2번으로 인덴팅을 하기 때문에 comma-first style이 보기 좋은 듯

### A real-life analogy
변수 개념에 대한 설명

※ 함수형 언어에서는 변수의 재사용이 금지됨

### Variable naming
JS의 변수 이름에 대한 2가지 제한:
1. 변수 이름에는 알파벳, 숫자, `$`, `_`만 들어가야 함
2. 첫 번째 글자는 숫자가 될 수 없음

변수 이름이 길면 보통 camelCase로 지음  
`$`, `_`도 각각 변수 이름으로 사용할 수 있음  
대소문자 구별함!  
non-latin 문자도 가능은 함  
예약된 keyword 존재(`let`, `class`, `return`, `function` 등)

strict mode를 사용하지 않으면 `num=5;`라는 대입 자체가 변수 선언도 해줬음  
strict mode를 사용하면 저 문장은 에러가 남

### Constants
`const`를 사용해서 선언  

#### Uppercase constants
대문자와 underscore를 이용해서 상수 이름을 짓고 사용하는게 관행임(진짜 상수값들에 대해서 alias 느낌으로)  
e.g. `const COLOR_RED="F00";`

상수 중에 프로그램이 실행되면서 계산되는 상수들은 정상적으로 이름지음  
e.g. `cost pageLoadTime=/*calculated time*/;`

### Name things right
프로젝트를 진행하면 기존의 코드를 수정하고 확장하는게 대부분이기 때문에 변수 이름을 잘 짓는게 중요함  
몇 가지 명명 규칙들:
- 읽을 수 있는 이름을 사용
- 약칭이나 `a`, `b`, `c`같은 짧은 이름을 피해야 함
- 이름이 최대한 변수에 대해 설명하도록 지어야 함(`data`는 너무 광범위함)
- 사전에 약속된 언어를 사용(사이트에 방문한 사람들을 user라고 정했으면 `currentUser`와 같이)

※ JS minifiers, browser에 의해 코드가 최적화되기 때문에 변수를 재사용하기 보다는 새 변수를 선언하는게 나음(최적화할 때도 코드의 목적을 더 쉽게 파악할 수 있음)

## Data types
JS에는 8가지 기초적인 자료형이 있음  

변수는 여러 자료형을 저장할 수 있음  
아래 코드도 정상적으로 작동함  
```javascript
let message="hello";
message=1234;
```
- 위와 같은 것이 허용되는 것을 dynamically typed라고 함(data type이 존재하지만 변수는 어느 자료형에도 속하지 않음)

### Number
integer, float 등의 값들  
special numeric values도 존재함:
- `Infinity`, `-Infinity` : `1/0`, `Infinity` 등으로 선언 가능
	- 출력하면 Infinity라는 글자 그대로 나옴
- `NaN` : 틀리거나 정의되지 않은 연산을 할 때 나옴
	- `"asdf"/2` 등
	- `NaN`과의 모든 연산 결과는 `NaN`으로 출력됨

※ divide by zero, non-numeric에 대한 수학적 연산 등 일반적으로 허용되지 않는 연산을 하더라도 JS에서는 에러가 나오지 않음

### BigInt
`Number`은 `2^53 - 1` 초과의 수나 `-(2^53 -1)` 미만의 정수를 표현하지 못함  
`BigInt`는 임의의 길이의 정수를 표현하기 위해 최근에 추가된 자료형임  
정수의 끝에 `n`을 붙여서 `BigInt` value를 만들 수 있음

```javascript
const bigInt=123456486974865416541658654648541n;
```
- 현재는 Firefox, Chrome, Edge, Safari 등이 지원함(IE는 지원하지 않음)

### String
JS에서의 `String` 표현 방법 3가지:
1. Double quotes: `"Hello"`
2. Single quotes: `'Hello'`
3. Backticks: `` `Hello` ``

backtick을 이용하면 다른 변수나 식을 string 안에 넣을 수 있음  
아래와 같이 `${...}`의 형식을 이용  
```javascript
let name="John";
alert(`Hello, ${name}!`);
alert(`1+2=${1+2}`);
```

> JS에는 character type이 없음!

### Boolean(logical type)
`Boolean`은 `true`, `false` 두 가지 값만 가질 수 있음  
비교문의 결과가 boolean으로 출력됨  
```javascript
let isGreater=4>1;
alert(isGreater);
```

### The "null" value
`null`은 그 자체로 하나의 type임  
JS에서 `null`은 '존재하지 않는 객체로의 참조', 'null pointer'등의 의미를 가지지 않음  
'empty', 'value unknown' 등의 의미로 생각하면 됨  
```javascript
let age=null;
```

### The "undefined" value
`undefined`도 이 자체로 하나의 type임
'값이 대입되지 않음'의 의미로 생각하면 됨  
```javascript
let age;
alert(age);

/* separated scripts */

let age=100;
age=undefined;
alert(age);
```
- 두 script 모두 `undefined`를 출력함
- `null`은 비었다는 뜻으로 사용되고 `undefined`는 선언되었지만 아무런 값이 대입되지 않았을 때 사용하는 default initial value임

### Objects and Symbols
위의 모든 type들은 한 가지의 값만 저장하는 **primitive**임  
반면 object는 더 복잡한 데이터를 저장함

symbol은 object의 identifier를 생성할 때 사용함

### The typeof operator
`typeof` operator를 사용해서 특정한 변수의 type을 알 수 있음  
두 가지 syntax가 존재:
1. operator로 사용 : `typeof x`
2. function으로 사용 : `typoef(x)`

`typeof x`는 type name을 string으로 반환함

#### Example
```javascript
typeof undefined // "undefined"
typeof 0 // "number"
typeof 10n // "bigint"
typeof Math // "object"
typeof null // "object"
typeof alert // "function"
```

- `null`은 *object가 아니지만* 예전의 코드와 호환성을 위해서 `"object"`가 반환됨
- function은 `object` 타입에 속해있지만 `typeof`에서는 `"function"`을 리턴함(마찬가지로 이전의 JS와 호환성을 위해)

## Interaction: alert, promprt, confirm
`alert`, `prompt`, `confirm` 총 3가지의 browser-specific functions를 소개함

### alert
메시지를 띄우고 OK버튼을 누를 때까지 기다림  
메시지를 띄우는 창을 *modal window*라 부름
- *modal*이라는 단어는 유저들이 정해진 조건을 만족하기 전에는 다른 요소들과 상호작용할 수 없는 것을 말함(이 경우에는 OK버튼)

### prompt
```javascript
result=promprt(title[, default]);
```
와 같이 사용됨  
input field, OK, Cancel 두 버튼이 있는 modal window를 띄움  
- `title` : prompt(사용자에게 보여지는 메시지)
- `default` : input field의 초기값, optional

※ `[...]`는 parameter가 optional하다는 것을 나타냄

#### Example
JS:  
```javascript
let age = prompt('How old are you?', 100);

alert(`You are ${age} years old!`); // You are 100 years old!
```

|Result:|
|:---|
|![js-prompt](https://github.com/siriyaoff/MDN-note/blob/master/images/js-prompt.PNG?raw=true)|

- cancel을 누르거나 Esc로 창을 닫으면 `null`이 반환됨
- IE의 경우 default를 선언해놓지 않으면 default가 반환되어야 할 때 `"undefined"`를 반환함
	따라서 `''`와 같은 것을 default로 넣어놓는게 좋음

### confirm
```javascript
result=comfirm(question);
```
와 같이 사용됨  
`question`과 OK, Cancel 두 버튼이 있는 modal window를 띄움  
OK를 누르면 `true`, 아니면 `false` 반환

### Summary
`alert`, `prompt`, `confirm` 모두 modal window에 대해서 위치, 스타일을 수정할 수 없음  
browser에 따라 모두 다름  
chrome에서는 `prompt`가 제대로 작동하지 않음

## Type Conversions
대부분 operator, function들은 자동으로 값을 알맞은 타입으로 변환해줌  
예를 들어 `alert`는 자동으로 값을 `String` type으로 바꿔서 출력하고 mathematical operations는 값을 숫자로 바꿈

`object`에 대해서는 나중에 object to primitive conversion을 살펴볼 예정

### String Conversion
`String(value)` function을 이용해서 `String` type으로 conversion 가능

### Numeric Conversion
수학 함수나 식 안에서 자동으로 numeric conversion이 일어남  
예를 들어 `alert("6"/"2");`는 3을 출력함(`/`가 수학 연산자이기 때문)

`Number(value)`를 이용해서 명시적으로 conversion 가능  
Numeric conversion rules:

|Value|Becomes...|
|:---|:---|
|`undefined`|`NaN`|
|`null`|`0`|
|`true` and `false`|`1` and `0`|
|string|Trim 후 남아있는 string이 없으면 `0`, 아니면 숫자를 읽음, string에 숫자만 있는게 아니면 `NaN` 리턴|

#### Example
```javascript
alert(Number("   123   ")); // 123
alert(Number("123z")); // NaN
alert(Number(true)); //1
```

- `undefined`일 때 `NaN`, `null`일 때 `0`으로 리턴이 다른 것에 주의!!
- 대부분의 수학 연산자도 이러한 conversion을 수행함

### Boolean Conversion
논리 연산자에서 자동으로 일어나고, `Boolean(value)`를 이용해서 명시적으로 가능  
Boolean conversion rules:
- `0`, empty string(`""`), `null`, `undefined`, `NaN`과 같은 비었다는 의미의 값들은 `false`로 변환됨
- 다른 값들은 모두 `true`로 변환됨

※ `"0"`, `" "` 등 unempty string은 모두 `true`로 변환됨에 주의!(PHP에서는 `"0"`이 `false`로 반환됨)

## Basic operators, maths
### Terms: "unary", "binary", "operand"
- *operand* : 피연산자
- *unary* operator : 단항연산자
- *binary* operator : 이항연산자

### Maths
`+`, `-`, `*`, `/`, `%`, `**` 등이 지원됨  
`**` : exponentiation(python이랑 동일, 제곱근도 지원됨)

### String concatenation with binary `+`
```javascript
alert(2 + 2 + '1' ); // "41" and not "221"
alert('1' + 2 + 2); // "122" and not "14"
alert( 6 - '2' ); // 4, converts '2' to a number
alert( '6' / '2' ); // 3, converts both operands to numbers
```
- `+` 연산자의 경우 `String`, `Number` type이 둘 다 존재하면 concatenation으로 취급됨
	- 계산 순서에 유의(교환법칙 성립하지 않음!)
- 다른 수학 연산자들은 모두 `String`이 `Number`로 conversion된 후 계산됨

### Numeric conversion, unary `+`
`Number` 타입에 대해서는 아무런 영향이 없지만, 다른 타입들에 대해선 `Number`로 conversion을 실행함  
`Number(...)` function과 동일  
아래와 같이 `String` type으로 표현된 숫자들을 더할 때 유용함  
```javascript
let apples="2";
let oranges="3";

alert( apples + oranges ); // "23", the binary plus concatenates strings

// both values converted to numbers before the binary plus
alert( +apples + +oranges ); // 5
```
- unary +가 연산자 우선순위가 더 높음

### Operator precedence
JS에서는 precedence number가 클 수록 우선순위가 큼

### Assignment
#### Assignment `=` returns a value
`x=value`는 `x`에 `value`를 대입한 후 그걸 반환함  
따라서 `let c=3-(a=b+1);`와 같은 statement도 가능

#### Chaining assignments
대입 연산자를 연속으로 사용하면 오른쪽에서 왼쪽으로 계산됨  
(`a=b=c=2+2;`와 같이)

### Modify-in-place
`+=`, `*=`와 같은 것들

### Increment/decrement
`++`, `--`  

### Bitwise operators
`&`, `|`, `^`, `~`, `<<`, `>>`, `>>>`  
`>>>` : zero-fill right shift

### Comma
`,`를 이용해서 여러 식을 쓸 수 있지만, 모두 계산된 뒤 맨 마지막 것만 리턴됨  
예를 들어 `let a=(1+2, 3+4);`를 실행하면 `a`에는 `7`이 저장됨  
`a=1, b=3, c=a*b`도 가능함(위에는 괄호때문에 대입이 가장 나중에 실행됨)

comma가 우선순위 값이 가장 낮음

### Tasks
- `" \t \n" -2`는 `-2`가 반환됨
	- space characters는 모두 trim되고 난 후 conversion이 일어나기 때문

## Comparisons
### Boolean is the result
모든 비교 연산자들은 `boolean`을 리턴함

### String comparison
string도 비교가 가능함(사전 순으로)  
사전 순으로 뒤쪽에 올수록 더 큰 것으로 취급됨  
`Bee` > `Be` : `true`

※ 사실 unicode 순서이기 때문에 알파벳의 경우 소문자가 더 크다고 판단함

### Comparison of different types
비교하는 값들의 type이 다를 경우 값들을 `Number`로 변환해서 비교함  

#### Example
```javascript
alert('2'>1); // true;
alert('01'==1); // true;
alert(false==0); // true;

let a=0;
alert(Boolean(a)); // false

let b='0';
alert(Boolean(b)); // true

alert(a==b); // true
```
- `"0"==0`의 결과가 `true`임에 유의!

### Strict equality
equal 연산자 `==`는 아래의 조건문처럼 `0`, `false`, `''`을 구별하지 못함  
```javascript
alert( 0 == false ); // true
alert( '' == false ); // true
```

A **strict equality operator** `===` checks the equality **without type conversion**  
=> `===`는 비교하는 두 operand의 type이 다를 경우 바로 `false`를 반환함

strict non-equality operator `!==`도 존재함

### Comparison with null and undefined
`null`이나 `undefined`가 비교 대상으로 사용될 때는 예상치 못한 결과가 나올 수도 있음

```javascript
alert(null===undefined); // false
alert(null==undefined); // true
alert(null==0); // false
alert(undefined==0); // false
```
- `==` 연산자를 사용할 때 `null`와 `undefined`는 둘을 비교할 때만 `true`를 반환, 다른 값과 비교할 때는 모두 `false`를 반환함!!
- `<`, `>`, `<=`, `>=`와 같은 다른 비교 연산자들에서는 `null`은 `0`으로, `undefined`는 `NaN`으로 변환되어 비교됨

#### Strange result: `null` vs `0`
```javascript
alert( null > 0 );  // (1) false
alert( null == 0 ); // (2) false
alert( null >= 0 ); // (3) true
```
- 위에서 설명했듯이 `null`은 `undefined` 이외의 값과 `==` 연산을 하면 `false`가 나오기 때문에 (2)의 결과가 나옴
- 나머지 비교 연산자에서는 `0`으로 변환된 후 비교되기 때문에 (3)의 결과가 나옴

#### An incomoparable undefined
`undefined`는 다른 값들과 비교하면 안됨

```javascript
alert( undefined > 0 ); // false (1)
alert( undefined < 0 ); // false (2)
alert( undefined == 0 ); // false (3)
```
- (3)은 `null`을 넣었을 때와 같은 이유임
- (1), (2)는 `undefined`가 `NaN`으로 변환되어 비교되기 때문임

#### Avoid problems
- `undefined` 또는 `null`과의 비교문은 주의해서 사용해야 함!(`===` 제외)
- `null` 또는 `undefined`가 들어갈 수 있는 변수에 대해선 case를 나눠서 처리

### Tasks
- `"2">"12"` : `true`
	- 둘 다 string이기 때문에 number로 변환되어 비교되지 않음
	- `2>"12"`로 바꾸면 `false`가 됨

## Conditional branching: if, '?'
### The "if" statement
### Boolean conversion
### The "else" clause
### Several conditions: "else if"
### Conditional operator `?`
C와 같음

### Multiple `?`
```javascript
let age = prompt('age?', 18);

let message = (age < 3) ? 'Hi, baby!' :
  (age < 18) ? 'Hello!' :
  (age < 100) ? 'Greetings!' :
  'What an unusual age!';
```
- if else와 같음

### Non-traditional use of `?`
```javascript
let company = prompt('Which company created JavaScript?', '');

(company == 'Netscape') ?
   alert('Right!') : alert('Wrong.');
```
- 아예 statement를 넣을 수도 있음
- 가독성이 떨어지기 때문에 알고만 있으면 될 듯

### Tasks
- `String`과 `Number`를 비교할 때는 `String`을 캐스팅하지 않아도 됨(`Number`이 있어서 자동으로 변환됨)

## Logical operators
JS에는 `||`, `&&`, `!`, `??`, 총 4개의 논리 연산자가 존재함  
이 article에서는 앞 3개만 다룸  
모든 type에 적용 가능하고, 결과 또한 모든 타입이 될 수 있음

### `||`(OR)
모든 operand가 조건문이거나 `boolean`일 경우 계산 후 `true` / `false`를 반환함  
=> C에서와 동일하게 논리 연산자로 사용 가능

### OR `||` finds the first truthy value
```javascript
result = value1 || value2 || value3;
```
- 위의 코드에서 `||`는 다음과 같이 작동함
	- 왼쪽에서 오른쪽 순서로 operand를 계산
	- 순서대로 계산하면서 결과가 `true`면 그 operand의 원래 값을 반환
	- 만약 모든 operand가 계산되면(모든 결과가 `false`면), 마지막 operand를 반환
- operand가 다른 type일지라도 위의 설명처럼 논리 연산자로 사용 가능

boolean-only OR과 비교해서 다음과 같은 용도로 사용됨
1. 변수들과 식들의 리스트 중 첫 번째 truthy를 구함
	```javascript
	let firstName = "";
	let lastName = "";
	let nickName = "SuperCoder";

	alert( firstName || lastName || nickName || "Anonymous"); // SuperCoder
	```
	- 만약 모든 값들이 falsy라면 `"Anonymous"`가 출력됨
2. Short-circuit evaluation
	각 operand들을 순서대로 계산하면서 truthy를 마주치면 바로 그 operand를 반환하는 성질을 이용  
	```javascript
	true || alert("not printed");
	false || alert("printed");
	```
	- 왼쪽 operand가 falsy일 때만 실행되는 statement를 만들 때 사용됨

### `&&`(AND)
operand가 모두 boolean일 때는 C와 동일하게 사용됨

### AND `&&` finds the first falsy value
```javascript
result = value1 && value2 && value3;
```
- 위의 코드에서 `&&`는 위의 `||`와 반대로 작동함
	- 왼쪽에서 오른쪽 순서로 operand를 계산
	- 순서대로 계산하면서 결과가 `false`이면 그 operand의 원래 값을 반환
	- 만약 모든 operand가 계산되면(모든 결과가 `ture`면), 마지막 operand를 반환
- 마찬가지로 논리연산자로 사용 가능(애초에 falsy가 반환되면 조건문 실행이 안됨)

#### Example
```javascript
alert( 1 && 2 && null && 3 ); // null
alert( 1 && 2 && 3 ); // 3, the last one
```

※ `&&`가 `||`보다 우선순위가 높음

아래 코드와 같이 `if`문을 `||`, `&&`를 이용해서 대신할 수 있지만 각각의 목적에 맞게 사용하는게 가독성을 높여줌  
```javascript
let x = 1;

(x > 0) && alert( 'Greater than zero!' );
```

### `!`(NOT)
C와 같음

아래와 같이 `!!`를 이용해서 값을 `boolean`으로 바꿀 수 있음  
```javascript
alert( !!"non-empty string" ); // true
alert( !!null ); // false
```
- `Boolean(...)`를 사용하는 것보다 간단함
- `!`는 모든 논리 연산자 중에 가장 우선순위가 높음

### Tasks
- `alert` 함수는 아무런 값을 반환하지 않기 때문에 operand로 사용될 경우 `undefined`를 반환함

```javascript
alert(alert(1) && alert(2));
```
- 위 코드를 실행하면 `1`이 출력된 후 `undefined`가 출력됨
	- `alert`가 `undefined`를 반환하기 때문에 `1`을 출력하고 `alert`의 리턴값을 반환하고 끝남

## Nullish coalescing operator `??`
`null`이나 `undefined`가 아니면 "defined"라고 부름  
`a ?? b`:
- `a`가 defined => `a` 리턴
- `a`가 defined가 아님 => `b` 리턴

⇔  
```javascript
(a !== null && a !== undefined) ? a : b
```

아래 코드와 같이 사용 가능함  
```javascript
let firstName = null;
let lastName = null;
let nickName = "Supercoder";

// shows the first defined value:
alert(firstName ?? lastName ?? nickName ?? "Anonymous"); // Supercoder
```

### Comparison with `||`
위 예시는 `||`로 대체 가능함  
`||`는 JS가 개발될 때부터 존재했고, `??`는 최근에 생김  
두 연산자의 차이점은 아래와 같음
- `||` : first *truthy* value 리턴
	- `false`, `0`, `""`, `null/undefined`를 구별하지 않음
- `??` : first *defined* value 리턴
	- `null/undefined`를 다른 falsy value와 구별함  
		=> 값이 진짜로 비어있거나 설정되지 않았는지 판단 가능

#### Example
```javascript
let height = 0;

alert(height || 100); // 100
alert(height ?? 100); // 0
```
- 위 예시에서는 값이 0으로 설정되었기 때문에 `??`를 이용하는 것이 올바른 결과를 출력함
- `a=a?100;`와 같이 변수의 초깃값을 설정할 때 사용 가능

### Precedence
`??`(5)는 `||`(6)보다 우선순위가 1단계 낮음(괄호 안은 precedence value, 높을수록 우선순위가 높음)  
=> `=`, `?` 전에, `+`, `*` 등 보다 뒤에 계산됨  
=> `let area = (height ?? 100) * (width ?? 50)`와 같이 사용해야 함

#### Using `??` with `&&` or `||`
JS에서는 `??`를 `&&`나 `||`와 같이 사용하는 것을 금지함(괄호로 묶어서 명시적으로 우선순위를 정했을 때는 가능)  
즉 아래의 두 번째 줄과 같이 사용해야 함

```javascript
let x = 1 && 2 ?? 3; // Syntax error
let x = (1 && 2) ?? 3; // Works
```
- `??`가 생기고나서 사람들의 혼동을 방지하기 위해 이런 제한이 생김

## Loops: while and for
### The "while" loop
### The "do...while" loop
### The "for" loop
C와 같음

### Continue to the next iteration
ternary operator `?`를 사용할 때 expression이 아닌 것들은 사용할 수 없음  
예를 들어 아래와 같은 코드는 syntax error가 남

```javascript
(i > 5) ? alert(i) : continue; // continue isn't allowed here
```
- `if`대신 `?`를 사용하면 안되는 이유 중 한가지임

### Labels for break/continue
label을 이용해서 break/continue할 위치를 정할 수 있음

```javascript
outer:
for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`Value at coords (${i},${j})`, '');

    // if an empty string or canceled, then break out of both loops
    if (!input) break outer; // (*)

    // do something with the value...
  }
}
alert('Done!');
```
- `break <labelName>`을 사용하면 `<labelName>`이 붙어 있는 곳을 빠져나감
- `continue`도 label을 동일하게 적용 가능

label이 모든 곳으로 jump시켜주는 것은 아님!  
아래 코드와 같이 사용할 수 없음  
```javascript
break label; // jump to the label below (doesn't work)

label: for (...)
```

`break`는 code block안에 위치해야 함!!  
아래와 같이 반복문 없이도 사용 가능함(`continue`는 불가능)  
```javascript
label: {
  // ...
  break label; // works
  // ...
}
```

### Tasks
- `(i%2)||alert(i);`로 짝수 출력 가능
- `prompt`에서 사용자가 cancel을 누르면 `null`이 들어감  
	=> `null`은 `0`으로 변환되는 것에 주의!!!

## The "switch" statement
### The syntax
### Grouping of "case"
C와 같음

### Type matters
`case a:`와 같이 equality check일 때는 항상 strict equality operator `===`를 사용함!!  
따라서 `switch`의 변수와 `case`의 비교 대상의 type이 다르면 실행이 되지 않음(`3`, `"3"`과 같이)

## Functions
### Function Declaration
### Local variables
### Outer variables
C와 같음

### Parameters
Call by value가 적용됨

### Default values
아래와 같이 parameter에 default value 선언 가능  
```javascript
function showMessage(from, text = anotherFunction()) {
  // anotherFunction() only executed if no text given
  // its result becomes the value of text
}
```

#### Alternative default parameters
함수 내부에서 아래와 같이 기본값을 선언 가능함  
```javascript
// 1
if (text === undefined) {
  text = 'empty';
}

// 2
text = text || 'empty';

// 3
text = count ?? 'empty'
```
- 상황에 따라 맞게 설정해야 함  
	예를 들어 0도 입력으로 들어올 수 있는 경우 `||` 대신 `??` 사용해야 함

### Returning a value
`return;` 또는 `return`을 사용하지 않으면 `undefined`를 리턴함

```javascript
return
 (some + long + expression + or + whatever * f(a) + f(b))
```
- 위와 같이 `return` 다음 줄을 바꾸고 리턴값을 적으면 `return;`와 같음
	=> 긴 식을 리턴하고 싶을 때는 `return (`와 같이 괄호를 `return`과 같은 줄에 적어야 함

### Naming a function
### Functions == Comments
함수가 복잡한 구현이 필요할 경우 여러 함수들로 세분화하는게 나음  
=> 재사용이 많이 되지 않아도 코드의 가독성을 위해서 함수를 선언하는게 나음

### Tasks
- `?`에는 `return`이 operand로 들어갈 수 없음
- `**` 연산자는 소숫점도 지원됨

## Function expressions
JS에서 function은 값으로도 취급됨  
Function Expression : `function() {...}`을 expression처럼 사용하는 것  
아래와 같이 *Function Expression*을 사용 가능함  
```javascript
let sayHi = function() {
  alert( "Hello" );
};

alert(sayHi); // shows the function code
```
- 다른 값들처럼 출력도 가능함
	- `sayHi()`로 함수가 호출된게 아니기 때문에 함수가 실행되지 않음
- function declaration이 아니라 function expression으로 선언할 경우 맨 뒤에 `;`가 붙는 것에 주의!!

함수가 값으로 취급될 수 있기 때문에 아래와 같이 복사도 가능함  
```javascript
function sayHi() {   // (1) create
  alert( "Hello" );
}

let func = sayHi;    // (2) copy

func(); // Hello     // (3) run the copy (it works)!
sayHi(); // Hello    //     this still works too (why wouldn't it)
```
- `func==sayHi`는 `ture`임
	(∵ sayHi의 코드를 다 복사하기 때문에 같음)

### Callback functions
함수 a의 parameter로 다른 함수 b, c를 넣어서  
함수 b, c가 함수 a에서 필요시 실행될 수 있음  
이 때 함수 b, c를 함수 a의 *callback functions* 또는 *callbacks*라고 함

#### Example
```javascript
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

function showOk() {
  alert( "You agreed." );
}

function showCancel() {
  alert( "You canceled the execution." );
}

// usage: functions showOk, showCancel are passed as arguments to ask
ask("Do you agree?", showOk, showCancel);
```
- JS에서 function은 *action*을 나타낸다고 생각하면 됨(cf. value는 *data*를 나타냄)  
	=> variable처럼 다루고 필요할 때 실행시킬 수 있음

아래와 같이 function expression으로 구현할 수도 있음

```javascript
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

ask(
  "Do you agree?",
  function() { alert("You agreed."); },
  function() { alert("You canceled the execution."); }
);
```
- 더 간단한게 구현 가능
- `ask`를 호출하는 statement 안에서 선언되었고, 이름도 없기 때문에 밖에서 사용할 수 없음(*anonymous*라고 부름)

### Function Expression vs Function Declaration
syntax 이외에도 JS engine에 의한 함수 생성 시점이 다름
- Function Expression은 statement를 실행할 때 생성되고 그때부터 호출 가능함
- Function Declaration은 선언부보다 위에서도 호출 가능함

Function Declaration은 명시된 scope도 중요함
- block scope 선언되었다면 그 block 안에서만 호출 가능함

Function Expression을 이용해서 아래와 같이 Declaration으로는 불가능한 것을 구현할 수 있음  
```javascript
let welcome = (age < 18) ?
  function() { alert("Hello!"); } :
  function() { alert("Greetings!"); };

welcome(); // ok now
```

> Function Declaration과 Function Expression을 선택하는 방법:  
> 가능하면 Function Declaration을 사용하는게 나음(가독성 ↑, 가용성 ↑)  
> conditional declaration이 필요하거나 다른 이유로 Function Declaration이 맞지 않을 경우 Function Expression을 사용하면 됨

## Arrow functions, the basics
아래 두 코드는 같은 함수를 만듦  
```javascript
let func = (arg1, arg2, ..., argN) => expression;

let func = function(arg1, arg2, ..., argN) {
  return expression;
};
```
- parameter가 없어도 `()`로 표시해줘야 함
- Function Expression처럼 value로 사용 가능
	```javascript
	let welcome = (age < 18) ?
	  () => alert('Hello') :
	  () => alert("Greetings!");

	welcome();
	```
- one-line action을 구현할 때 효율적임

### Multiline arrow functions
curly braces로 expression을 여러 줄로 늘릴 수 있음  
```javascript
let sum = (a, b) => {  // the curly brace opens a multiline function
  let result = a + b;
  return result; // if we use curly braces, then we need an explicit "return"
};
```
- `{}`를 사용하면 반드시 `return`이 있어야 함


# Code quality
## Debugging in Chrome
Debugging : process of finding and fixing errors within a script

### The "Sources" panel
File navigator, code editor, JavaScript debugging pane이 존재

### Console
`Esc`를 누르면 console창이 열림

### Breakpoints
line number를 클릭해서 설정 가능함  
Breakpoints panel에서 breakpoint들을 확인 가능함

※ line number를 오른쪽 클릭해서 conditional breakpoint를 설정 가능함(지정한 조건이 만족할 때만 멈춤)

### Debugger command
`debugger;` statement를 script에 넣어서 breakpoint를 만들 수도 있음  
=> browser을 킬 필요 없이 code editor에서 바로 중단점 설정 가능

### Pause and look around
Debugging pane의 탭에서 여러 가지 정보를 확인 가능
- Watch 탭 : expression의 현재 값을 보여줌
- Call Stack 탭 : 호출 스택을 보여줌
	- 가장 밑에는 script가 있는 파일이 anonymous로 있음
- Scope 탭 : 변수들을 scope로 분류해서 보여줌

### Tracing the execution
- Resume
	- hotkey : `F8`
	- 실행을 재개함
- Step
	- hotkey : `F9`
	- 다음 statement 하나를 실행함
- Step over
	- hotkey : `F10`
	- 다음 statement 하나를 실행하지만, 그게 직접 정의한 함수의 호출이면 넘김
- Step into
	- hotkey : `F11`
	- Step은 async action을 무시하지만 step into는 asynchronous function call도 고려해서 비동기적인 함수가 호출되면 그 함수의 코드를 차례대로 실행함(interrupt를 허용하는 느낌)
- Step out
	- hotkey : `Shift + F11`
	- 현재 함수의 끝까지 실행함

※ Continue to here을 이용하면 바로 원하는 줄로 갈 수 있음

### Logging
`console.log` 함수를 이용해서 값의 변화를 볼 수 있음  
console이 열려있어야 출력됨

#### Example
```javascript
for (let i = 0; i < 5; i++) {
  console.log("value,", i);
}
```
- console에 `"value,", 0` 이런 형태로 한 줄씩 출력됨

### Summary
script를 멈추는 3가지 주요 방법:
1. breakpoint
2. `debugger` statement
3. error(dev tool이 열려있고 automatic pause가 활성화되어 있어야 함)

## Coding Style
### Syntax
JS는 indentation으로 space 2개를 사용

#### Curly Braces
"Egyptian" style을 주로 사용함(`{`는 같은 줄, `}`는 다른 줄

#### Line Length
`` ` ``은 string에 줄바꿈을 허용함  
최대 줄 길이를 정해놓는게 좋음(80 - 120 글자 정도)

#### Indents
Horizontal indents : 2 or 4 spaces

#### Semicolons
#### Nesting Levels
nesting을 너무 많이 하지 않는게 좋음(`continue`나 `return`등을 사용해서)

### Function Placement
보통 코드를 먼저 쓰고 함수 정의를 나중에 쓰는 경우가 많음  
(∵ 함수가 어떤 역할인지 알면 읽을 필요가 없기 때문)

### Style Guides
- Google JS Style Guide
- Airbnb JS Style Guide
- Idiomatic.JS
- StandardJS

등의 style guides가 존재함

### Automated Linters
- JSLint
- JSHint
- ESLint

등의 Linter가 존재  
code style 뿐만 아니라 오타도 찾아줌  
대부분 editor와 함께 통합되어 있음  
Node.js에서 ESLint를 설치하는 방법:
1. Node.js 설치
2. `npm install -g eslint`로 ESLint 설치
3. `.eslintrc` 파일을 JS project root에 생성
4. plugin 허용

`.eslintrc`의 예시:  
```
{
  "extends": "eslint:recommended",
  "env": {
    "browser": true,
    "node": true,
    "es6": true
  },
  "rules": {
    "no-console": 0,
    "indent": 2
  }
}
```
- `extends`로 기본적으로 따를 설정을 정하고 밑에 직접 정의

## Comments
### Bad comments
코드의 작동 방식을 설명함

만약 코드가 불분명하고 주석이 필요하다면 다시 쓰는게 나을 수도 있음

#### Recipe: factor out functions
한 기능을 하는 코드를 함수로 대체

#### Recipe: create functions
코드가 길다면 함수로 대체

위와 같은 방법들은 함수 이름으로 기능을 파악하고 바로 다음 부분으로 넘어가게 해주기 때문에 코드의 가독성을 높여줌

### Good comments
#### Describe the architecture
어떻게 코드가 서로 상호작용하는지, control flow가 어떻게 흘러가는지 등을 UML을 이용해서 제공

#### Document function parameters and usage
JSDoc이라는 syntax를 이용해서 주석으로 함수의 용도, 인자, 리턴값을 문서화할 수 있음

위와 같은 방법들은 함수의 목적과, 코드를 보지 않고 알맞게 사용하는 방법을 제공함  
WebStorm, JSDoc3등에 이런 기능이 있음

#### Why is the task solved this way?
어떤 문제가 (특히 가장 명확한 방법이 아닌) 특정한 방법으로 풀렸을 때 주석을 제공해야 함

#### Any subtle features of the code? Where they are used?

### Summary
#### Comment this:
- Overall architecture, high-level view
- Function usage
- Important solutions, especially when not immediately obvious

#### Avoid comments
- That tell "how code works" and "what it does"
- Put them in only if it's impossible to make the code so simple and self-descriptive that it doesn't require them

## Ninja code
프로젝트에서는 숏코딩, 변수 재사용 등 금지

## Automated testing with Mocha
### Why do we need tests?
직접 돌려가면서 테스트를 하면, 인자가 다르게 들어왔을 때 잘못된 결과가 나오게 고치는 등의 실수를 할 수 있음

자동화된 테스트는 코드와 별도로 테스트 케이스들을 작성하고 테스트해서 예상 결과와 비교함

### Behavior Driven Development(BDD)
BDD : tests AND documentation AND examples

BDD를 이해하기 위해 실제 개발 사례를 살펴보자

### Development of "pow": the spec
`n>=0`이라 가정하고 `x`를 `n`제곱한 결과를 리턴하는 `pow(x, n)` 함수를 만든다고 가정해보자.  
함수를 구현하기 전에 이 함수의 기능을 정의하고 표현해야 함    
=> *specification*(명세서)으로 함수의 개요와 사용 방법을 제공할 수 있음:  
```javascript
describe("pow", function() {

  it("raises to n-th power", function() {
    assert.equal(pow(2, 3), 8);
  });

});
```
- `describe("title", function() { ... })`
	구현하려는 기능에 대한 설명을 넣음  
	`it` 여러 개가 들어갈 수도 있기 때문에 function expression을 사용함
- `it("use case description", function() { ... })`
	title에는 사용 방법을 자연어로 적음  
	두 번째에는 use case test함수를 넣음
- `assert.equal(value1, value2)`
	`assert.*` 함수는 `pow`가 예상대로 동작하는지 확인해줌  
	위 예시에서는 `assert.equal`을 사용함  
	=> 두 값이 일치하는지 비교, 그렇지 않으면 에러를 출력

※ specification은 실행할 수 있음

### The development flow
1. An initial spec is written, with tests for the most basic functionality
2. An initial implementation is created
3. To check whether it works, we run the testing framework Mocha that runs the spec. While the functionality is not complete, errors are displayed. We make corrections until everything works
4. We add more use cases to the spec, probably not yet supported by the implementations. Tests start to fail
5. Go to 3, update the implementation till tests give no errors
6. Repeat steps 3-5 till the functionality is ready

### The spec in action
`pow` 함수의 initial spec와 JS libraries를 이용해서 spec을 실행해보자  
아래의 라이브러리들을 사용할 예정:
- Mocha : core framework, `describe`, `it` 등의 함수 제공
- Chai : assertion에 관한 라이브러리
- Sinon : a library to spy over functions

위 라이브러리들은 in-browser과 server-side 모두에서 사용 가능함

#### Example
The full HTML page with these frameworks and `pow` spec:  
```javascript
<!DOCTYPE html>
<html>
<head>
  <!-- add mocha css, to show results -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/mocha/3.2.0/mocha.css">
  <!-- add mocha framework code -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/mocha/3.2.0/mocha.js"></script>
  <script>
    mocha.setup('bdd'); // minimal setup
  </script>
  <!-- add chai -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/chai/3.5.0/chai.js"></script>
  <script>
    // chai has a lot of stuff, let's make assert global
    let assert = chai.assert;
  </script>
</head>

<body>

  <script>
    function pow(x, n) {
      /* function code is to be written, empty now */
    }
  </script>

  <!-- the script with tests (describe, it...) -->
  <script src="test.js"></script>

  <!-- the element with id="mocha" will contain test results -->
  <div id="mocha"></div>

  <!-- run tests! -->
  <script>
    mocha.run();
  </script>
</body>

</html>
```

|Result:|
|:---|
|![js-spec-in-action1](https://github.com/siriyaoff/MDN-note/blob/master/images/js-spec-in-action1.PNG?raw=true)|

- `let assert=chai.assert;`로 chai의 assert 함수들을 사용
- `.mocha` div에 테스트 결과가 표시됨
- 지금은 `pow()`가 구현되지 않은 상태이기 때문에 에러가 출력됨

### Initial implementation
`pow` 함수를 아래와 같이 구현:  
```javascript
function pow(x, n) {
  return 8; // :) we cheat!
}
```

|Result:|
|:---|
|![js-spec-in-action2](https://github.com/siriyaoff/MDN-note/blob/master/images/js-spec-in-action2.PNG?raw=true)|

- `it`의 ㅕㅕ `it` 함수의 두 번째 인자를 볼 수 있음

### Improving the spec
spec에 test를 추가하는 두 가지 방법:
1. 같은 `it` block에 추가 - test case를 추가함
	```javascript
	describe("pow", function() {

	  it("raises to n-th power", function() {
		assert.equal(pow(2, 3), 8);
		assert.equal(pow(3, 4), 81);
	  });

	});
	```
	
	|Result:|
	|:---|
	|![js-spec-in-action3](https://github.com/siriyaoff/MDN-note/blob/master/images/js-spec-in-action3.PNG?raw=true)|
2. `it` block을 추가 - test를 하나 더 만듦
	```javascript
	describe("pow", function() {

	  it("2 raised to power 3 is 8", function() {
		assert.equal(pow(2, 3), 8);
	  });

	  it("3 raised to power 4 is 81", function() {
		assert.equal(pow(3, 4), 81);
	  });

	});
	```
	
	|Result:|
	|:---|
	|![js-spec-in-action4](https://github.com/siriyaoff/MDN-note/blob/master/images/js-spec-in-action4.PNG?raw=true)|

두 방법의 가장 큰 차이점 : `assert`가 에러를 발생시키는 시점  
=> 첫 번째 방법은 첫 번째 `assert`가 에러나면 두 번째 `assert`는 아예 실행되지가 않아서 결과를 알 수 없음  
따라서 두 번째 방법을 사용하는 것이 나음  
(+ 하나의 test에는 하나만 체크하는게 좋음)

### Improving the implementation
`pow`를 아래와 같이 구현:  
```javascript
function pow(x, n) {
  let result = 1;

  for (let i = 0; i < n; i++) {
    result *= x;
  }

  return result;
}
```

`it`를 자동으로 생성되게 구현:  
```javascript
describe("pow", function() {

  function makeTest(x) {
    let expected = x * x * x;
    it(`${x} in the power 3 is ${expected}`, function() {
      assert.equal(pow(x, 3), expected);
    });
  }

  for (let x = 1; x <= 5; x++) {
    makeTest(x);
  }

});
```

|Result:|
|:---|
|![js-spec-in-action5](https://github.com/siriyaoff/MDN-note/blob/master/images/js-spec-in-action5.PNG?raw=true)|

### Nested describe
`it`를 추가해서 test 안에 test case를 추가할 수 있지만, 아예 `describe`를 중첩해서 test를 추가할 수도 있음:  
```javascript
describe("pow", function() {

  describe("raises x to power 3", function() {

    function makeTest(x) {
      let expected = x * x * x;
      it(`${x} in the power 3 is ${expected}`, function() {
        assert.equal(pow(x, 3), expected);
      });
    }

    for (let x = 1; x <= 5; x++) {
      makeTest(x);
    }

  });

  // ... more tests to follow here, both describe and it can be added
});
```

|Result:|
|:---|
|![js-spec-in-action6](https://github.com/siriyaoff/MDN-note/blob/master/images/js-spec-in-action6.PNG?raw=true)|

`before`, `after`, `beforeEach`, `afterEach`를 이용해서 `it` 실행 전/후로 실행될 내용을 정의 가능:  
```javascript
describe("test", function() {

  before(() => alert("Testing started – before all tests"));
  after(() => alert("Testing finished – after all tests"));

  beforeEach(() => alert("Before a test – enter a test"));
  afterEach(() => alert("After a test – exit a test"));

  it('test 1', () => alert(1));
  it('test 2', () => alert(2));

});
```

Result:  
```
Testing started – before all tests (before)
Before a test – enter a test (beforeEach)
1
After a test – exit a test   (afterEach)
Before a test – enter a test (beforeEach)
2
After a test – exit a test   (afterEach)
Testing finished – after all tests (after)
```

- 카운터를 0으로 설정하는 것과 같이 테스트 사이에 초기화를 할 때도 사용됨

### Extending the spec
`pow(x, n)`은 `n`이 양수라 가정하기 때문에 이외의 값이 들어오면 `NaN`이 출력되도록 먼저 spec을 확장:  
```javascript
describe("pow", function() {

  // ...

  it("for negative n the result is NaN", function() {
    assert.isNaN(pow(2, -1));
  });

  it("for non-integer n the result is NaN", function() {
    assert.isNaN(pow(2, 1.5));
  });

});
```

|Result:|
|:---|
|![js-spec-in-action7](https://github.com/siriyaoff/MDN-note/blob/master/images/js-spec-in-action7.PNG?raw=true)|

- JS에서는 보통 에러를 `NaN`으로 표현
- 현재는 n이 양수일 경우만 구현하고 예외처리를 하지 않았기 때문에 테스트가 실패함(`NaN` 리턴하지 않음)

#### Other assertions
- `assert.isNaN(value)` : checks that `value === NaN`
- `assert.equal(value1, value2)` : checks the equality `value1 == value2`
- `assert.strictEqual(value1, value2)` : checks the strict equality `value1 === value2`
- `assert.notEqual`, `assert.notStrictEqual` : inverse checks to the ones above
- `assert.isTrue(value)` : checks that `value === true`
- `assert.isFalse(value)` : checks that `value === false`

`pow`에 예외처리를 위해 아래 코드를 추가:  
```javascript
  if (n < 0) return NaN;
  if (Math.round(n) != n) return NaN;
```

|Result:|
|:---|
|![js-spec-in-action8](https://github.com/siriyaoff/MDN-note/blob/master/images/js-spec-in-action8.PNG?raw=true)|

### Summary
BDD에 따르면, spec을 먼저 작성하고 난 다음에 기능을 구현함  
spec은 3가지 용도로 사용될 수 있음:
1. As Tests
2. As Docs
3. As Examples

well-tested code has better architecture  
(∵ 함수의 기능, 입력, 출력을 정의한 다음 구현하기 때문)

### Tasks
`it`는 iteration의 약자라고 생각하면 될 듯(하나의 `it`에 하나의 테스트 케이스만)  
`it.only()`를 사용하면 sibling인 `it`가 있어도 `it.only()`만 실행함

## Polyfills and transpilers
JS에서 새로운 제안이 가치있다고 판단되면 ecma 리스트에 추가되고 specification으로 처리됨  
최신의 코드가 오래된 엔진에서 돌아가게 하기 위해서 Transpilers, Polyfills를 사용함

### Transpilers
modern code를 parse하고 결과가 같도록 older syntax로 다시 써주는 프로그램  
e.g. 2020년 이전에는 `??`가 존재하지 않았기 때문에 바꿈

보통 transpiler를 돌린 코드를 서버로 deploy함  
[Babel](https://babeljs.io/)이 인기있는 transpiler임  
webpack같은 modern project build system에서 'provide'가 transpiler을 자동으로 돌리는 옵션임

### Polyfills
`Math.trunc(n)`과 같이 새로운 내장 함수가 추가되기도 하는데, 오래된 JS engine에서는 이런 새로 추가된 내장 함수가 지원되지 않기 때문에 에러가 남  
문법이 바뀐게 아니기 때문에 transpile할 수 없고 아예 새로 선언해야 함  
=> 새로운 기능을 업데이트하거나 추가해주는 script를 *polyfill*이라고 함  
(It "fills in" the gap and adds missing implementation)

`if(!Math.trunc)`와 같이 함수가 있는지 판별 가능  
JS에서는 built-in function도 수정이 가능함  
polyfill을 지원하는 libraries:
- core js
- polyfill.io

※ Chrome이 대부분 최신 기능을 가장 먼저 지원함


# Objects: the basics
## Objects
object는 `{...}` 안에 `key: value`와 같이 properties를 선언함으로써 만들어짐  
empty object는 object constructor, object literal, 두 가지 방법으로 만들 수 있음:  
```javascript
let user = new Object(); // "object constructor" syntax
let user = {};  // "object literal" syntax
```
- 보통 object literal로 객체를 선언함

### Literals and properties
처음 선언할 때 아래와 같이 property를 선언할 수 있음:  
```javascript
let user = {     // an object
  name: "John",  // by key "name" store value "John"
  age: 30,        // by key "age" store value 30
  "likes birds": true,
};
```
- 따옴표를 사용하면 property 이름으로 여러 단어를 사용할 수 있음!
- `user.isAdmin=true;`와 같이 선언한 이후에도 property를 추가할 수 있음
- 마지막 줄에도 `,`를 남기는 것을 "trailing" or "hanging" comma라고 함  
	=> properties를 쉽게 수정할 수 있음

`delete user.age;`와 같이 `delete` operator를 이용해서 property를 삭제할 수 있음

### Square brackets
multiword properties의 경우 `user.likes birds`로 호출할 수 없음  
(∵ `.`으로 호출하기 위해선 valid variable identifier이어야 함(공백 없음, 숫자로 시작 x, 특수문자 x)  
=> `user.["likes birds"]`와 같이 square bracket notation을 이용해서 호출해야 함

key도 string이기 때문에 아래와 같이 string을 이용해서 호출도 가능함  
```javascript
let key = "likes birds";

// same as user["likes birds"] = true;
user[key] = true;
```
- `user.key`로는 호출할 수 없음에 주의!!
- python의 dictionary처럼 property를 추가할 수 있다고 생각하면 될 듯

#### Computed properties
object literal으로 객체를 선언할 때 `[]`를 사용할 수 있음  
이렇게 선언된 property를 *computed property*라고 함  
```javascript
let fruit = prompt("Which fruit to buy?", "apple");

let bag = {
  [fruit]: 5, // the name of the property is taken from the variable fruit
};

alert( bag.apple ); // 5 if fruit="apple"
```
- `[fruit+'Computers']`와 같이 property를 선언할 때 concatenation을 해도 상관없음

### Property value shorthand
```javascript
function makeUser(name, age) {
  return {
    name: name,
    age: age,
    // ...other properties
  };
}

let user = makeUser("John", 30);
alert(user.name); // John
```

위 코드의 object literal 부분을 아래와 같이 shorthand를 사용해서 바꿀 수 있음

```javascript
function makeUser(name, age) {
  return {
    name, // same as name: name
    age,  // same as age: age
    // ...
  };
}
```
- property name(key)와 value가 같을 경우 사용 가능

### Property names limitations
object는 "for", "let", "return"등의 reserved words도 property name으로 사용 가능함  
※ `0`과 같은 숫자도 이름으로 사용 가능!!  
```javascript
let obj = {
  0: "test" // same as "0": "test"
};

// both alerts access the same property (the number 0 is converted to string "0")
alert( obj["0"] ); // test
alert( obj[0] ); // test (same property)
```
- `0`이 자동으로 `"0"`(`String`)으로 바뀜
- `obj["0"]`, `obj[0]` 두 가지 방식으로 호출할 수 있음  

> 객체 배열을 선언하면 그것과는 구별을 어떻게 하나?  
> - Integer property와 배열은 코드에서 바로 구분할 수는 없을 듯  
>	꼭 알아야 할 상황이면 `Array.isArray()`를 사용하면 됨

`__proto__`는 non-object value로 설정할 수 없음!  
`obj.__proto__`와 같이 호출하면 아예 object가 리턴됨

### Property existence test, "in" operator
다른 언어들과 비교해서 object에 관한 JS의 가장 큰 특징은 어떤 property라도 접근할 수 있다는 것임  
property가 존재하지 않아도 가능  
=> 존재하지 않는 property를 호출하면 `undefined`를 리턴함

`in` operator를 사용해서 object에 property가 있는지 확인할 수 있음  
`"key" in object` => `key`라는 property가 존재하면 `true`, 아니면 `false` 리턴  
`"key"` 대신 변수를 넣으면 해당 변수의 value가 object의 property인지 확인함
- property가 `undefined`를 저장하고 있을 때 유용(`undefined`를 명시적으로 대입할 일이 별로 없기 때문에 이런 상황은 잘 일어나지 않음)

### The "for...in" loop
```javascript
let user = {
  name: "John",
  age: 30,
  isAdmin: true
};

for (let key in user) {
  // keys
  alert( key );  // name, age, isAdmin
  // values for the keys
  alert( user[key] ); // John, 30, true
}
```
- `in` 뒤에 object가 오면 iterator에 property name이 들어감

#### Ordered like an object
object의 poperties가 *integer properties*인지 아닌지에 따라서 나열되는 기준이 다름

Integer property : `"1"`, `"41"`과 같이 property name을 Integer로 변환했다가 다시 `String`으로 변환해도 값이 같은 property(`"+41"`, `"1.2"`는 같지 않음)
⇔ `name == String(Math.trunc(Number(name)))`

"for...in"으로 key를 나열하면, 
- Integer property인 경우 크기 순으로 나열됨
- 아닌 경우 생성된 순으로 나열됨

※ 숫자들을 key로 사용하고 싶지만 생성된 순으로 나열되기 하고 싶을 때는 `"+49"`와 같이 선언하고 출력할 때 `Number`로 변환해서 출력하면 됨!!

### Summary

|code|description|
|:---|:---|
|`let user = {};`|object literal|
|`user[key]=1;`|computed properties<br>object literal에서도 사용 가능|
|`"key" in obj`|이름이 `"key"`인 property 존재 여부|
|`for(let key in user) {...}`|properties 탐색<br>숫자 property만 오름차순, 나머지는 생성 시간 기준으로 나열됨|

- property 선언
	- object literal 안에서 : `name: "John",`
	- 선언 후 : `user.name="John";`
- `Array`, `Date`, `Error` 등의 다양한 `object`들이 존재함(나중에 배울 예정)

### Tasks
객체의 isEmpty를 아래와 같이 구현할 수 있음:  
```javascript
function isEmpty(obj) {
  for (let key in obj) {
    // if the loop has started, there is a property
    return false;
  }
  return true;
}
```

## Object references and copying
object는 저장, 복사될 때 "call by reference"로 처리됨  
(cf. primitive는 "call by value"로 처리됨)  
```javascript
let user = { name: 'John' };

let admin = user;

admin.name = 'Pete'; // changed by the "admin" reference

alert(user.name); // 'Pete', changes are seen from the "user" reference
```

### Comparison by reference
아예 선언부터 독립적으로 해야 독립적인 두 개의 객체가 생성됨

### Cloning and merging, Object.assign
object cloning을 위한 내장 함수는 없음  
=> 두 가지 방법 존재:
1. for...in을 사용해서 properties를 복사  
	```javascript
	let user = {
	  name: "John",
	  age: 30
	};

	let clone = {}; // the new empty object

	// let's copy all user properties into it
	for (let key in user) {
	  clone[key] = user[key];
	}

	// now clone is a fully independent object with the same content
	clone.name = "Pete"; // changed the data in it

	alert( user.name ); // still John in the original object
	```
2. `Object.assign` method 이용  
	```javascript
	Object.assign(dest, [src1, src2, src3...])
	```
	- `src1, ..., srcN`은 source **objects**임
	- source objects의 모든 properties는 `dest`로 복사됨
	- `dest`를 리턴함
	
	```javascript
	// (1)
	let user = { name: "John" };

	let permissions1 = { canView: true };
	let permissions2 = { canEdit: true };

	Object.assign(user, permissions1, permissions2, { name: "Pete" });

	// now user = { name: "Pete", canView: true, canEdit: true }
	
	// (2)
	let user = {
	  name: "John",
	  age: 30
	};

	let clone = Object.assign({}, user);
	```
	
	- (2) : 위의 `for...in`을 이용한 방법이랑 같은 방법임

### Nested cloning
```javascript
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};
```
- 위와 같은 nested object의 경우 위 방법(`for...in`, `object.assign`)만으로는 복사가 완벽하게 되지 않음  
	`object` type인 property가 reference로 복사되기 때문  
	=> "shallow copy"라고 함
- 따라서 properties의 type을 확인하고 `object`일 경우 따로 복제해줘야 함  
	=> "deep cloning"이라고 함
	
	재귀로 구현하거나 [lodash](https://lodash.com/)의 `_.cloneDeep(obj)` 이용

※ object는 `const`로 선언해도 properties는 수정할 수 있음(`name=...`와 같이 객체 자체를 수정하려 할 때만 에러남)  
properties를 constant로 만들기 위해선 Property flags를 사용해야 함!(나중에 다룸)

### Summary

|code|description|
|:---|:---|
|`Object.assign(dest[, src1, src2...]);`|object cloning(shallow copy)|

- `object`는 호출될 때 항상 call by reference로 처리됨
- deep copy는 lodash의 `_.cloneDeep(obj)` 이용

## Garbage collection
### Reachability
*Reachability*(*도달 가능성*)이 JS memory management의 핵심 개념임  
"reachable" values는 memory에 저장될 수 있게 보장됨
1. 명확한 이유로 reachable values인 값들을 *roots*라고 부름
	- 현재 실행중인 함수와 그 안의 지역 변수, 인자들
	- 중첩된 호출에 속한 함수들과 그 지역 변수, 인자들
	- 전역 변수들  
		...
2. root를 참조할 경우 reachable이라 판단됨  
	예를 들어, object A가 전역 변수고 다른 object B를 property로 참조하고 있으면 B도 reachable임

garbage collector가 unreachable한 objects, primitives를 제거함

※ garbage collection은 자동적으로 일어나고, 우리가 강제할 수 없음

### Two references
unreachable해야 garbage collect됨

### Interlinked objects
```javascript
function marry(man, woman) {
  woman.husband = man;
  man.wife = woman;

  return {
    father: man,
    mother: woman
  }
}

let family = marry({
  name: "John"
}, {
  name: "Ann"
});
```

|Result:|
|:---|
|![js-garbage-collection1](https://github.com/siriyaoff/MDN-note/blob/master/images/js-garbage-collection1.PNG?raw=true)|

- 모든 object가 reachable함

두 개의 references 제거:  
```javascript
delete family.father;
delete family.mother.husband;
```

|Result:|
|:---|
|![js-garbage-collection2](https://github.com/siriyaoff/MDN-note/blob/master/images/js-garbage-collection2.PNG?raw=true)|

- 위의 경우 `name: john`인 object가 garbage collect됨
- incoming reference만 object를 reachable하게 만들 수 있음

### Unreachable island
위의 예시에서 아예 global variable로부터의 reference를 끊으면(`family=null`) 모든 object가 unreachable하게 됨  
서로 incoming references가 존재하지만 reachable value로부터의 reference가 없기 때문에 unreachable함  
=> 참조되었다고 reachable한건 아님!!

### Internal algorithms
garbage collection은 "mark-and-sweep"이라는 algorithm을 기반으로 함:  
1. garbage collector가 roots를 찾고 mark해놓음(방문한 사실도 저장함)
2. mark된 객체들을 방문해서 그것들이 참조하는 객체들을 다시 mark
3. 모든 reachable references를 방문할 때까지 2를 반복
4. mark된 객체를 제외한 객체들을 없앰

bfs랑 비슷  
JS engine에서는 아래와 같은 최적화를 실행함:
- Generational collection  
	object를 new, old로 분류함  
	old들은 오랫동안 유지된 객체들이기 때문에 자주 조사하지 않음
- Incremental collection  
	전체를 한꺼번에 처리하는 대신, 조각으로 나눠서 조금씩 처리함  
	visible delay가 발생하지 않음
- Idle-time collection  
	CPU가 idle일 때만 garbage collector를 실행해서 실행 시간에 영향을 주지 않게 만듦

garbage collection에 관한 지식은 low-level optimization을 수행할 때 요구됨

## Object methods, "this"
object의 property로 선언된 function을 object의 *method*라고 함

### Method examples
```javascript
let user = {
  name: "John",
  age: 30
};

user.sayHi = function() {
  alert("Hello!");
};

user.sayHi(); // Hello!
```
- 위 예시에서는 `sayHi`가 `user`의 method임

아래와 같이 미리 선언된 함수를 method로 사용할 수도 있음:  
```javascript
let user = {
  // ...
};

// first, declare
function sayHi() {
  alert("Hello!");
};

// then add as a method
user.sayHi = sayHi;

user.sayHi(); // Hello!
```

> In Object-oriented programming, we use objects to represent entities

#### Method shorthand
아래 두 가지 방법으로 method를 선언할 수 있음:  
```javascript
user = {
  sayHi: function() {
    alert("Hello");
  }
};

// method shorthand looks better, right?
user = {
  sayHi() { // same as "sayHi: function(){...}"
    alert("Hello");
  }
};
```

### "this" in methods
object에 접근하기 위해, method 내에서 `this` keyword를 이용함:  
```javascript
let user = {
  name: "John",
  age: 30,

  sayHi() {
    // "this" is the "current object"
    alert(this.name);
  }
};

user.sayHi(); // John
```

`this`를 사용하지 않고 위의 method 구현부에서 `alert(user.name);`으로 적어도 작동은 됨  
하지만 아래와 같이 `user`을 overwrite하면 문제가 생김:  
```javascript
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert( user.name ); // leads to an error
  }
};


let admin = user;
user = null; // overwrite to make things obvious

admin.sayHi(); // TypeError: Cannot read property 'name' of null
```

### "this" is not bound
`this`를 method가 아닌 함수에서도 사용 가능함  
=> run-time에 `this`의 값이 계산됨

#### Example
```javascript
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert( this.name );
}

// use the same function in two objects
user.f = sayHi;
admin.f = sayHi;

// these calls have different this
// "this" inside the function is the object "before the dot"
user.f(); // John  (this == user)
admin.f(); // Admin  (this == admin)

admin['f'](); // Admin (dot or square brackets access the method – doesn't matter)
```
- method도 square brackets와 string으로 호출할 수 있다는 것에 유의!
- `sayHi`를 method가 아닌 일반 함수로 호출하면(`sayHi();`):
	- strict mode에서는 `this`가 `undefined`로 바뀜  
		=> `this.name`을 접근할 때 에러가 남
	- non-strict mode에서는 `this`가 *global object*를 가리킴  
		strict mode로 고친 예전의 에러임
	
	보통 `this`를 사용하는 함수는 method로 사용되기 때문에 object를 통해서 호출되지 않으면 에러인 경우가 많음

> JS에서의 `this`의 취급  
> 다른 언어들에서는 보통 `this`를 method가 정의된 객체만을 참조함("bound this")  
> 하지만 JS에서는 `this`가 method가 정의된 객체만을 참조하지 않고, method를 호출한 객체를 참조함  
> 장점 : 재사용성 ↑, 단점 : 실수가 잦아질 수 있음

### Arrow functions have no "this"
arrow function에서 `this`를 사용하면, arrow function이 구현된 함수(outer normal function)를 호출한 객체를 참조함:  
```javascript
let user = {
  firstName: "Ilya",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  }
};

user.sayHi(); // Ilya


let usera = {
  firstName: "Ilya",
  userb: {
    firstName: "Ilya2",
    sayHi : () => alert(this.firstName)
  }
};

let userc={
  firstName: "Ilya3",
  sayHi: ()=> alert(this.firstName)
};

usera.userb.sayHi(); // undefined
userc.sayHi(); // undefined
```
- outer normal function 없이 바로 method로 사용되고 `this`를 사용할 경우 `this`는 `undefined`로 바뀜!!  
	위의 경우에도 `this`를 사용하지 않으면 arrow function을 바로 method로 사용할 수 있음

### Summary
- method에서 property를 참조하기 위해서는 `this`를 이용해야 함(`this.prop`)
- property만 있는 객체는 object literal을 리턴하는 것으로 간단하게 constructor를 구현 가능  
	(constructor function syntax를 사용하지 않고)  
	
	`this`를 사용해야 하는 경우 constructor function을 사용  
	(호출할 때 `new`와 같이 사용되기 때문에 일반 함수와 분명한 차이가 있음)
- arrow function으로 method를 구현할 때 `this`를 사용하면 arrow function을 사용한 method를 소유한 객체를 리턴함  
	※ 반드시 method안에서 arrow function을 function expression으로 사용해야 함!!  
	arrow function 자체를 method로 정의하면 `this`가 `undefined`를 반환함  
	이런 특징때문에 arrow function은 method를 구현할 때 사용하지 않는 것이 좋음!!

### Tasks
```javascript
function makeUser() {
  return {
    name: "John",
    ref: this
  };
}

let user = makeUser();

alert( user.ref.name ); // Error: Cannot read property 'name' of undefined
```
- `ref`에는 `undefined`가 저장됨!  
	∵ `this`의 값은 호출 시점에 결정되는데, `makeUser()`가 method가 아닌, 일반 함수로 호출되었기 때문에 전체 함수인 `undefined`가 들어감(code block과 object literal은 영향을 주지 않음)  
	따라서 `ref: this`는 현재 `this`의 값인 `undefined`가 저장되고, `user.ref`가 `undefined`가 됨
	
	아래 코드와 동치임:  
	```javascript
	function makeUser(){
	  return this; // 이번엔 객체 리터럴을 사용하지 않았습니다.
	}

	alert( makeUser().name ); // Error: Cannot read property 'name' of undefined
	```
	
	원래 의도대로 구현한 코드:  
	```javascript
	function makeUser() {
	  return {
		name: "John",
		ref() {
		  return this;
		}
	  };
	};

	let user = makeUser();

	alert( user.ref().name ); // John
	alert( user.ref().ref().name ); // John
	```
	- `user.ref()`가 method가 되기 때문에 `this`는 `.`앞의 객체로 선정됨

```javascript
let ladder = {
  step: 0,
  up() {
    this.step++;
    return this;
  },
  down() {
    this.step--;
    return this;
  },
  showStep() { // 사다리에서 몇 번째 단에 올라와 있는지 보여줌
    alert( this.step );
    return this;
  }
};

ladder.up();
ladder.up();
ladder.down();
ladder.showStep(); // 1

ladder.up().up().down().showStep(); // 2
```
- method의 리턴을 `this`로 설정해서 호출을 chainable하게 만들 수 있음

## Constructor, operator "new"
비슷한 객체를 많이 만들어야 하는 경우에는 object literal로 하기에 불필요한 반복이 많음  
=> constructor function과 `new` operator를 사용

### Constructor function
생성자 함수는 기능적으로는 보통의 함수와 같음  
생성자 함수의 규칙 2가지:
1. 대문자로 시작(common agreement)
2. `new` operator와 같이 사용되어야 함

#### Example
```javascript
function User(name) {
  // this = {};  (implicitly)

  // add properties to this
  this.name = name;
  this.isAdmin = false;

  // return this;  (implicitly)
}

let user = new User("Jack");

alert(user.name); // Jack
alert(user.isAdmin); // false
```
- 생성자 함수에서는 주석과 같이 `this`에 이미 객체가 선언되어 있다고 생각하면 됨(`undefined`가 리턴되지 않음!)
- 모든 함수들이 생성자로 사용될 수 있음 => `new`와 같이 사용되면 모든 함수들이 위와 같이 `this`를 리턴함

`let user=new function() { ... };`와 같이 사용하면 constructor는 재사용할 수 없는 대신 하나의 객체만을 생성하도록 코드를 encapsulate하는 효과가 있음

### Constructor mode test: new.target
`new.target` property를 사용하면 함수 내부에서 이 함수가 `new`와 함께 호출되었는지 알 수 있음  
- `new`와 함께 호출된 함수에서 사용하면 함수 자체(`function User() { ... }`)가 리턴됨
- `new`없이 호출된 함수에서 사용하면 `undefined` 리턴

아래와 같이 `new`가 있던 없던 constructor mode로 동작하게 구현할 수 있음:  
```javascript
function User(name) {
  if (!new.target) { // if you run me without new
    return new User(name); // ...I will add new for you
  }

  this.name = name;
}

let john = User("John"); // redirects call to new User
alert(john.name); // John
```
- 문법을 더 유연하게 만들지만, `new`를 생략해서 코드의 가독성을 떨어뜨릴 수 있음

### Return from constructors
보통 constructor는 `return` 문장이 없지만, 있을 경우 아래와 같이 처리됨:
- `return`이 object와 같이 사용되면 `this` 대신 그 object를 리턴
- `return`이 primitive와 같이 사용되거나 혼자 사용되면 무시됨

#### Example
```javascript
function BigUser() {

  this.name = "John";

  return { name: "Godzilla" };  // <-- returns this object
}

alert( new BigUser().name );  // Godzilla, got that object
```
- `new` operator가 `.`보다 우선순위가 높은듯

※ `new`를 사용하면 constructor의 괄호를 생략할 수 있음(인자가 없을 때)  
하지만 이것 또한 가독성을 떨어뜨리기 때문에 좋은 코딩 스타일이 아님

### Methods in constructor
method도 `this`를 사용해서 정의 가능함:  
```javascript
function User(name) {
  this.name = name;

  this.sayHi = function() {
    alert( "My name is: " + this.name );
  };
}

let john = new User("John");

john.sayHi(); // My name is: John
```
- class를 이용하면 더 복잡한 object를 생성할 수 있음(지금 다루는 object는 구조체 느낌인듯)

### Summary

|code|description|
|:---|:---|
|`let user = new User([param...]);`|Constructor function|
|`new.target`|현재 함수가 `new`와 함께 호출되었는지 판별|

- `new` operator가 `.`보다 우선순위가 높음  
	`new User().name`을 실행하면 만들어진 객체의 `name` property가 정상적으로 출력됨
- object literal으로 선언할 때는 `:`, constructor function에서 선언할 때는 일반 statement처럼 `=` 사용

### Tasks
- constructor로 method를 정의할 때는 무조건 `this.method= function expression;`을 사용해야 하는 듯(function declaration을 사용하면 method로 추가되지 않음)  
	아니면 function declaration으로 정의한 뒤에 `this.method=func_name;`으로 정의해도 됨

## Optional chaining `?.`
property를 호출하는 안전한 방법임(특히 A.B.C와 같이 중첩된 property 호출에서 B가 `null`일 수도 있을 때)

### The "non-existing property" problem
```javascript
let user = {}; // a user without "address" property

alert(user.address.street); // Error!
```
- 위의 상황처럼 `user`가 `address` property를 가지지 않음  
	=> `user.address`가 `undefined`이기 때문에 `user.address.street`을 호출하면 에러가 남

web development에서도 `document.querySelector('.elem')`함수를 사용할 때 해당하는 element가 없으면 `null`이 반환됨:  
```javascript
let html = document.querySelector('.elem').innerHTML; // error if it's null
```

#### 해당 element가 업을 때 `html`에 `null`을 대입하려면?
`if`나 삼항연산자 `?`를 사용  
e.g. `alert(user.address ? user.address.street : undefined);`

중첩이 많아지면 코드에 불필요한 반복이 너무 많아짐  
=> `&&` 이용:  
`alert(user.address && user.address.street && user.address.street.name );`

AND'ing 또한 반복이 너무 많음  
이런 반복을 줄이기 위해서 optional chaining `?.`가 추가됨

### Optional chaining
`?.`는 왼쪽 대상이 `undefined`거나 `null`이면 계산을 멈추고 `undefined`를 리턴함  
아래에서는 편의를 위해 `null`이나 `undefined`가 아니면 객체가 존재한다고 가정함

즉, `value?.prop`는 아래와 같이 작동함:
- `value`가 존재한다면 `value.prop` 리턴
- `value`가 존재하지 않는다면(`undefined` 또는 `null`일 경우) `undefined` 리턴

위의 예제에 optional chaining을 적용하면 아래와 같음:  
```javascript
let user = {}; // user has no address

alert( user?.address?.street ); // undefined (no error)
```
- `user = null`일 경우에도 작동함(당연히 `undefined` 반환)

> optional chaining은 존재하지 않아도 괜찮은 대상에만 사용해야 함  
> 모든 대상에 사용하면 항상 존재해야 하는 대상이 실수로 정의되지 않아도 에러가 나지 않기 때문에 디버깅하기 어려워짐!

> `?.` 전의 값은 반드시 선언되어 있어야 함!  
> optional chaining은 선언된 변수에 대해서만 동작함

### Short-circuiting
`?.`는 왼쪽 대상이 존재하지 않으면 아예 멈춤  
=> 아래와 같이 함수나 증가식도 계산되지 않음:  
```javascript
let user = null;
let x = 0;

user?.sayHi(x++); // no "sayHi", so the execution doesn't reach x++

alert(x); // 0, value not incremented
```

### Other variants: `?.()`, `?.[]`
method를 호출할 때 `method()`대신 `method?.()`로 호출해서 optional chaining과 같은 효과를 낼 수 있음:  
```javascript
let userAdmin = {
  admin() {
    alert("I am admin");
  }
};

let userGuest = {};

userAdmin.admin?.(); // I am admin

userGuest.admin?.(); // nothing (no such method)
```

변수를 이용한 property 호출도 원래는 `obj[var]`과 같이 호출하지만 `obj?.[var]`로 optional chaining과 같은 효과를 낼 수 있음:  
```javascript
let key = "firstName";

let user1 = {
  firstName: "John"
};

let user2 = null;

alert( user1?.[key] ); // John
alert( user2?.[key] ); // undefined
```

`delete` operator도 `?.`과 함께 사용할 수 있음:  
```javascript
delete user?.name; // delete user.name if user exists
```

> `?.`를 이용해서 읽기, 삭제를 안전하게 수행할 수 있지만 수정은 안됨!  
> `user?.name = "john";`은 `user`가 존재하지 않으면 `undefined`에 RHS를 대입하는 꼴이 되기 때문에 어차피 에러남

### Summary

|code|description|
|:---|:---|
|`user?.address`|optional chaining<br>연산자 이전의 값은 반드시 선언되어 있어야 함|
|`obj.method?.()`|method에 대해 optional chaining 적용|
|`obj?.[var]`|computed property에 대해 optional chaining 적용|

## Symbol type
specification에 따르면, object property key는 `String` type이거나 `Symbol` type임  

### Symbols
`Symbol()`을 사용해서 unique identifier을 만들 수 있음:  
```javascript
// id is a symbol with the description "id"
let id = Symbol("id");

let id1 = Symbol("id");

alert(id == id1); // false
```
- 같은 description을 써서 생성하더라도 둘은 다른 symbol들임

※ symbol들은 자동으로 `String`으로 변환되지 않음!!  
```javascript
let id = Symbol("id");
alert(id); // TypeError: Cannot convert a Symbol value to a string
alert(id.toString()); // Symbol(id), now it works
alert(id.description); // id
```
- `Symbol`과 `String`은 근본적으로 다르기 때문에 `Symbol`은 아예 다른 형으로 변환되는 것이 막혀있음
- `Symbol`을 출력하기 위해서는 `toString()`을 이용하거나 description을 출력해야 함

### "Hidden" properties
`Symbol`을 key로 이용해서 숨겨진 property를 생성할 수 있음  
=> `Symbol`을 이용하지 않고는 접근할 수 없음

#### Example
```javascript
let user = { // belongs to another code
  name: "John"
};

let id = Symbol("id");

user[id] = 1;

alert( user[id] ); // we can access the data using the symbol as the key
```
- symbol은 항상 다르기 때문에, 다른 곳에서 똑같은 `id`를 symbol로 사용하더라도 `user[id]`는 서로 다른 properties가 됨  
	cf. `"id"`를 property name으로 사용할 경우 충돌이 일어남

### Symbols in an object literal
square brackets `[]`를 이용해서 object literal에서도 symbol을 사용할 수 있음:  
```javascript
let id = Symbol("id");

let user = {
  name: "John",
  [id]: 123 // not "id": 123
};
```

### Symbols are skipped by for...in
symbol로 선언된 property는 심지어 `for...in` 반복문에서도 배제됨:  
```javascript
let id = Symbol("id");
let user = {
  name: "John",
  age: 30,
  [id]: 123
};

for (let key in user) alert(key); // name, age (no symbols)

// the direct access by the symbol works
alert( "Direct: " + user[id] );
```

`object.assign`을 이용해서 object를 복제할 때는 symbol properties도 복사됨

### Global symbols
global symbol을 이용해서 다른 곳에서 같은 symbol을 사용할 수 있음  
`Symbol.for(key)`를 사용해서 *global symbol registry*에 *global symbol*을 등록하거나 등록되어 있는 것을 읽음
- global symbol registry에 `key`에 해당하는 global symbol이 등록되어 있지 않으면 생성, 등록하고 반환
- 등록되어 있는 경우 해당 global symbol을 반환함

```javascript
// read from the global registry
let id = Symbol.for("id"); // if the symbol did not exist, it is created

// read it again (maybe from another part of the code)
let idAgain = Symbol.for("id");

// the same symbol
alert( id === idAgain ); // true
```

> Ruby에서의 symbol이 JS에서의 global symbol과 비슷함

#### `Symbol.keyFor`
`Symbol.keyFor(sym)`을 사용해서 global symbol 값에 해당하는 `key`를 찾을 수 있음  
```javascript
let globalSymbol = Symbol.for("name");
let localSymbol = Symbol("name");

alert( Symbol.keyFor(globalSymbol) ); // name, global symbol
alert( Symbol.keyFor(localSymbol) ); // undefined, not global

alert( localSymbol.description ); // name
alert( globalSymbol.description ); // name
```
- `Symbol.keyFor(sym)`은 global symbol registry에서 `sym`에 해당하는 key를 찾아서 반환함  
	=> non-global symbol에 대해서는 key값을 찾을 수 없기 때문에 `undefined` 반환
- 모든 symbol들은 `description` property를 가짐!  
	global symbol도 key가 description이기 때문에 `.description`으로 출력 가능함

### System symbols
system symbols가 존재함:
- Symbol.hasInstance
- Symbol.isConcatSpreadable
- Symbol.iterator
- Symbol.toPrimitive
	- object to primitive conversion에 필요함

### Summary

|code|description|
|:---|:---|
|`let id = Symbol("description");`|symbol 생성|
|`sym.description`|symbol의 `"description"` 반환|
|`let id = Symbol.for("description");`|global symbol 생성|
|`Symbol.keyFor(sym)`|global symbol의 key(`"description"`) 반환|

- symbolic property는 `for...in`에서도 배제됨
- global symbol은 `sym.description`을 사용하든 `Symbol.keyFor()`을 사용하든 생성될 때 사용한 description을 리턴함
- `Object.getOwnPropertySymbols(obj)`를 사용하면 properties 뿐만 아니라 symbol들까지 알 수 있음  
- `Reflect.ownKeys(obj)`를 사용하면 symbolic properties를 포함해서 모든 properties의 key를 알 수 있음

## Object to primitive conversion
`obj1 + obj2` 등 객체끼리 연산될 때는 자동으로 primitives로 변환됨:
1. 모든 객체는 boolean으로 변환될 때 `true`로 취급됨 => 객체를 변환할 때는 numeric, string으로의 변환만 사용함
2. 객체끼리 뺄셈이나 수학적 함수를 적용할 때 numeric conversion이 일어남  
	e.g. `Date` 객체의 연산 : `date1 - date2`
3. string conversion은 보통 `alert(obj)`와 같이 객체를 출력할 때 일어남

### ToPrimitive
`"string"`, `"number"`, `"default"` 3개의 hint를 이용해서 객체의 변환을 조절할 수 있음  
hint는 목표로 하는 자료형으로 이해하면 됨

#### `"string"`
`alert()`와 같이 문자열이 들어가는 연산을 수행하면 hint가 string이 됨:  
```javascript
// output
alert(obj);

// using object as a property key
anotherObj[obj] = 123;
```

#### `"number"`
계산할 때는 hint가 number가 됨:  
```javascript
// explicit conversion
let num = Number(obj);

// maths (except binary plus)
let n = +obj; // unary plus
let delta = date1 - date2;

// less/greater comparison
let greater = user1 > user2;
```

#### `"default"`
`+`, `==`와 같이 숫자, 문자 모두에서 사용되는 연산자에서는 hint가 default가 됨:  
```javascript
// binary plus uses the "default" hint
let total = obj1 + obj2;

// obj == number uses the "default" hint
if (user == 1) { ... };
```
- `<`, `>`와 같은 비교 연산자들도 숫자, 문자 모두 피연산자로 사용 가능하지만 hint가 number로 됨  
	`Date` 객체를 제외하면 대부분의 내장된 객체에서 default도 number처럼 동작하기 때문에 다 외울 필요는 없음

※ hint는 3개만 존재함!(number, string, default)  
boolean은 hint가 아님!!

conversion을 할 때 JS는 아래 순서대로 작동함:
1. 객체에 `obj[Symbol.toPrimitive](hint)` method를 찾고, 있으면 호출함  
	`Symbol.toPrimitive`는 system symbol으로, 따로 만드는게 아님
2. 위의 경우에 해당하지 않고 hint가 string일 때  
	`obj.toString()`, `obj.valueOf()` 순서대로 찾으면서 존재하는 것을 실행함
3. 위의 경우에 해당하지 않고 hint가 number 또는 default일 때  
	`obj.valueOf()`, `obj.toString()` 순서대로 찾으면서 존재하는 것을 실행함  

### Symbol.toPrimitive
`Symbol.toPrimitive`는 내장 symbol로, conversion method로 사용됨

#### Example
```javascript
let user = {
  name: "John",
  money: 1000,

  [Symbol.toPrimitive](hint) {
    alert(`hint: ${hint}`);
    return hint == "string" ? `{name: "${this.name}"}` : this.money;
  }
};

// conversions demo:
alert(user); // hint: string -> {name: "John"}
alert(+user); // hint: number -> 1000
alert(user + 500); // hint: default -> 1500
```

### toString/valueOf
위의 symbolic key와 다르게 string-named method임  
반드시 primitive value를 리턴해야 함  
(`object`를 리턴할 경우 아예 무시됨)

각 함수의 default:
- `toString`은 `"[object Object]"`를 리턴함
- `valueOf`는 object 자체를 리턴함

```javascript
let user = {name: "John"};

alert(user); // [object Object]
alert(user.valueOf() === user); // true
```

- 재정의하고 사용하기 때문에 큰 의미는 없음

#### Example
```javascript
let user = {
  name: "John",
  money: 1000,

  // for hint="string"
  toString() {
    return `{name: "${this.name}"}`;
  },

  // for hint="number" or "default"
  valueOf() {
    return this.money;
  }

};
```
- `[Symbol.toPrimitive](hint)`와 동일한 기능임
- 객체를 변환하는 순서에 따라서, `Symbol.toPrimitive`와 `valueOf`가 없으면 `toString`이 모든 변환을 담당함  
	

### Return types
primitive-conversion method들이 반드시 hint와 같은 primitive를 리턴할 필요는 없음  
primtivie만 리턴하면 됨

> `toString`과 `valueOf`는 객체를 리턴해도 에러가 나지 않고 method가 존재하지 않는 것처럼 무시됨  
> 예전에는 JS에 에러에 관한 명확한 정의가 없었기 때문  
> 반면, `Symbol.toPrimitive`는 primitive를 리턴하지 않으면 에러남

### Further conversions
객체가 인자로 사용될 때 두 단계에 거쳐서 conversion이 일어남:
1. 위 규칙에 따라서 객체가 primitive로 변환됨
2. 변환된 primitive가 적절한 type이 아니면 변환됨

#### Example
```javascript
let obj = {
  // toString handles all conversions in the absence of other methods
  toString() {
    return "2";
  }
};

alert(obj * 2); // 4
alert(obj + 2); // 22
```

### Summary

|code|description|
|:---|:---|
|`[Symbol.toPrimitive](hint)`|conversion method|
|`toString()`|conversion method|
|`valueOf()`|conversion method|

- 실무에서는 `obj.toString()`가 모든 변환을 담당하는 "catch-all" method로 구현되는 경우가 많음
- 호환성을 위해서 `toString()`, `valueOf()`을 `return this[Symbol.toPrimitive]('string or number')`과 같이 구현할 수 있음


# Data types
## Methods of primitives
primitive와 object의 차이점:
- A primitive
	- primitive type의 값임
	- 7개의 type이 존재 : `String`, `Number`, `Bigint`, `Boolean`, `Symbol`, `null`, `undefined`
- An object
	- 여러 개의 값을 property로 저장할 수 있음
	- `{}`로 생성할 수 있고 JS에는 함수와 같은 여러 종류의 object가 있음
	- 함수도 property로 저장(method)할 수 있음
	- primitive보다 자원을 많이 소모함

### A primitive as an object
primitive를 method와 함께 사용하기 위해 아래와 같은 방법을 사용함:
- `String`, `Number`, `Boolean`, `Symbol`의 method와 property에 접근하는 것을 허용함
- 위 접근을 가능하게 하기 위해, *object wrapper*를 제공함(임시적으로 생성, 소멸됨)

object wrapper는 각각의 primitive type에 따라 다르며, primitive의 이름과 같음(`String`, `Number`, `Boolean`, `Symbol`)  
각각 다른 methods를 제공함

#### Example
string method `str.toUpperCase()`는 `str`를 capitalize한 것을 반환함:  
```javascript
let str = "Hello";

alert( str.toUpperCase() ); // HELLO
```
이 method를 호출했을 때 일어나는 일:
1. `str`은 primitive이기 때문에, property에 접근하는 순간 string의 값과 `toUpperCase()` 등의 method를 가진 객체가 생성됨
2. method가 실행되고 새로운 string이 반환됨
3. 객체가 파괴되고 primitive인 `str`만 남음

이렇게 primitive가 method를 제공하면서 가볍게 유지됨  
JS 엔진은 추가적인 객체를 생성하지 않을 만큼 최적화되어 있지만 명세서에는 그것을 생성하는 것처럼 적혀있음

`Number`에는 `toFixed(n)`과 같은 method가 존재함  
`alert( n.toFixed(2) );` : 소수점 `n`자리까지 남도록 반올림함

> ※ `String/Number/Boolean`을 생성자로는 사용하지 않는 게 좋음  
> Java와 같은 언어에서는 명시적으로 wrapper object를 생성할 수 있음(`new Number(0)`과 같이)  
> JS에서도 가능은 하지만 크게 아래의 이유로 추천되지 않음:  
> - primitive가 아닌 object로 인식되기 때문에 조건문에서 값에 상관없이 참을 반환함
>
> 반면 `new`를 사용하지 않고 `String/Number/Boolean`만 쓰는 것은 값을 원하는 type으로 변환하게 도와주기 때문에 유용함  
> e.g. `let num = Number("123");`

> ※ `null/undefined`는 method가 없음  
> 위 type들은 wrapper object가 없음  
> `alert(null.test);`와 같이 proeprty에 접근하려 하면 에러가 발생함

### Summary
- primitive를 다룰 때 유용한 기능들이 각각의 primitive 안에 있음
	- method로 구현된 기능을 호출하면 임시적으로 object wrapper라는 객체가 생성되고, method가 실행된 뒤 파괴됨

### Tasks
#### primitive가 method를 호출하면 객체로 처리되는데, property를 추가할 수 있을까?  
```javascript
let str = "Hello";

str.test = 5;

alert(str.test);
```
- strict mode의 사용 여부에 따라 결과가 다름
	- strict mode를 사용하지 않으면 `undefined`가 출력됨
	- strict mode를 사용하면 error가 발생함

- property에 접근할 때 wrapper object가 생성은 됨!
	- strict mode에서는 값을 수정할 수 없음
	- strict mode가 아닐 경우, 객체가 `test` property를 가지지만, 그 statement가 끝난 후 사라짐!  
		따라서 마지막 줄에서 `str`은 `test`라는 property를 찾을 수 없음!
	
	primitive와 object의 차이점 중 하나임:  
	primitive는 추가적인 데이터를 저장할 수 없음!!

## Numbers
최신의 JS에는 두 가지 타입의 숫자가 존재함:
1. 일반적인 숫자는 64-bit format IEEE-764(double precision floating point number)으로 저장됨
2. 임의의 길이의 숫자를 표현하기 위해서 BigInt가 사용됨  
	일반적인 숫자는 `[-2^53, 2^53]`의 수만 표현 가능하기 때문

이 article에서는 일반적인 숫자에 대해 다룰 예정

### More ways to write a number
underscore `_`를 숫자 사이에 구분자로 넣을 수 있음:  
```javascript
let billion = 1_000_000_000;
```
- 숫자의 가독성을 높여줌
- JS 엔진은 숫자 자리수 사이에 사용된 `_`는 무시함

`"e"`를 지수승 표기로 사용할 수 있음:
```javascript
let billion = 1e-6;  // 0.000001

alert( 7.3e9 );  // 7300000000
```

#### Hex, binary and octal numbers
`0x`, `0b`, `0o` for hex, binary, octal numbers  
case doesn't matter  
for other numeral systems, we should use the function `parseInt`

### toString(base)
`num.toString(base)`를 사용하면 숫자를 `base`진법으로 변환한 결과를 string으로 반환함  
```javascript
let num = 255;

alert( num.toString(16) );  // ff
alert( 123456..toString(36) ); // 2n9c
```
- `base`는 `[2, 36]` 내의 숫자만 가능
- 마지막 줄의 `..`은 method를 호출하기 위해 사용한 것임  
	점을 하나만 쓰면 소수점이라 인식하기 때문에 method를 바로 호출하려면 `..`을 사용해야 함  
	`(1234).toString(36)`과 같이 괄호로 묶어도 됨

### Rounding
- `Math.floor` : rounds down
- `Math.ceil` : rounds up
- `Math.round` : rounds to the nearest integer
- `Math.trunc` : removes anything afer the decimal point

위 함수들의 계산 결과는 모두 integer임  
소수점 이하 n자리까지 나오게 계산하고 싶다면?
1. 수학적 조작(2자리까지 나오게 하고싶다면 100을 곱한 값을 함수에 넣음)
2. `toFixed(n)` 사용(자동으로 반올림됨)
	- 결과는 `String`이기 때문에 unary plus로 변환해줘야 함

### Imprecise calculations
64비트 IEEE-754에서 52비트는 가수(fraction), 11비트는 지수(exponent), 1비트가 부호로 사용됨
- 숫자가 너무 크면 `Infinity`로 바뀜
- 정밀도 손실이 일어남(`0.1 + 0.2 == 0.3`은 `false`임)  
	(+ `alert( 9999999999999999 ); // shows 10000000000000000`)  
	부동 소수점으로 저장하기 때문  
	해결 방법:
	1. 소수들을 계산할 동안만 정수로 바꿔서 계산
		- 값이 크지 않을 때 사용해야 함
		- 다시 소수점을 돌려놓는 과정에서 에러가 발생하기 때문에 오차를 줄이는 정도임
	2. `toFixed(n)`을 사용해서 오차를 표현하지 않으면 됨  
		e.g. `alert( sum.toFixed(2) );`

> ※ 부동소수점 덕분에 두 개의 0이 존재함(`0`, `-0`)

### Tests: isFinite and isNaN
`isNaN(value)`는 `value`가 `NaN`이면 `ture`를 리턴함:  
```javascript
alert( isNaN(NaN) ); // true
alert( isNaN("str") ); // true

alert( NaN === NaN ); // false
```
- 마지막 줄처럼, `NaN`은 자신을 포함해서 모든 것들과 같지 않기 때문에 `isNaN()` 함수가 필요함

`isFinite(value)`는 `value`를 숫자로 변환하고 일반적인 숫자면 `true`, `NaN/Infinity/-Infinity`면 `false`를 반환함:  
```javascript
alert( isFinite("15") ); // true
alert( isFinite("str") ); // false, because a special value: NaN
alert( isFinite(Infinity) ); // false, because a special value: Infinity
```
- 빈 문자열이나 공백, `null`은 `0`으로 취급되기 때문에 `true`를 반환함

> ※ `Object.is`는 `===`와 비슷한 기능의 내장 메소드지만, 아래 두 가지 edge case에서 더 신뢰할만한 결과를 반환함:
> 1. `Object.is(NaN, NaN) === true`
> 2. `Object.is(0, -0) === false`
> 
> 위와 같은 비교 방식은 specification에서 SameValue라고 불림

### parseInt and parseFloat
인자의 시작부터 변환 가능한 문자까지만 변환해서 리턴, 변환할 수 없다면 `NaN` 리턴:  
```javascript
alert( parseInt('100px') ); // 100
alert( parseFloat('12.5em') ); // 12.5

alert( parseInt('12.3') ); // 12, only the integer part is returned
alert( parseFloat('12.3.4') ); // 12.3, the second point stops the reading

alert( parseInt('a123') ); // NaN, the first symbol stops the process
```
- `parseInt(str, radix)`로도 사용 가능, `radix` 진법으로 `str`를 읽고 숫자로 변환함  
	e.g. `alert( parseInt('2n9c', 36) ); // 123456`

### Other math functions
- `Math.random()` : returns a random number in `[0, 1)`
- `Math.max(a, b, c...)` / `Math.min(a, b, c...)` : returns the max / min
- `Math.pow(n, power)` : returns `n^pow`

### Summary

|code|description|
|:---|:---|
|`num.toString(base)`|`num`을 `base`진법의 문자열으로 변환|
|`Math.floor()`<br>`Math.ceil()`<br>`Math.round()`<br>`Math.trunc()`|소수점 처리|
|`num.toFixed(n)`|소수점 이하 `n`자리까지 남도록 반올림|
|`isNaN(val)`|`val`이 `NaN`인지 판별|
|`isFinite(val)`|`val`이 finite한 수인지 판별|
|`Object.is(v1, v2)`|`v1`, `v2`가 SameValue인지 판별|
|`parseInt(str[, radix])`|`str`을 `radix` 진법으로 파싱함|
|`parseFloat(str)`|`str`을 소수점까지 파싱함|
|`Math.random()`|`[0, 1)` 범위의 임의의 수 반환|
|`Math.max(a, b, c...)`<br>`Math.min(a, b, c...)`|max, min 반환|
|`Math.pow(n, pow)`|`n^pow` 반환|

- SameValue는 `===`과 비슷하지만, `(NaN, NaN)`은 같고, `(0, -0)`은 다름

### Tasks
- `num.toFixed(n)`는 소수점 이하 `n`까지 나오도록 실제 값을 반올림하기 때문에 오차가 발생 가능함  
	```javascript
	alert( 6.35.toFixed(1) ); // 6.3
	alert( 6.35.toFixed(20) ); // 6.34999999999999964473
	
	alert( Math.round(6.35 * 10) / 10); // 6.35 -> 63.5 -> 64(rounded) -> 6.4
	```
	따라서 `n` 번째 자리까지 구하기 위해선 마지막 줄같이 소수점 이하 `n` 번째 자리를 소수점 이하 1 번째 자리로 만든 후 `Math.round()`를 사용하는게 좋음
- `prompt`에서 취소를 누르면 `null`이 입력되는 것에 유의!!!

## Strings
`String`의 포맷은 항상 **UTF-16**임!(page encoding과는 연관이 없음)

### Quotes
quotes 중 backtick(`` ` ` ``)은 안에 변수를 포함(`${}`)하거나 줄바꿈을 할 수 있음  
추가로 backtick을 이용하면 template function을 사용할 수 있음:
- ``func`string` ``으로 사용
- string과 내장된 식을 받아서 처리할 수 있음([tagged template](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#tagged_templates)이라고도 불림)
- 자동완성같은 기능으로, 실무에서는 잘 사용하지 않는 듯

### Special characters

|Character|Description|
|:---|:---|
|`\n`|New line|
|`\r`|Carriage return<br>window에서는 line break가 `\r\n`으로 표현됨|
|`\'`, `\"`|Quotes|
|`\\`|Backslash|
|`\t`|Tab|
|`\b`, `\f`, `\v`|Backspace, Form feed, Vertical tab<br>호환성을 위해서 유지되지만, 현재는 사용되지 않음|
|`\xXX`|Unicode character with the given hexadecimal Unicode `XX`<br>e.g. `\x7A` = `'z'`|
|`\uXXXX`|Unicode symbol with the hex code `XXXX` in UTF-16 encoding|
|`\u{X...XXXXXX}`<br>(1 to 6 hex characters)|Unicode symbol with the given UTF-32 encoding|

- escape character `\`를 이용해서 특수문자를 표현

### String length
`length` property를 사용해서 구함:  
```javascript
alert( `My\n`.length ); // 3
```

### Accessing characters
1. square brackets `[]`
	- `str[0]`
	- 해당하는 문자가 없으면 `undefined` 리턴
2. `str.charAt(pos)`
	- `str.charAt(pos)`
	- 해당하는 문자가 없으면 empty string `''` 리턴
3. iterating
	- `for (let char of "Hello")`

### Strings are immutable
`String`의 일부를 수정할 수는 없음  
`String` 전체를 바꿀 수는 있음:  
```javascript
let str = 'Hi';
str[0] = 'h'; // doesn't work
alert( str[0] ); // H

str = 'h' + str[1]; // replace the string
alert( str ); // hi
```

### Changing the case
`toLowerCase()`, `toUpperCase()` method를 사용:  
```javascript
alert( 'Interface'.toUpperCase() ); // INTERFACE
alert( 'Interface'.toLowerCase() ); // interface
alert( 'Interface'[0].toLowerCase() ); // 'i'
```
- 한 문자에 대해서도 사용 가능

### Searching for a substring
#### str.indexOf
`str.indexOf(substr[, pos])` : `substr`을 `str`의 `pos` 번째 문자부터 찾아나감  
일치하는 부분이 있을 경우 시작하는 위치를 리턴, 없을 경우 `-1` 리턴:  
```javascript
let str = 'Widget with id';

alert( str.indexOf('Widget') ); // 0
alert( str.indexOf('widget') ); // -1
alert( str.indexOf('id', 2) ) // 12
```
- 대소문자 구별함
- `str.lastIndexOf(substr[, pos])`도 있음
	- `str`의 마지막부터 `substr`을 찾아나감

#### The bitwise NOT trick
JS에서 bitwise NOT `~`는 숫자를 32-bit 정수로 변환한 다음 NOT 연산을 실행함  
`~n`이 `-(n+1)`과 같다는 점을 이용해서 `indexOf`로 부분문자열을 찾지 못했을 때 조건을 간단히 할 수 있음  
=> `if (~str.indexOf("Widget"))`

큰 숫자는 잘리고, `~(2^31-1)`도 `0`이기 때문에 긴 문자열에 대해서는 사용할 수 없음  
최신의 JS에서는 `.includes` method를 이용함

#### includes, startsWith, endsWith
`str.includes(substr[, pos])`는 `str`에 `substr`이 들어있는지 판별함  
=> `true/false` 리턴

`str.startsWith(substr)`, `str.endsWith(substr)`는 `str`이 `substr`로 시작하거나, 끝나는지 판별함  
=> `true/false` 리턴

```javascript
alert( "Widget".startsWith("Wid") ); // true
alert( "Widget".endsWith("get") ); // true
```

### Getting a substring
1. `str.slice(start[, end])`
	- `str`의 `[start, end)` 부분문자열을 반환  
		`end`가 없을 경우 `start`부터 끝까지 포함한 부분문자열을 반환
	- `start`, `end`에 음수도 넣을 수 있음
2. `str.substring(start[, end])`
	- `str`의 `start`와 `end` 사이를 포함한 부분문자열을 반환  
		`slice`와 비슷하지만, `start`가 `end`보다 클 수 있음:  
		```javascript
		let str = "stringify";

		// these are same for substring
		alert( str.substring(2, 6) ); // "ring"
		alert( str.substring(6, 2) ); // "ring"

		// ...but not for slice:
		alert( str.slice(2, 6) ); // "ring" (the same)
		alert( str.slice(6, 2) ); // "" (an empty string)
		```
	- Negative arguments가 허용되지 않음
3. `str.substr(start[, length])`
	- `str`의 `start`부터 시작하는, 길이가 `length`인 부분문자열을 반환
	- `start`는 음수를 넣을 수 있음

> ※ `substr`은 JS specification에 나와있지 않아서 non-browser 환경에서는 지원하지 않을 수도 있음  
> 웬만하면 다 지원됨  
> `slice`는 음수도 인자로 넣을 수 있기 때문에 `substr`보다 유연함  
> 사실상 `slice`만 기억해도 충분함

### Comparing strings
문자끼리는 알파벳 순서로 비교 가능함  
ASCII를 이용하지 않고 UTF-16을 이용!

`str.codePointAt(pos)` : `str`의 `pos` 번째 문자의 코드 반환  
`String.fromCodePoint(code)` : `code`에 해당하는 문자 반환

#### Example
```javascript
alert( "z".codePointAt(0) ); // 122
alert( "Z".codePointAt(0) ); // 90

alert( String.fromCodePoint(90) ); // Z
alert( '\u005a' ); // Z(0x005a == 90)
```
- `\u` prefix를 사용해서 UTF-16 코드를 직접 입력할 수 있음

#### Correct comparisons
다른 언어들끼리 비교하기 위해서 ECMA-402 안의 `str.localeCompare(str2)` 함수를 사용하면 됨
- `str`이 `str2`보다 작으면 음수 리턴
- `str`이 `str2`보다 크면 양수 리턴
- 둘이 같으면 `0` 리턴

> ※ default로 diacritical marks(Ö와 같은 발음 구별 부호)가 알파벳(O와 같이)과 동일하게 처리됨

> ※ IE10 이하는 Intl.js라는 라이브러리가 필요함

### Internals, Unicode
#### Surrogate pairs
자주 사용되는 문자들은 2-byte code에 저장되지만, 잘 쓰이지 않는 문자들은 추가적으로 2바이트를 더해 surrogate pair로 인코딩됨:  
```javascript
alert( '𝒳'.length ); // 2, MATHEMATICAL SCRIPT CAPITAL X
alert( '😂'.length ); // 2, FACE WITH TEARS OF JOY
alert( '𩷶'.length ); // 2, a rare Chinese hieroglyph
```

`String.fromCodePoint`와 `str.codePointAt`은 surrogate pairs를 넣어도 정상적으로 작동함  
이 함수들이 개발되기 이전의 함수들인 `String.fromCharCode`와 `str.charCodeAt`은 surrogate pairs를 넣으면 제대로 작동하지 않음

```javascript
alert( '𝒳'[0] ); // strange symbols...
alert( '𝒳'[1] ); // ...pieces of the surrogate pair

alert( '𝒳'.charCodeAt(0).toString(16) ); // d835, between 0xd800 and 0xdbff
alert( '𝒳'.charCodeAt(1).toString(16) ); // dcb3, between 0xdc00 and 0xdfff

alert('𝒳'.codePointAt(0).toString(16)); // 1d4b3
alert('𝒳'.codePointAt(1).toString(16)); // dcb3 (*)

alert(String.fromCodePoint(0x1d4b3)); // 𝒳

alert('\u{1d4b3}'); // 𝒳
```
- 이전의 함수들은 surrogate pair를 분리해서 처리해줘야 함  
	surrogate pair의 첫 번째 문자는 `[0xd800, 0xdbff]` 사이의 코드,  
	두 번째는 `[0xdc00, 0xdfff]` 사이의 코드를 가짐
- 최신의 두 함수(`String.fromCodePoint`, `str.codePointAt`)은 surrogate pair도 정상적으로 한 문자처럼 처리함  
	하지만 `(*)`와 같이 두 번째 문자에 접근은 가능하고, surrogate pair는 두 개의 인덱스를 가지는 건 같음!

#### Diacritical marks and normalization
발음 구별 기호 중 자주 사용되는 것은 UTF-16에 등록되어 있지만, 나머지도 표현하기 위해서 문자를 조합 가능함:  
```javascript
alert( 'S\u0307' ); // Ṡ
alert( 'S\u0307\u0323' ); // Ṩ
```
- `\u0307`이 위에 점, `\u0323`이 아래 점임

두 코드의 순서를 바꾸면, 보기에는 똑같지만 `==`를 사용해서 비교할 경우 `false`를 반환함  
이것을 해결하기 위해 Unicode normalization을 사용함  
`str.normalize()`로 구현되어 있음:  
```javascript
alert( "S\u0307\u0323".normalize() == "S\u0323\u0307".normalize() ); // true
alert( "S\u0307\u0323".normalize().length ); // 1

alert( "S\u0307\u0323".normalize() == "\u1e68" ); // true
```
- `str.normalize()`를 사용하면 보기에 똑같은 문자들을 모두 같게 만들어 준다는 것을 알 수 있음
- normalization을 거친 문자는 code 상으로 여러 개가 합쳐졌어도 길이가 `1`이라는 것에 유의!

### Summary

|code|description|
|:---|:---|
|`str.length`|`str`의 길이 리턴|
|`str[n]`|`str`의 `n` 번째 문자(없으면 `undefined`) 리턴|
|`str.charAt(pos)`|`str`의 `pos` 번째 문자(없으면 `''`) 리턴|
|`for...of`|iterating할 때 사용|
|`str.toUpperCase()`<br>`str.toLowerCase()`|`str`을 대/소문자화|
|`str.indexOf(substr[, pos])`|`str`의 `pos` 번째 문자부터 오른쪽으로 `substr`을 찾고 첫 번째 위치(없으면 `-1`) 리턴|
|`str.lastIndexOf(substr[, pos])`|`str`의 `pos` 번째 문자부터 왼쪽으로 `substr`을 찾고 첫 번째 위치(없으면 `-1`) 리턴|
|`str.includes(substr[, pos])`|`str`에 `substr`이 있는지 판별<br>`true/false` 리턴|
|`str.startsWith(substr)`<br>`str.endsWith(substr)`|`str`이 `substr`로 시작/끝나는지 판별<br>`true/false` 리턴|
|`str.slice(start[, end])`|`str`의 `[start, end)`(`end` 없으면 끝까지) 리턴<br>`start`, `end`는 음수가 허용됨|
|`str.substring(start[, end])`|`start`와 `end` 사이의 부분문자열 리턴<br>`start`가 `end`보다 클 수 있지만, 음수가 허용되지 않음|
|`str.substr(start[, length])`|`str`에서 `start`부터 시작하고 길이가 `length`인 부분문자열 리턴<br>`start`는 음수가 허용됨|
|`str.codePointAt(pos)`|`str`의 `pos`번째 문자의 코드 리턴|
|`String.fromCodePoint(code)`|`code`에 해당하는 문자 리턴|
|`str.localeCompare(str2)`|`str`과 `str2`를 비교, (`<`, `>`, `==`) 각각의 경우에 (음수, 양수, 0) 리턴|
|`str.normalize()`|`str`을 Unicode normalization 처리함|
|`str.trim()`|`str`을 trim한 결과 리턴|
|`str.repeat(n)`|`str`을 `n`번 반복한 결과 리턴|

- `str.toUpperCase()`, `str.toLowerCase()`는 문자 하나에도 사용 가능
- 문자열을 비교할 때 기본적으로 발음 구별 기호들은 알파벳으로 취급됨

### Tasks
- `Number(str)` 보다 `+str`가 편리함

## Arrays
### Declaration
```javascript
let arr = new Array();
let arr = [];

let fruits = ["Apple", "Orange", "Plum"];
fruits[3] = 'Lemon';
alert( fruits.length ); // 4
alert( fruits ); // Apple,Orange,Plum,Lemon

let arr = [ 'Apple', { name: 'John' }, true, function() { alert('hello'); } ];
```
- 대부분 두 번째 방법 이용
- `append`같은 method 없이 원소를 바로 추가 가능
- `arr.length`로 길이 반환
- 배열 자체를 출력할 수도 있음(csv같이 나옴)
- pyhton의 list처럼 자료형에 제한이 없음
- object literal처럼 trailing comma를 사용할 수 있음

### Methods pop/push, shift/unshift
JS의 array는 아래 4가지 method를 사용해서 queue나 stack으로 활용 가능함:
- `pop`
	- array의 마지막 원소를 빼서 반환
	- `array.pop();`
- `push`
	- array의 마지막에 원소를 추가, 전체 길이 반환
	- `array.push(elem[, elem2...]);`
- `shift`
	- array의 첫 번째 원소를 빼서 반환
	- `array.shift();`
- `unshift`
	- array의 맨 처음에 원소를 추가, 전체 길이 반환
	- `array.unshift(elem[, elem2...]);`

### Internals
array도 근본적으로는 object이기 때문에, **reference로 복사됨**  
JS에서도 배열이 순서가 있는 데이터를 처리하는데 최적화가 되어있음  
하지만 배열을 아래 예시처럼 일반적인 객체로 사용하면 소용이 없어짐:  
```javascript
let fruits = []; // make an array

fruits[99999] = 5; // assign a property with the index far greater than its length

fruits.age = 25; // create a property with an arbitrary name
```
- array를 잘 못 사용하는 경우:
	- non-numeric property를 추가
	- 인덱스를 불연속적이게 정의
	- 배열을 역순으로 채움

### Performance
`push`, `pop`은 `O(1)`이지만, `unshift`, `shift`는 `O(n)`임!

### Loops
기본 `for`문, `for...of`, `for...in` 세 가지 방법으로 반복문을 돌릴 수 있음:
- `for...in`과 `for...of`를 사용하면 index는 알 수 없음
- `for...in`은 numeric이 아닌 property와 method에도 접근함  
	`for...in`은 일반적인 객체와 사용하는 것에 최적화되어있기 때문에 10-100배 정도 느림  
	=> array-like object와 사용하지 않는게 좋음

### A word about "length"
`length`는 배열 안에 값의 개수를 세는 것이 아닌, *가장 큰 인덱스* + 1로 계산됨:  
```javascript
let fruits = [];
fruits[123] = "Apple";

alert( fruits.length ); // 124
```
- 이런 식으로 쓰면 안됨!

`length`는 수정이 가능함:  
```javascript
let arr = [1, 2, 3, 4, 5];

arr.length = 2; // truncate to 2 elements
alert( arr ); // [1, 2]

arr.length = 5; // return length back
alert( arr[3] ); // undefined: the values do not return
```
- 배열에 들어있는 원소의 개수보다 작게 만들면 뒤쪽의 원소들은 없어짐  
	다시 길이를 늘려도 복구되지 않음  
	따라서 `arr.length = 0;`으로 간단하게 배열을 초기화할 수 있음

### new Array()
```javascript
let arr = new Array("Apple", "Pear", "etc");

let arr = new Array(2); // (*)
alert( arr[0] ); // undefined! no elements.
```
- `(*)`와 같이 선언하면 `vector<int> vi(2);`와 같이 원소가 선언되지만 안에 값이 없음

### Multidimensional arrays
```javascript
let matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

alert( matrix[1][1] ); // 5, the central element
```

### toString
array에는 `toString`만 존재(`Symbol.toPrimitive`, `valueOf`는 구현되어있지 않음):  
```javascript
let arr = [1, 2, 3];

alert( arr ); // 1,2,3
alert( String(arr) === '1,2,3' ); // true

alert( [] + 1 ); // "1"
alert( [1] + 1 ); // "11"
alert( [1,2] + 1 ); // "1,21"
```
- 배열은 csv처럼 변환됨
- `[]`와 같은 비어있는 배열은 `""`로 변환됨

### Don't compare arrays with `==`
`==`은 array를 위한 처리가 구현되어있지 않아서 다른 객체들처럼 처리됨:  
```javascript
alert( [] == [] ); // false, (1)
alert( [0] == [0] ); // false, (2)

alert( 0 == [] ); // true, (3)
alert('0' == [] ); // false, (4)
```
- `(1), (2)`는 operand가 양쪽 다 객체이기 때문에 객체끼리 비교
- `(3), (4)`는 `[]`가 내장 `toString`에 의해 `''`로 변환된 다음 알맞은 type으로 다시 변환됨  
	`(3)`에서는 숫자로 변환되는데 `''`가 `0`으로 변환되기 때문에 `ture`  
	`(4)`에서는 `'0'`과 `''`를 비교하기 때문에 `false`

> ※ `===`는 type이 다르면 바로 `false`, 같으면 `==`와 동일하게 비교!!

배열을 비교하기 위해선 원소를 하나하나 비교하거나 iteration methods를 사용해야 함

### Summary

|code|description|
|:---|:---|
|`arr.length`|`arr`의 길이 반환|
|`arr.push(val[, val2...])`<br>`arr.pop()`|`arr`의 뒤쪽에 원소 삽입/삭제|
|`arr.unshift(val[, val2...])`<br>`arr.shift()`|`arr`의 앞쪽에 원소 삽입/삭제|

- `unshift`, `shift`는 `O(n)`임
- 웬만하면 `for...of` 사용해서 탐색
- `arr.length=0;`으로 간단하게 초기화 가능

### Tasks
- `ar=ar+ar2;`를 실행하면 `ar`들이 `String`으로 변환된 후 합쳐져 `ar`의 type이 `String`으로 바뀜!!  
	`ar[0]`을 출력하면 첫 번째 원소가 아니라 첫 번째 문자가 출력됨
- `ar.push(ar2);`를 실행하면 `ar2`가 `ar`의 원소로 들어감  
	=> 둘 다 길이가 2였다면 실행한 후 `ar`의 길이는 4가 아니라 3이 됨
- method도 배열의 원소로 들어갈 수 있음:  
	```javascript
	let arr = ["a", "b"];

	arr.push(function() {
	  alert( this );
	})

	arr[2](); // a,b,function(){...}
	```
	- `arr[2]`에는 함수 자체가 들어가 있기 때문에 호출하면 `arr`이 리턴됨

## Array methods
### Add/remove items
`push/pop/unshift/shift` 이외에도 아래 method들이 있음

#### splice
array도 객체이므로 `delete`를 사용해서 property를 지울 수 있긴 하지만 index는 그대로 남음:  
```javascript
let arr = ["I", "go", "home"];

delete arr[2]; // remove "go"

alert( arr[2] ); // undefined

// now arr = ["I",  , "home"];
alert( arr.length ); // 3
```
- `delete obj.key`는 `key`에 해당하는 값을 지우는 것이기 때문에 index가 줄어들지는 않음

`arr.splice`을 사용하면 됨  
```javascript
arr.splice(start[, deleteCount, elem1, ..., elemN]);
```
- `arr`의 `start` 번째부터 `deleteCount`만큼 지운 다음 `elem1, ..., elemN`을 삽입하고,  
	지운 원소들의 배열을 반환함

#### Example
```javascript
let arr = ["I", "study", "JavaScript", "right", "now"];

// remove 3 first elements and replace them with another
arr.splice(0, 3, "Let's", "dance");
alert( arr ) // now ["Let's", "dance", "right", "now"]

let removed = arr.splice(0, 2);
alert( removed ); // "Let's", "dance"
```
- `deleteCount`에 `0`을 넣어서 삽입만 할 수 있음
- `start`는 음수가 허용됨

#### slice
```javascript
arr.slice([start[, end]]);
```
- `String`의 method함수 `str.slice(start[, end])`와 같은 기능임
- 인자 없이 `arr.slice()`를 실행하면 `arr`을 복사할 수 있음
- `arr`이 수정되는게 아니라 새로운 배열이 반환됨

#### concat
```javascript
arr.concat(arg1, arg2...);
```
- `arr`의 원소 + `arg...`로 이루어진 배열이 반환됨  
	**`arr`에 원소가 추가되지 않음!!**  
	`arr`에 추가하기 위해선 `arr = arr.concat(arg);`와 같이 사용해야 함
- `arg`로 array, value 둘 다 들어갈 수 있음
- 순서대로 추가됨
- `arg`가 array면 원소들이 반환되는 배열에 추가됨  
	array 이외의 type이면 `arg` 자체가 복사(shallow copy)되어 추가됨  
	
	e.g.  
	```javascript
	let arr = [1, 2];

	let arrayLike = {
	  0: "something",
	  length: 1
	};

	alert( arr = arr.concat(arrayLike) ); // 1,2,[object Object]
	alert( arr.length); // 3
	arr[2][0] = 'other';
	alert( arrayLike[0] ); // other
	
	arr.length = 2;
	
	let stra="asdf";
	alert( arr = arr.concat(stra) ); // 1,2,asdf
	arr[2]="iiii";
	alert(arr[2]); // iiii
	alert(stra); // asdf
	```
	- `.`으로 호출하기 위해선 valid variable identifier이어야 함(공백 없음, 숫자로 시작 x, 특수문자 x)
	- numeric property와 length만 있다해도 `new Array()`나 `[]`으로 선언하지 않으면 array-like object가 됨
	
	array-like object는 array처럼 원소가 추가되도록 만들 수 있음  
	=> `Symbol.isConcatSpreadable` property를 `true`로 설정하면 됨!  
	```javascript
	let arrayLike = {
	  0: "something",
	  1: "else",
	  [Symbol.isConcatSpreadable]: true,
	  length: 2
	};

	alert( [].concat(arrayLike) ); // something,else
	```

### Iterate: forEach
```javascript
arr.forEach(function(item, index, array) { ... });
```
- `item`, `index`, `array`는 필요하면 함수의 parameter로 사용 가능
- parameter name은 `item/index/array`로 고정된게 아니고 순서대로 저렇게 들어가는 듯

#### Example
```javascript
// for each element call alert
["Bilbo", "Gandalf", "Nazgul"].forEach(alert);

["Bilbo", "Gandalf", "Nazgul"].forEach((item, index, array) => {
  alert(`${item} is at index ${index} in ${array}`);
});
```
- 함수의 result는 무시됨

### Searching in array
#### indexOf/lastIndexOf and includes
`String`의 method들과 같음

- `arr.indexOf(item[, from])`
- `arr.lastIndexOf(item[, from])`
- `arr.includes(item[, from])`

> ※ 모두 비교할 때 `===`을 사용함  
> => `false`를 넣으면 falsy value가 아닌 `false`만 찾음

`includes` method는 `indexOf/lastIndexOf`와 다르게 `NaN`을 처리할 수 있음:  
```javascript
const arr = [NaN];
alert( arr.indexOf(NaN) ); // -1 (should be 0, but === equality doesn't work for NaN)
alert( arr.includes(NaN) );// true (correct)
```
- 포함 여부를 확인할 때는 `includes`를 사용하는게 좋음

#### find and findIndex
```javascript
let result = arr.find(function(item, index, array) { ... });
let result = arr.findIndex(function(item, index, array) { ... });
```
- argument로 들어가는 함수가 `true`를 반환할 경우 탐색을 멈추고 그 `item/index`을 반환  
	만족하는 `item/index`가 없을 경우 `undefined/-1` 반환

#### Example
```javascript
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

let user = users.find(item => item.id == 1);

alert(user.name); // John
```

#### filter
```javascript
let results = arr.filter(function(item, index, array) { ... });
```
- 함수가 `true`를 반환할 경우 result array에 item을 추가하고 반복을 계속함  
	반복이 끝난 후 result를 반환(만족하는 item이 없었다면 empty array가 반환됨)
- `find`와 유사하지만, `find`는 만족하는 item 하나만 찾아주는 반면 `filter`는 만족하는 모든 item을 찾아줌

#### Example
```javascript
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

// returns array of the first two users
let someUsers = users.filter(item => item.id < 3);

alert(someUsers.length); // 2
```

### Transform an array
#### map
```javascript
let result = arr.map(function(item, index, array) { ... });

/*-------------example--------------*/

let lengths = ["Bilbo", "Gandalf", "Nazgul"].map(item => item.length);
alert(lengths); // 5,7,6
```
- argument로 들어가는 함수를 사용해서 `arr`의 item을 매핑하고, 그 결과를 반환

#### sort(fn)
```javascript
arr.sort([function() { ... }]);

/*-------------example--------------*/

let arr = [ 1, 2, 15 ];
arr.sort();
alert( arr );  // 1, 15, 2

function compareNumeric(a, b) {
  if (a > b) return 1;
  if (a == b) return 0;
  if (a < b) return -1;
}

arr.sort(compareNumeric);
alert(arr);  // 1, 2, 15
```
- `sort`도 정렬된 array를 반환하긴 하지만, `arr` 자체도 바뀌기 때문에 보통 리턴값을 사용하지 않음
- 인자를 넣지 않으면 `String`을 기준으로 정렬함
	- 비교함수를 넣어서 정렬 기준을 바꿀 수 있음  
		비교함수는 `(a, b)`를 비교할 때 `a`가 더 크면 양수, `b`가 더 크면 음수를 리턴하도록 구현하면 됨  
		=> `arr.sort( (a, b) => a-b )`로 코드를 간결하게 만들 수 있음

> ※ chrome에서는 항상 stable sort로 정렬됨

string을 비교하는 경우 `localeCompare`을 사용하는게 좋음:  
```javascript
let countries = ['Österreich', 'Andorra', 'Vietnam'];

alert( countries.sort( (a, b) => a > b ? 1 : -1) );
// Andorra, Vietnam, Österreich (wrong)

alert( countries.sort( (a, b) => a.localeCompare(b) ) );
// Andorra,Österreich,Vietnam (correct!)
```

#### reverse
```javascript
arr.reverse();

/*-------------example--------------*/

let arr = [1, 2, 3, 4, 5];
arr.reverse();

alert( arr ); // 5,4,3,2,1
```
- `sort`와 마찬가지로 reversed array를 반환함

#### split and join
```javascript
str.split([delim[, limit]]);

/*-------------example--------------*/

let names = 'Bilbo, Gandalf, Nazgul';

let arr = names.split(', '); // ['Bilbo', 'Gandalf', 'Nazgul']
```
- `delim`이 생략되면 `str` 전체가 하나의 element로 들어감  
	`delim`에 문자열이 들어갈 수 있음  
	`delim`이 `str`의 시작/끝에 나타나면 empty string이 시작/끝에 element로 들어감
- `limit`이 `0`이면 empty array를 반환  
	배열의 길이가 `limit`가 되기 전에 `str`의 끝에 다다르면 바로 종료됨  
	(배열의 길이가 `limit`가 되도록 채우지 않음)

```javascript
arr.join(glue);

/*-------------example--------------*/

let arr = ['Bilbo', 'Gandalf', 'Nazgul'];

let str = arr.join(';'); // glue the array into a string using ;

alert( str ); // Bilbo;Gandalf;Nazgul
```
- `glue`를 넣지 않으면 원소만 이음

#### reduce/reduceRight
```javascript
let value = arr.reduce(function(accumulator, item, index, array) { ... }, [initial]);
let value = arr.reduceRight(function(accumulator, item, index, array) { ... }, [initial]);

/*-------------example--------------*/

let arr = [1, 2, 3, 4, 5];
let result = arr.reduce((sum, current) => sum + current, 0);

alert(result); // 15
```
- array를 기반으로 값을 도출할 때 사용
- `accumulator` : 이전 호출의 결과(`initial`이 있는 경우 처음에는 `initial`)  
	반복이 끝난 뒤 `accumulator`가 `reduce`의 결과로 반환됨
- empty array에서 `initial` 없이 `reduce`를 호출할 경우 에러남!

### Array.isArray
array도 `object` type에 속하기 때문에 `typeof`로 타입을 알 수 없음  
=> `Array.isArray(value)`으로 배열인지 판별

### Most methods support "thisArg"
array method 중 `find`, `filter`, `map`과 같이 함수를 argument로 호출하는 method들은 `thisArg`를 추가적으로 붙일 수 있음:  
```javascript
arr.find(func, thisArg);
arr.filter(func, thisArg);
arr.map(func, thisArg);
```
- `thisArg`는 optional last argument임
- `thisArg`의 값은 `func`의 `this`가 됨

#### Example
```javascript
let army = {
  minAge: 18,
  maxAge: 27,
  canJoin(user) {
    return user.age >= this.minAge && user.age < this.maxAge;
  }
};

let users = [
  {age: 16},
  {age: 20},
  {age: 23},
  {age: 30}
];

// find users, for who army.canJoin returns true
let soldiers = users.filter(army.canJoin, army);

alert(soldiers.length); // 2
alert(soldiers[0].age); // 20
alert(soldiers[1].age); // 23
```
- `army.canJoin`은 method로 호출된게 아니라 `filter`의 argument로 들어간 것이기 때문에 함수의 구현부(코드)만 인자로 들어간 상태임  
	=> 실행될 때 `this`가 가리키는 것은 없는 상태이기 때문에 `thisArg`로 `this`를 표시해줘야 함  
	
	`users.filter(user => army.canJoin(user));`로 `thisArg` 없이 사용할 수 있음

### Summary

|code|description|
|:---|:---|
|`arr.splice(start[, deleteCount, elem1, ..., elemN])`|`arr`의 `start` 번째부터 `deleteCount`만큼 지운 다음 `elem1, ..., elemN`을 삽입하고, 지운 원소들의 배열을 리턴<br>`arr`도 변화함|
|`arr.slice([start[, end]])`|`arr`의 `[start, end)`를 리턴|
|`arr.concat(arg1, arg2...)`|`arr`에 `arg...`을 더한 배열을 리턴|
|`arr.forEach(function(item, index, array) { ... })`|`arr`의 원소들을 순회하면서 함수에 대입함|
|`arr.indexOf(item[, from])`<br>`arr.lastIndexOf(item[, from])`|`arr`의 `from` 번째부터 `item`을 찾고 첫 번째 일치하는 원소의 인덱스(없으면 `-1`)을 리턴<br>`arr`의 `from`부터 왼쪽으로 `item`을 찾고 첫 번째 일치하는 원소의 인덱스(없으면 `-1`)을 리턴|
|`arr.includes(item[, from])`|`arr`의 `from` 번째부터 `item`이 존재하는지 판별<br>`true/false` 리턴|
|`arr.find(function(item, index, array) { ... })`<br>`arr.findIndex(function(item, index, array) { ... })`|함수가 `true`를 반환하면 탐색을 멈추고 해당 원소 리턴<br>`arr.find`와 같지만, 해당 index 리턴|
|`arr.filter(function(item, index, array) { ... })`|함수를 `true`로 만드는 원소들의 배열 리턴|
|`arr.map(function(item, index, array) { ... })`|함수로 `arr`을 매핑하고 result array를 리턴|
|`arr.sort([function() { ... })`|함수를 기준으로 정렬한 결과를 리턴<br>`arr`도 변화함<br>함수를 생략하면 string으로 비교해서 정렬함|
|`arr.reverse()`|`arr`을 역순으로 정렬하고 결과 리턴<br>`arr`도 변화함|
|`str.split([delim[, limit]])`|`str`을 `delim`으로 구분하고 `limit` 개까지만 array에 저장 후 리턴<br>아무 것도 넣지 않을 경우 나눠지지 않고, `''`을 넣을 경우 한 글자씩 나눠짐|
|`arr.join(glue)`|`arr`의 원소들을 `glue`를 사이에 넣어서 이은 string을 리턴|
|`arr.reduce(function(accumulator, item, index, array) { ... }, [initial])`|`arr`의 원소들을 함수에 넣으면서 `accumulator`에 결과를 저장하고 반환<br>`initial`은 `accumulator`의 초기값|
|`arr.reduceRight(function(accumulator, item, index, array) { ... }, [initial])`|`arr.reduce`와 같은 기능이지만 원소들을 역순으로 처리함|
|`Array.isArray(value)`|`value`가 `Array` type인지 판별|
|`arr.some(function(item, index, array) { ... })`<br>`arr.every(function(item, index, array) { ... })`|`arr` 안에 함수를 `true`로 만드는 원소가 있는지 판별<br>모든 원소가 함수를 `ture`로 만드는지 판별|
|`arr.fill(value[, start[, end]])`|`arr`의 `[start, end)`를 `value`로 채우고 리턴<br>`arr`도 변화함|
|`arr.copyWithin(target[, start[, end]])`|`arr`의 `[start, end)`를 `target` 번째부터 시작해서 붙여넣고 리턴<br>`arr`도 변화함|
|`arr.flat([depth])`|`arr`의 원소들을 `depth`만큼 차원을 낮춘 결과를 리턴<br>`depth`를 `Infinity`로 설정할 수 있음|
|`arr.flatMap(function(item, index, array) { ... })`|`arr`의 원소들을 함수로 매핑 후 한 차원 낮춘 결과를 리턴|

- `arr.concat`은 shallow copy이기 때문에 객체의 배열은 deep copy를 따로 해야함
- `includes`는 `NaN`도 찾을 수 있음  
	cf. `NaN === NaN`이 `false`이기 때문에 `indexOf`로는 찾지 못함
- 함수를 argument로 받는 method들은 `thisArg` parameter를 추가할 수 있음  
	(argument인 함수가 method일 때 `this`가 가리키는 객체 지정)
- `arr.every`를 이용해서 배열 2개가 같은지 판별할 수 있음:  
	```javascript
	function arraysEqual(arr1, arr2) {
	  return arr1.length === arr2.length && arr1.every((value, index) => value === arr2[index]);
	}

	alert( arraysEqual([1, 2], [1, 2])); // true
	```
- 호출 후 `arr`도 변화하는 함수들:
	- `arr.splice`
	- `arr.sort`
	- `arr.reverse`
	- `arr.fill`
	- `arr.copyWithin`

### Tasks
- string을 `-`로 split하고 첫 번째 단어 제외 camelize:  
	```javascript
	function camelize(str) {
	  return str.split('-')
	  .map((word, index) => index == 0 ? word : word[0].toUpperCase() + word.slice(1))
	  .join('');
	}
	```
- `forEach`도 반복문과 비슷하게 인덱스를 기반으로 돌아감  
	=> 안에서 `splice` 등으로 배열의 index가 바뀔 경우 영향을 받음  
	e.g. `splice(i, 1)`과 같이 원소 하나를 뺄 경우 반복문처럼 i 바로 다음 원소는 순회하지 않음!
- `f(ar)`에서 arr을 argument로 넘기면, arr의 레퍼런스가 argument로 들어감  
	=> 레퍼런스를 이용해서 method, property를 호출하면 arr을 수정할 수 있지만, 그냥 ar에 배열을 대입하려 하면 함수의 local variable ar에 대입되기 때문에 함수 밖의 arr은 수정되지 않음
- 확장 가능한 계산기 만들기:  
	operator, expression을 분리할 필요 없이 operator를 property로 사용하는 객체를 property로 사용하면 됨  
	```javascript
	this.methods = {
      "-": (a, b) => a - b,
      "+": (a, b) => a + b
    };
	```
- arrow function에서 object literal을 리턴할 경우 `({ ... })`와 같이 괄호로 감싸야 함  
	∵ arrow function에는 `value => expr`, `value => { ... }`와 같이 두 종류가 있음!
- cpp에서의 string은 객체라서 때문에 문자 하나를 수정 가능하지만,  
	JS의 string은 primitive이기 때문에 문자 하나의 수정은 불가능함
- shuffle an array
	- `arr`에서 하나씩 골라 집어넣는 방법(`O(N^2)`)  
		```javascript
		function shuffle(arr) {
		  let iar=[];
		  for(let i=0;i<arr.length;i++)
			iar.push(arr[i]);
		  for(let i=0;i<arr.length;i++) {
			let t=Math.trunc(Math.random()*iar.length);
			arr[i]=iar[t];
			iar.splice(t, 1);
		  }
		}
		```
	- Fisher-Yates shuffle(`O(N)`)  
		```javascript
		function shuffle(array) {
		  for (let i = array.length - 1; i > 0; i--) {
			let j = Math.floor(Math.random() * (i + 1));
			[array[i], array[j]] = [array[j], array[i]];
		  }
		}
		```
		- `[a, b] = [b, a]`는 destructing assignment로, 나중에 다룰 예정
		- 모든 케이스가 동일한 확률을 가짐
- `arr.reduce`를 사용해서 데이터들을 하나의 객체로 변환할 수 있음

## Iterables
객체가 array가 아니더라도 데이터의 모음(list, set 등)으로 표현되면, *iterable*로 만들어 `for...of`로 효과적으로 순회하도록 만들 수 있음

### Symbol.iterator
```javascript
let range = {
  from: 1,
  to: 5
};

range[Symbol.iterator] = function() {  // 1
  return { // 2
    current: this.from,
    last: this.to,

    // 3
    next() { // 4
      if (this.current <= this.last) {
        return { done: false, value: this.current++ };
      } else {
        return { done: true };
      }
    }
  };
};


for (let num of range) {
  alert(num); // 1, then 2, 3, 4, 5
}
```
- `range`를 iterable로 만들기 위해서 `[Symbol.iterator]()` method를 추가해야 함  
	`Symbol.iterator` : 객체를 iterable하게 만들기 위해 존재하는 내장 symbol  
	1. `for...of`가 처음 실행될 때 이 메소드를 호출함  
		이 메소드는 *iterator*(`next`라는 method를 가지는 객체)를 리턴해야 함  
		이 메소드를 찾지 못하면 에러를 반환함
	2. `for...of`는 리턴된 iterator로만 실행됨
	3. `for...of`가 다음 iteration으로 넘어가려 할 때마다 `next()`를 호출함
	4. `next()`는 `{done: Boolean, value: any}` 형식의 객체를 리턴해야 함  
		`done=true`는 iteration이 끝났다는 것을 의미함  
		그게 아니면 `value`에 다음 값을 넣어야함
- `next()`가 리턴하는 객체의 key는 이름을 바꾸면 에러남
- `range` 자체를 iterator로 만들어도 됨:  
	```javascript
	let range = {
	  from: 1,
	  to: 5,

	  [Symbol.iterator]() {
		this.current = this.from;
		return this;
	  },

	  next() {
		if (this.current <= this.to) {
		  return { done: false, value: this.current++ };
		} else {
		  return { done: true };
		}
	  }
	};
	```
	- `Symbol.iterator` method에서 iterator를 다른 객체로 만들어 리턴하지 않고, `range` 자신을 리턴함  
		=> `range`에 `next()`가 선언되어 있어야 함
- 하나의 `range`로 중첩된 `for...of`를 돌릴 수 없음  
	안쪽 반복이 끝난 후 `current`가 공유되기 때문에 바깥쪽 반복도 바로 종료됨

### String is iterable
`Array`와 `String`이 널리 쓰이는 내장 iterable임  
`String`의 경우 `for...of`를 돌리면 문자 하나씩 순회함:  
```javascript
for (let char of "test") {
  // triggers 4 times: once for each character
  alert( char ); // t, then e, then s, then t
}

let str = '𝒳😂';
for (let char of str) {
    alert( char ); // 𝒳, and then 😂
}
```
- surrogate pair로 이루어진 문자열을 넣어도 정상적으로 작동함!

### Calling an iterator explicitly
iterator을 명시적으로 호출할 수도 있음:  
```javascript
let str = "Hello";

// does the same as
// for (let char of str) alert(char);

let iterator = str[Symbol.iterator]();

while (true) {
  let result = iterator.next();
  if (result.done) break;
  alert(result.value); // outputs characters one by one
}
```
- `for...of`를 호출한 것과 같은 결과임
- string은 method를 호출할 때 wrapper object가 생성되기 때문에 따로 method를 정의해도 그 구문 뒤에 바로 사라짐

### Iterables and array-likes
- iterable : `[Symbol.iterator]()` method를 구현한 객체
	- `for...of` 반복문에 넣을 수 있음
- array-like : indexes, `length`를 key로 가지는 객체
	- numeric indexes를 가짐

string은 iterable이면서(`for...of`에서 작동함) array-like(numeric indexes, `length`가 존재)임  
보통은 iterable이거나 array-like이거나 둘 중에 하나임  
둘 다 `push`, `pop`과 같은 method가 없다는 것은 같음

### Array.from
`Array.from` method를 사용해서 iterable이나 array-like로 진짜 `Array` type으로 만들 수 있음:  
```javascript
Array.from(obj[, mapFn, thisArg]);

/*-------------example--------------*/

let arrayLike = {
  0: "Hello",
  1: "World",
  length: 2
};

let arr = Array.from(arrayLike); // (*)
alert(arr.pop()); // World (method works)

let str = '𝒳😂';

// splits str into array of characters
let chars = Array.from(str);

alert(chars[0]); // 𝒳
alert(chars[1]); // 😂
alert(chars.length); // 2
```
- iterable, array-like 모두에 대해서 작동함
- surrogate pairs에 대해서도 정상적으로 작동함

### Summary

|code|description|
|:---|:---|
|`range.[Symbol.iterator]()`|객체 `range`를 iterable로 만들기 위해서 정의해야 함<br>iterator 객체를 리턴해야 함|
|`iterator.next()`|`iterator`가 다음 반복으로 넘어가기 전에 호출하는 함수<br>`done`, `value` property를 가진 객체를 리턴해야 함|
|`Array.from(obj[, mapFn, thisArg])`|iterable 또는 array-like 객체인 `obj`를 `Array` type으로 바꾸고 `mapFn`을 사용해서 매핑한 배열을 리턴|

- `[Symbol.iterator]()` method는 `for...of`가 호출될 때 자동으로 실행됨
- `String`, `Array` 같은 built-in iterables도 위 메소드가 구현되어 있음
- string iterable을 이용하면 surrogate pairs를 수월하게 처리 가능

## Map and Set
object를 사용해서 keyed collection을 저장  
array를 사용해서 ordered collection을 저장

### Map
Map은 object와 비슷하게 keyed data를 저장하지만, **모든 타입의 key를 허용**함  
기본적인 method, property들:
- `new Map([entries])` : entries로 초기화된 map 리턴
- `map.set(key, value)` : `key`와 `value`를 저장하고 `map` 리턴
	- 자신을 리턴하기 때문에 chaining이 가능함
- `map.get(key)` : `key`에 해당하는 값(`key`가 존재하지 않으면 `undefined`)을 리턴
- `map.has(key)` : `key`가 존재하면 `true`, 아니면 `false` 리턴
- `map.delete(key)` : `key`와 해당하는 `value`를 삭제
	- 성공적으로 삭제했다면 `true`, 해당하는 `key`가 었다면 `false` 리턴
- `map.clear()` : `map`을 비움
- `map.size` : `map`의 현재 원소 수를 리턴

> ※ `map[key]`로 해도 property를 추가할 수 있지만, 이 문법은 일반 객체에 적용되는 제한(string/symbol key만 가능)을 적용시킴  
> 따라서 `Map`의 method인 `set`, `get`을 사용하는게 좋음

`Map`은 객체도 key로 사용할 수 있음  
cf. 일반 객체는 객체를 key로 사용하면 모든 객체가 `"[object Object]"`로 변환되기 때문에, 다른 객체를 넣어도 `obj["[object Object]"]`라는 property 하나로 처리됨

> ※ `Map`은 SameValue 알고리즘을 이용해서 key들을 비교함  
> 이 알고리즘은 수정될 수 없음

### Iteration over Map
`Map`을 순회하는 3가지 method:
- `map.keys()` : key의 iterable을 리턴
- `map.values()` : value의 iterable을 리턴
- `map.entries()` : `[key, value]`의 iterable을 리턴
	- `Map`을 `for...of`를 사용하여 순회할 때 default로 호출됨

#### Example
```javascript
let recipeMap = new Map([
  ['cucumber', 500],
  ['tomatoes', 350],
  ['onion',    50]
]);

// iterate over keys (vegetables)
for (let vegetable of recipeMap.keys()) {
  alert(vegetable); // cucumber, tomatoes, onion
}

// iterate over values (amounts)
for (let amount of recipeMap.values()) {
  alert(amount); // 500, 350, 50
}

// iterate over [key, value] entries
for (let entry of recipeMap) { // the same as of recipeMap.entries()
  alert(entry); // cucumber,500 (and so on)
}
```
- `Map`은 값이 삽입된 순서대로 순회함  
	cf. 일반 객체는 반복할 때 Integer property일 경우 정렬한 순서대로 순회함

> ※ `Map`도 `Array`와 비슷하게 `forEach` method를 가지고 있음:  
```javascript
// runs the function for each (key, value) pair
recipeMap.forEach( (value, key, map) => {
  alert(`${key}: ${value}`); // cucumber: 500 etc
});
```

### Object.entries: Map from Object
`Map`을 생성할 때 array나 다른 iterable을 argument로 사용해서 초기화할 수 있음:  
```javascript
// array of [key, value] pairs
let map = new Map([
  ['1',  'str1'],
  [1,    'num1'],
  [true, 'bool1']
]);

alert( map.get('1') ); // str1
```
- 다른 iterable도 key/value pair가 property로 들어가 있어야 하고 `next()`를 정의할 수 있어야 하기 때문에, `Map`을 초기화할 때 사용하기 위해선 해봤자 integer property를 가지는 객체일 듯

`Object.entries(obj)` : `obj` -> entries  
```javascript
let obj = {
  name: "John",
  age: 30
};

let map = new Map(Object.entries(obj));

alert( map.get('name') ); // John
```
- `Object.entries(obj)`는 `Map`의 constructor 안에 들어가는 entries를 `obj`로부터 만들어서 반환함  
	이 코드에서는 `[ ["name","John"], ["age", 30] ]`를 리턴함

### Object.fromEntries: Object from Map
`Object.fromEntries(entries)` : `entries` -> obj  
```javascript
let prices = Object.fromEntries([
  ['banana', 1],
  ['orange', 2],
  ['meat', 4]
]);

// now prices = { banana: 1, orange: 2, meat: 4 }

alert(prices.orange); // 2
```
- parameter가 꼭 `Array`일 필요는 없음  
	iterable object면 됨 => map을 바로 넣어도 됨  
	e.g. `obj = Object.fromEntries(map)`

### Set
`Set`를 이용해서 set of values를 저장  
key가 없고 각 값들은 여러 번 추가해도 처음 한 번만 저장됨  
기본적인 method, property들:
- `new Set([iterable])` : `iterable`의 values로 초기화된 set 리턴
- `set.add(value)` : `value`를 추가하고 자신을 리턴
- `set.delete(value)` : `value`가 존재하면 삭제하고 `true`, 아니면 `false` 리턴
- `set.has(value)` : `value`가 존재하면 `true`, 아니면 `false` 리턴
- `set.clear()` : `set`을 비움
- `set.size` : `set`의 현재 원소 개수 리턴

> uniqueness check가 필요한 자료구조에 효율적

### Iteration over Set
`for...of`, `forEach` 둘 다 사용 가능:  
```javascript
let set = new Set(["oranges", "apples", "bananas"]);

for (let value of set) alert(value);

// the same with forEach:
set.forEach((value, valueAgain, set) => {
  alert(value);
});
```
- `forEach`를 사용할 때 callback function에 parameter가 3개임에 주의!  
	`valueAgain`은 `Map`과의 호환성을 위한 것임  
	`Map`을 `Set`으로 바꿀 때 유용함
- `Map`과 비슷하게 아래의 메소드들을 `for...of`에서 사용 가능
	- `set.keys()` : value의 iterable을 리턴
	- `set.values()` : value의 iterable을 리턴
	- `set.entries()` : `[value, value]`의 iterable을 리턴
	
	`Map`과의 호환을 위해서 구현됨

### Summary

|code|description|
|:---|:---|
|**Map**| |
|`new Map([entries])`|`entries`로 초기화된 map 리턴|
|`map.set(key, value)`|`key`와 `value`를 저장하고 `map` 리턴|
|`map.get(key)`|`key`에 해당하는 값(존재하지 않으면 `undefined`) 리턴|
|`map.has(key)`|`key`가 존재하면 `ture`, 아니면 `false` 리턴|
|`map.delete(key)`|`key`, `value`가 존재하면 삭제하고 `true`, 아니면 `false` 리턴|
|`map.clear()`|`map`을 비움|
|`map.size`|`map`의 현재 원소 수를 리턴|
|`map.keys()`<br>`map.values()`<br>`map.entries()`|key의 iterable을 리턴<br>value의 iterable을 리턴<br>`[key, value]`의 iterable을 리턴|
|`Object.entries(obj)`|`obj`로부터 entries의 **array**를 만들어서 리턴|
|`Object.fromEntries(entries)`|`entries`로부터 object를 만들어서 리턴<br>`entries`는 꼭 array를 이용하지 않아도 entries를 포함한 iterable이면 됨|
|**Set**| |
|`new Set([iterable])`|`iterable`의 values로 초기화된 set 리턴|
|`set.add(value)`|`value`를 추가하고 `set` 리턴|
|`set.delete(value)`|`value`가 존재하면 삭제하고 `true`, 아니면 `false` 리턴|
|`set.has(value)`|`value`가 존재하면 `true`, 아니면 `false` 리턴|
|`set.clear()`|`set`을 비움|
|`set.size`|`set`의 현재 원소 수를 리턴|
|`set.keys()`<br>`set.values()`<br>`set.entries()`|value의 iterable을 리턴<br>value의 iterable을 리턴<br>`[value, value]`의 iterable을 리턴|

- `Object` : collection of keyed values  
	`Map` : collection of keyed values  
	`Array` : collection of ordered values  
	`Set` : collection of unique values
- `Set`에는 `Map`과의 호환성을 위해서 구현된 메소드가 많음

### Tasks
- `Array.from(obj)`는 **모든 Array-like, iterable에 대해 사용 가능**
- `Object.keys/values/entries`는 **array**를 리턴하는 반면,  
	`map/set.keys/values/entries`는 **iterable**을 리턴함
- `Array.from(iterable)`을 `[iterable]`로 간단한게 구현 가능

## WeakMap and WeakSet
`Map`은 객체도 key로 사용할 수 있는데, key로 사용되는 객체는 garbage collect되지 않음  
하지만 `WeakMap`은 key로 사용되는 객체가 garbage collect의 대상이 되는 것을 막아주지 않음

### WeakMap
`WeakMap`의 key는 object만 가능함  
object가 `WeakMap`의 key로 사용되는 상황에서 object로의 reference가 하나도 없다면 그 object는 `WeakMap`과 메모리에서 자동으로 지워짐(garbage collect됨):  
```javascript
let john = { name: "John" };

let weakMap = new WeakMap();
weakMap.set(john, "...");

john = null; // overwrite the reference

// john is removed from memory!
```

추가로, `WeakMap`은 iteration과 `keys/values/entries()`와 같은 method를 지원하지 않고, 아래의 method만 지원함:
- `weakMap.get(key)`
- `weakMap.set(key, value)`
- `weakMap.delete(key)`
- `weakMap.has(key)`

=> 모든 key나 value를 알아낼 수 없음  
∵ 객체가 다른 reference를 가지지 않으면 garbage collect의 대상이 되지만, garbage collection이 언제 일어나는지는 JS engine에 의해 결정되기 때문(바로 지워질지, 기다렸다가 한꺼번에 지워질지)  
즉, `WeakMap`의 현재 원소 개수는 알 수 없음

### Use case: additional data
`WeakMap`은 *additional data storage*로써 유용하게 사용됨  
third-party library에 속하거나 다른 이유로 객체 안에 property를 추가하는게 적합하지 않은 상황에서, 객체가 살아있는 동안에만 유효한 데이터를 저장하고 싶을 때 `WeakMap`이 적합한 자료구조임  
`WeakMap`에 데이터를 넣으면 key인 object가 garbage collect될 때 데이터도 자동으로 삭제되기 때문

#### Example
```javascript
// 📁 visitsCount.js using Map
let visitsCountMap = new Map(); // map: user => visits count

// increase the visits count
function countUser(user) {
  let count = visitsCountMap.get(user) || 0;
  visitsCountMap.set(user, count + 1);
}

// 📁 main.js
let john = { name: "John" };

countUser(john); // count his visits

// later john leaves us
john = null;

// 📁 visitsCount.js using WeakMap
let visitsCountMap = new WeakMap(); // weakmap: user => visits count

// increase the visits count
function countUser(user) {
  let count = visitsCountMap.get(user) || 0;
  visitsCountMap.set(user, count + 1);
}
```
- `Map`을 사용할 경우 `john`이 사라져도 수동으로 `visitsCountMap`에서 데이터를 삭제해야 함  
	프로젝트가 커지면 수동으로 삭제하는데 많은 자원이 들어감  
	=> `WeakMap`으로 해결

### Use case: caching
객체를 parameter로 받는 함수가 객체별로 결과를 저장(cache)해놓고 재사용할 수 있음  
이 때 `Map`보다 `WeakMap`을 사용하는게 적합함:  
```javascript
// 📁 cache.js
let cache = new WeakMap();

// calculate and remember the result
function process(obj) {
  if (!cache.has(obj)) {
    let result = /* calculate the result for */ obj;

    cache.set(obj, result);
  }

  return cache.get(obj);
}

// 📁 main.js
let obj = {/* some object */};

let result1 = process(obj);
let result2 = process(obj);

// ...later, when the object is not needed any more:
obj = null;

// Can't get cache.size, as it's a WeakMap,
// but it's 0 or soon be 0
// When obj gets garbage collected, cached data will be removed as well
```
- memoization과 비슷

### WeakSet
- `Set`과 유사하지만, 객체만 저장 가능
- `WeakMap`과 마찬가지로 객체가 reachable할 때만 `WeakSet`안에서 유지됨
- `WeakMap`과 마찬가지로 iteration 불가
	- `weakSet.add(value)`
	- `weakSet.has(value)`
	- `weakSet.delete(value)`
	
	위 3개의 method만 지원함

`WeakMap`과 마찬가지로 additional storage 역할이지만, 임의의 데이터가 아닌, "yes/no"만 표현하는 데이터를 위한 자료구조임  
e.g. 사용자의 방문 횟수가 아닌, 방문 여부

`WeakMap`과 `WeakSet`의 가장 큰 단점은 반복 작업이 불가능한 것과 현재의 모든 원소에 대한 정보(개수 등)을 알 수 없다는 점임  
다른 곳에서 관리되거나 저장된 객체들에 대한 "additional" storage를 제공하는 역할임을 생각해야 함

### Summary

|code|description|
|:---|:---|
|**WeakMap**| |
|`weakMap.get(key)`|`weakMap`에 `key`에 해당하는 값 리턴|
|`weakMap.set(key, value)`|`weakMap`에 `key`, `value`를 추가하고 `weakMap` 리턴|
|`weakMap.delete(key)`|`weakMap`에서 `key`가 존재하면 삭제 후 `true`, 아니면 `false` 리턴|
|`weakMap.has(key)`|`weakMap`에 `key`가 존재하는지 판별|
|**WeakSet**| |
|`weakSet.add(value)`|`value`를 추가하고 `weakSet` 리턴|
|`weakSet.has(value)`|`value`가 존재하는지 판별|
|`weakSet.delete(value)`|`value`가 존재하면 삭제하고 `true`, 아니면 `false` 리턴|

- `WeakMap`과 `WeakSet`은 secondary storage로서, primary storage에서 객체가 지워지면 이 자료구조들에서도 자동으로 지워짐

### Tasks
- 객체 안에 property를 추가할 수 있다면, symbolic property를 추가해서 다른 사람들은 접근할 수 없는 property를 만들어서 `WeakSet`, `WeakMap`의 역할을 대신할 수 있음
	- 구조적인 관점에서 보면 `WeakSet`이나 `WeakMap`을 사용하는게 나음(secondary storage라는 semantic role이 있기 때문)

## Object.keys, values, entries
`keys/values/entries()`는 모든 자료 구조들에 대해서 사용 가능하도록 약속되어 있음  
=> 자료구조를 만들게 된다면 이 메소드들도 구현해야 함

`Map`, `Set`, `Array`에 대해서는 이미 배움(iterable을 리턴함)  
`Object`에 대해서도 사용 가능하지만, **array를 리턴**함!
- `Object.keys(obj)` : keys의 array를 리턴
- `Object.values(obj)` : values의 array를 리턴
- `Object.entries(obj)` : `[key, value]`의 array를 리턴
	- 호출 방법이 `map.keys()`와 다른 것에 유의  
		∵ `obj`가 `keys`라는 method를 가질 수도 있기 때문

> ※ `Object.keys/values/entries`는 symbolic properties를 무시함!!
> `Object.getOwnPropertySymbols(obj)`가 symbolic keys만 나열된 array를 리턴  
> `Reflect.ownKeys(obj)`가 모든 key가 나열된 array 리턴

### Transforming objects
객체에는 array의 `map`, `filter`와 같은 method들이 없음  
하지만 아래와 같이 property들을 순회할 수 있는 방법이 존재:
1. `Object.entries(obj)`를 사용해서 `obj`로부터 key/value pair의 배열을 얻음
2. 얻은 배열에 배열의 method를 적용
3. 반환된 배열을 `Object.fromEntries(array)`로 다시 객체로 만듦

```javascript
let prices = {
  banana: 1,
  orange: 2,
  meat: 4,
};

let doublePrices = Object.fromEntries(
  // convert to array, map, and then fromEntries gives back the object
  Object.entries(prices).map(([key, value]) => [key, value * 2])
);

alert(doublePrices.meat); // 8
```

### Summary

|code|description|
|:---|:---|
|`Object.keys(obj)`<br>`Object.values(obj)`<br>`Object.entries(obj)`|`obj`의 key들의 array 리턴<br>`obj`의 value들의 array 리턴<br>`obj`의 `[key, value]`들의 array 리턴|
|`Object.fromEntries(array)`|entry들로 이루어진 `array`를 바탕으로 객체를 생성하고 리턴|

- `Object.keys/values/entries`는 `Map`이나 다른 객체들의 method와 같이 iterable이 아닌 `Array`를 리턴함에 주의!

```javascript
let arr = ['a', , 'c'];
let sparseKeys = Object.keys(arr);
let denseKeys = [...arr.keys()];
alert(sparseKeys); // ['0', '2']
alert(denseKeys);  // [0, 1, 2]

alert(arr[1]);
```
- `Object.keys(arr)`은 arr의 arr[n]의 값이 `undefined`면 무시하지만, `arr.keys()`는 무시하지 않고 모두 출력함!

## Destructuring assignment
*Destructuring assignment*는 배열이나 객체를 변수들로 분리하는 문법임  
Destructuring은 수많은 파라미터, 기본값을 가지는 복잡한 함수에도 알맞음

### Array destructuring
```javascript
// 1
let [firstName, surname] = "John Smith".split(' ');
alert(surname);  // Smith

// 2
let [firstName, , title] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];
alert( title ); // Consul

// 3
let [a, b, c] = "abc"; // ["a", "b", "c"]
let [one, two, three] = new Set([1, 2, 3]);

// 4
let user = {
  name: "John",
  age: 30
};

// loop over keys-and-values
for (let [key, value] of Object.entries(user)) {
  alert(`${key}:${value}`); // name:John, then age:30
}

// 5
[guest, admin] = [admin, guest];

```
1. `"John Smith".split(' ')`와 같이 배열을 리턴하는 method도 "destructurize" 가능함
2. `,`를 사용해서 원소를 무시할 수 있음
3. 오른쪽에는 모든 iterable이 올 수 있음
4. destructuring을 이용해서 entries를 순회할 수 있음
	- `Map`, `Set`도 가능함
5. 손쉽게 swap을 구현할 수 있음

> ※ Destructuring은 destructive와 다른 의미임  
> 객체를 분해하지만, 객체 자체에 영향을 주지는 않음

#### The rest `...`
```javascript
let arr = ["Julius", "Caesar", "Consul", "of the Roman Republic"];
let [name1, name2] = arr;

alert(name1); // Julius
alert(name2); // Caesar

let [name1, name2, ...rest] = arr;

alert(rest[0]); // Consul
alert(rest[1]); // of the Roman Republic
alert(rest.length); // 2
```
- 길이가 4인 배열을 `[a1, a2]`로 destructurize하면 배열의 3, 4번째 원소들은 무시됨
- `...`을 사용하면 남는 원소들을 한꺼번에 저장할 수 있음
	- `...` 다음에 남는 원소들을 저장할 변수의 이름을 넣음
	- destructuring assignment에서만 사용 가능
	- 항상 left-side의 마지막에 사용해야 함

#### Default values
```javascript
// default values
let [name = "Guest", surname = "Anonymous"] = ["Julius"];

alert(name);    // Julius (from array)
alert(surname); // Anonymous (default used)

// runs only prompt for surname
let [name = prompt('name?'), surname = prompt('surname?')] = ["Julius"];

alert(name);    // Julius (from array)
alert(surname); // whatever prompt gets
```
- destructuring을 사용할 때 left-side에 default value 설정 가능
	- `prompt`를 사용해서 부족한 값을 입력받을 수 있음

### Object destructuring
```javascript
let {var1, var2} = {var1:..., var2:...};

/*-------------example--------------*/

let options = {
  title: "Menu",
  width: 100,
  height: 200
};

// 1
let {title, width, height} = options;

// 2
let {width, title, height} = options;

// 3
let {width: w, height: h, title} = options;

// 4
let {width = 100, height = prompt("height?"), title} = options;

// 5
let {width: w = 100, height: h = 200, title} = options;
```
1. destructurize할 객체의 key를 left-side에 넣어야 함  
	=> `title`, `width`, `height`라는 변수 안에 property의 값이 저장됨
2. left-side의 변수의 순서들은 상관없음
3. left-side에서 `sourceProperty: targetVariable`과 같이 이름을 다시 설정 가능함
4. array destructuring 같이 default value를 설정 가능함
5. `:`와 `=`를 동시에 사용 가능함

#### The rest pattern `...`
array destructuring과 같이 남는 property들을 rest pattern `...`을 사용해서 다른 객체에 저장 가능함:  
```javascript
let options = {
  title: "Menu",
  height: 200,
  width: 100
};

let {title, ...rest} = options;

alert(rest.height);  // 200
```
- 나머지 property들은 `rest`라는 객체 안에 저장됨
	- old IE의 경우 Babel 등으로 polyfill 해야함

> ※ `let` 없이 destructuring을 사용하기 위해선 아래와 같이 괄호로 묶어야 함!  
> `({title, width, height} = {title: "Menu", width: 200, height: 100});`  
> ∵ JS는 `{...}`을 code block으로 인식하기 때문

### Nested destructuring
```javascript
let options = {
  size: {
    width: 100,
    height: 200
  },
  items: ["Cake", "Donut"],
  extra: true
};

let {
  size: {
    width,
    height
  },
  items: [item1, item2],
  title = "Menu"
} = options;

alert(title);  // Menu
alert(width);  // 100
alert(height); // 200
alert(item1);  // Cake
alert(item2);  // Donut
```
- left-side pattern을 알맞게 설정해서 중첩된 객체도 destructurize 가능

### Smart function parameters
함수의 parameter에도 destructuring을 적용 가능:  
```javascript
function({
  incomingProperty: varName = defaultValue
  ...
}) { ... }

/*-------------example--------------*/

let options = {
  title: "My menu",
  items: ["Item1", "Item2"]
};

function showMenu({
  title = "Untitled",
  width: w = 100,  // width goes to w
  height: h = 200, // height goes to h
  items: [item1, item2] // items first element goes to item1, second to item2
} = {}) {
  alert( `${title} ${w} ${h}` ); // My Menu 100 200
  alert( item1 ); // Item1
  alert( item2 ); // Item2
}

showMenu(options);
```
- 함수의 parameter가 많을 때 객체 하나로 담아서 보낸 후 분해해서 사용가능하게 만듦
- destructuring은 항상 argument가 존재한다고 가정하기 때문에 destructuring에도 기본값(`= {}`)을 넣어줘야 함!

### Summary

|code|description|
|:---|:---|
|`let [...] = array;`|array destructuring|
|`let {...} = obj;`|object destructuring|
|`...`|rest pattern<br>객체일 경우 새로운 객체 안에, 배열일 경우 새로운 배열을 저장 공간으로 사용함|

- 기존에 존재하는 변수에 대해 수행할 경우 전체 문장을 괄호로 묶어야 함

## Date and time
### Creation
```javascript
new Date()
new Date(milliseconds)
new Date(datestring)
new Date(year, month, date, hours, minutes, seconds, ms)

/*-------------example--------------*/

let now = new Date();
let Jan02_1970 = new Date(24 * 3600 * 1000);
let date = new Date("2017-01-26");
let date = new Date(2011, 0, 1);
```
- argument 없이 호출하면 현재 시간을 저장
- milliseconds는 1970.01.01 UTC 기준, 음수도 가능
- datestring은 GMT 기준 0시로 설정된 후 실행되는 환경의 timezone을 따라서 수정됨
- 직접 입력하는 경우 끝쪽부터 연속으로 0인 부분은 생략 가능

### Access date components
- `date.getFullYear()` : 4자리로 `date`의 연도 리턴
- `date.getMonth()` : `[0, 11]`으로 `date`의 달 리턴
- `date.getDate()` : `[1, 31]`으로 `date`의 일 리턴
- `date.getHours()/.getMinutes()/.getSeconds()/.getMilliseconds()` : `date`의 시/분/초/밀리초 리턴
- `date.getDay()` : `[0, 6]`으로 `date`의 요일 리턴(0이 일요일)

> ※ 위의 메소드들은 모두 실행 환경의 timezone이 기준임  
> get뒤에 UTC를 붙여서 UTC 기준으로 시간을 출력할 수도 있음

- `date.getTime()` : 1970.01.01 UTC으로부터 현재까지 지난 시간을 ms단위로 리턴
- `date.getTimezoneOffset()` : UTC와 현재 timezone의 차이를 분 단위로 리턴  
	timezone이 UTC-1이면 `60`이 리턴됨(UTC+0이 기준임)

> ※ UTC+1이면 UTC보다 1시간 빠름

### Setting date components
- `date.setFullYear(year[, month[, date]])`
- `date.setMonth(month[, date])`
- `date.setDate(date)`
- `date.setHours(hour[, min[, sec[, ms]]])`
- `date.setMinutes(min[, sec[, ms]])`
- `date.setSeconds(sec[, ms])`
- `date.setMilliseconds(ms)`
- `date.setTime(milliseconds)` : `date`의 시간을 1970.01.01 UTC 기준으로 `milliseconds` ms 만큼 지난 시간으로 설정

`setTime`을 제외한 메소드들은 UTC-variant를 가짐  
e.g. `setUTCHours`

> ※ argument 이외의 부분은 수정되지 않음!

### Autocorrection
윤년이나 범위를 넘어선 값들은 알아서 계산해서 대입함:  
```javascript
let date = new Date(2013, 0, 32); // 1 Feb 2013

let date = new Date(2016, 1, 28); // 28 Feb 2016
date.setDate(date.getDate() + 2); // 1 Mar 2016

date.setDate(0); // 최소가 1이기 때문에 이전 달의 말일으로 변경됨 = 29 Feb 2016
```
- 달의 경우 `[0, 11]`으로 표현됨에 주의
- 일은 `[1, 31]`로 표현됨

### Date to number, date diff
`Date` 객체가 `Number`로 변환되면 `date.getTime()`과 같은 결과가 나옴  
=> 1970.01.01부터 현재까지 경과한 ms를 반환함  
=> 아래와 같이 실행시간 측정에 사용 가능  
```javascript
let start = new Date();

// do the job
for (let i = 0; i < 100000; i++) {
  let doSomething = i * i * i;
}

let end = new Date();
alert( `The loop took ${end - start} ms` );
```

### Date.now()
시간을 측정하기 위해서 `Date` 객체를 선언할 필요는 없음  
`Date.now()` method를 사용하면 현재 timestamp(1970.01.01부터 경과한 ms)를 알 수 있음  
`new Date().getTime()`과 같은 기능이지만 객체를 생성하지 않기 때문에 더 빠름  
```javascript
let start = Date.now();

// do the job
for (let i = 0; i < 100000; i++) {
  let doSomething = i * i * i;
}

let end = Date.now();
alert( `The loop took ${end - start} ms` );
```

### Benchmarking
```javascript
function diffSubtract(date1, date2) {
  return date2 - date1;
}

function diffGetTime(date1, date2) {
  return date2.getTime() - date1.getTime();
}
```
- 각 함수를 100000번씩 돌리면 `diffGetTime`이 더 빠름
	- type conversion을 하지 않기 때문
- multi-process OS에서는 병렬로 작업을 처리되는 작업이 존재할 수 있으므로 각 함수들을 번갈아가면서 여러 번 측정해야 더 신뢰할 수 있는 결과를 얻을 수 있음  
	```javascript
	// added for "heating up" prior to the main loop
	bench(diffSubtract);
	bench(diffGetTime);

	// now benchmark
	for (let i = 0; i < 10; i++) {
	  time1 += bench(diffSubtract);
	  time2 += bench(diffGetTime);
	}
	```
	- JS의 engine은 자주 실행되는 'hot code'만을 최적화하기 때문에 벤치마킹할 코드를 미리 실행시켜 heat-up하는게 좋음
- 최신의 JS engine들은 최적화를 많이 하기 때문에 연산자나 내장 함수 등을 측정하는 것은 테스트와 실제 환경에서 많이 다를 수 있음

### Date.parse from a string
`Date.parse(str)`을 사용해서 `String`으로부터 timestamp를 파싱할 수 있음  
`str`의 format은 `YYYY-MM-DDTHH:mm:ss.sssZ`이어야 함:
- `YYYY-MM-DD` : year-month-day
- `"T"` : delimiter(character)
- `HH:mm:ss.sss` : hour-minute-second-millisecond
- `Z` : timezone(`+-hh:mm`)
	- `Z`만 사용하면 UTC+0을 나타냄

#### Example
```javascript
let ms = Date.parse('2012-01-26T13:51:50.417-07:00');
alert(ms); // 1327611110417  (timestamp)

let date = new Date( Date.parse('2012-01-26T13:51:50.417-07:00') );
alert(date);
```
- 입력 포맷이 잘못되면 `NaN` 리턴
- 결과값을 바로 `Date`의 생성자에 넣어서 `Date` 객체 생성 가능

### Summary

|code|description|
|:---|:---|
|`date.getFullYear()`|`date`의 연도를 4자리로 리턴|
|`date.getMonth()`|`date`의 달을 `[0, 11]`으로 리턴|
|`date.getDate()`|`date`의 일을 `[1, 31]`으로 리턴|
|`date.getHours()`<br>`date.getMinutes()`<br>`date.getSeconds()`<br>`date.getMilliseconds()`|`date`의 시/분/초/밀리초 리턴|
|`date.getDay()`|`date`의 요일을 `[0, 6]`으로 리턴<br>0이 일요일|
|`date.getTime()`|1970.01.01 UTC+0부터 현재까지 경과한 시간을 ms 단위로 리턴|
|`date.getTimezoneOffset()`|UTC+0과 현재 timezone의 차이를 분 단위로 리턴<br>UTC+0 기준임|
|`date.setFullYear(year[, month[, date]])`<br>`date.setMonth(month[, date])`<br>`date.setDate(date)`<br>`date.setHours(hour[, min[, sec[, ms]]])`<br>`date.setMinutes(min[, sec[, ms]])`<br>`date.setSeconds(sec[, ms])`<br>`date.setMilliseconds(ms)`|`date`의 시간 설정|
|`date.setTime(milliseconds)`|`date`의 시간을 1970.01.01 UTC 기준으로 `milliseconds` ms 만큼 지난 시간으로 설정|
|`Date.now()`|`new Date().getTime()`과 같음|
|`Date.parse(str)`|`YYYY-MM-DDTHH:mm:ss.sssZ` 포맷의 `str`을 파싱해서 timestamp 리턴<br>`str`의 포맷이 잘못된 경우 `NaN` 리턴|

- 이름에 "Time"이 들어가지 않은 method들은 `get/set` 다음에 `UTC`를 붙여서 UTC+0 기준으로 설정 가능(= UTC-variant)
- `set*` 메소드들은 argument 이외의 정보들은 수정되지 않음  
	리턴값은 설정된 시간의 timestamp임
- Month은 `[0, 11]`, Day는 `[0, 6]`, Date는 `[1, 31]`로 표현됨에 주의
- `Date`를 `Number`로 변환하면 `date.getTime()`과 같은 결과임
- JS는 마이크로초로 시간을 측정해주는 메소드를 지원하지 않음  
	browser가 `performance.now()`로 페이지가 로딩될 때부터 경과된 시간을 마이크로초로 측정하는 메소드 지원  
	Node.js는 `microtime` 모듈로 지원함

### Tasks
- `new Date(year, month+1, 0).getDate()`로 `year.month`의 마지막 날을 알 수 있음

## JSON methods, toJSON
복잡한 객체를 전송/로깅 등의 이유로 `String`으로 바꿔야 한다고 가정하자.  
`toString()` method를 구현하는 방법은 property가 바뀔 때마다 갱신해줘야 하고, 중첩된 객체가 있을 경우도 고려해야 하므로 비효율적임  
=> JSON을 이용해서 표현 가능

### JSON.stringify
JSON(JavaScript Object Notation) : 값과 객체를 나타내는 범용적인 format  
원래는 JS를 위해서 만들어졌지만, 다른 언어들도 JSON을 처리하는 라이브러리를 가짐  
따라서 client가 JS를 사용하면 JSON을 사용해서 데이터를 교환하는게 편리함

JS는 아래 메소드들을 지원함:
- `JSON.stringify(obj)` : `obj`를 JSON으로 변환
- `JSON.parse` : JSON을 객체로 변환

#### Example
```javascript
let student = {
  name: 'John',
  age: 30,
  isAdmin: false,
  courses: ['html', 'css', 'js'],
  wife: null
};

let json = JSON.stringify(student);

alert(typeof json); // string
alert(json);
/*
{
  "name": "John",
  "age": 30,
  "isAdmin": false,
  "courses": ["html", "css", "js"],
  "wife": null
}
*/
```
- JSON은 `typeof`로 조사하면 `String`으로 나옴
- JSON을 사용해서 도출된 string `json`은 *JSON-encoded/serialized/stringified/marshalled* object라고 불림
- JSON-encoded object는 object literal과 몇 가지 차이점이 존재함:
	- `String`은 오직 큰 따옴표로 표현됨
	- property name도 큰 따옴표로 표현됨

```javascript
alert( JSON.stringify(1) ) // 1

alert( JSON.stringify('test') ) // "test"

alert( JSON.stringify(true) ); // true

alert( JSON.stringify([1, 2, 3]) ); // [1,2,3]
```
- `JSON.stringify`는 primitive에도 적용 가능함
- JSON은 아래와 같은 data types를 지원함:
	- Objects `{ ... }`
	- Arrays `[ ... ]`
	- Primitives(strings, numbers, booleans, `null`)

> ※ JSON은 data-only, language-independent하기 때문에 JS-specific한 properties는 `JSON.stringify`가 무시함  
> e.g. methods, symbolic properties, `undefined`를 저장하고 있는 properties

중요한 점은 nested object를 지원한다는 것임!  
하지만 circular reference가 있으면 에러가 남  
```javascript
let room = {
  number: 23
};

let meetup = {
  title: "Conference",
  participants: ["john", "ann"]
};

meetup.place = room;       // meetup references room
room.occupiedBy = meetup; // room references meetup

JSON.stringify(meetup); // Error: Converting circular structure to JSON
```

### Excluding and transforming: replacer
`JSON.stringify`의 full syntax는 아래와 같음:  
```javascript
let json = JSON.stringify(value[, replacer[, space]]);
```
- `value` : 인코딩할 값
- `replacer` : 인코딩할 property가 저장된 배열 또는 mapping function `function(key, value)`
	- mapping function은 인코딩하지 않을 property에 대해서 `undefined`를 리턴하면 됨
- `space` : indent 설정

#### Example
```javascript
let room = {
  number: 23
};

let meetup = {
  title: "Conference",
  participants: [{name: "John"}, {name: "Alice"}],
  place: room // meetup references room
};

room.occupiedBy = meetup; // room references meetup

// 1
alert( JSON.stringify(meetup, ['title', 'participants']) );
// {"title":"Conference","participants":[{},{}]}

// 2
alert( JSON.stringify(meetup, ['title', 'participants', 'place', 'name', 'number']) );
/*
{
  "title":"Conference",
  "participants":[{"name":"John"},{"name":"Alice"}],
  "place":{"number":23}
}
*/

// 3
alert( JSON.stringify(meetup, function replacer(key, value) {
  alert(`${key}: ${value}`);
  return (key == 'occupiedBy') ? undefined : value;
}));
/* key:value pairs that come to replacer:
:             [object Object]
title:        Conference
participants: [object Object],[object Object]
0:            [object Object]
name:         John
1:            [object Object]
name:         Alice
place:        [object Object]
number:       23
occupiedBy: [object Object]
*/
```
- nested object에도 `replacer`가 적용됨  
	=> nested object도 포함시켜야 정상적으로 인코딩됨  
	배열로 나열하기 너무 길 경우 함수를 사용하면 됨
- `replacer`로 사용하는 함수에서의 `this`는 현재 property를 가지는 object를 가리킴
- 첫 번째 `alert`가 key가 없는 이유 : wrapper object이기 때문(key가 없고 value는 object 전체를 가리킴)

### Formatting: space
`JSON.stringify(value, replacer, space)`의 `space`는 인덴팅을 조절하기 위해서 사용됨  
숫자 대신 string을 넣으면 그 string을 사용해서 indentation을 수행함  
오직 logging 또는 출력을 예쁘게 하기 위해서 사용(전송할 때는 indent가 없어도 됨)

### Custom "toJSON"
`toString`을 구현해서 객체가 `String`으로 변환되는 것을 조절하는 것처럼,  
`toJSON`을 구현해서 객체가 JSON으로 변환되는 것을 조절함(`toJSON`이 존재하면 `JSON.stringify`가 자동적으로 `toJSON`을 호출함)

#### Example
```javascript
let room = {
  number: 23,
  toJSON() {
    return this.number;
  }
};

let meetup = {
  title: "Conference",
  date: new Date(Date.UTC(2017, 0, 1)),
  room
};

alert( JSON.stringify(meetup) );
/*
  {
    "title":"Conference",
    "date":"2017-01-01T00:00:00.000Z",  // (1)
    "room": 23              // (2)
  }
*/
```
- (1) `Date` 객체는 날짜를 string으로 반환하는 built-in `toJSON` 메소드가 존재함
- (2) object `room`은 `toJSON` 메소드가 구현되어 있으므로 `meetup`이 `stringify`될 때도 property `room`의 value가 `23`으로 설정됨

### JSON.parse
JSON-string을 decode할 때 사용됨:  
```javascript
let value = JSON.parse(str[, reviver]);
```
- `str` : 파싱할 JSON-string
- `reviver` : `(key, value)`를 parameter로 받아서 property의 value를 계산하는 함수 `function(key, value)`
- JSON은 주석을 허용하지 않음!

### Using reviver
```javascript
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

// 1
let meetup = JSON.parse(str);
alert( meetup.date.getDate() ); // Error!

// 2
let meetup = JSON.parse(str, function(key, value) {
  if (key == 'date') return new Date(value);
  return value;
});
alert( meetup.date.getDate() ); // now works!
```
- `date`의 value는 `stringify`에서 이미 `String`으로 바뀜  
	=> `// 1`과 같이 `date`를 다른 property와 같이 처리하면 `Date` type으로 들어가지 않음  
	
	`// 2`와 같이 reviver를 사용해서 `date` property는 `Date` 객체로 선언해야 함
- replacer와 같이 reviver도 nested object에 대해서 잘 작동함

### Summary

|code|description|
|:---|:---|
|`JSON.stringify(value[, replacer[, space]])`|`value`를 JSON으로 변환함<br>`replacer`로 포함할 property 선택<br>`space`로 인덴팅 설정|
|`JSON.parse(str[, reviver])`|`str`을 object로 변환함<br>`reviver`로 `Date`와 같은 객체를 decode함|
|`obj.toJSON()`|`obj`의 JSON으로의 변환 구현(= custom `stringify`)|

- JSON은 plain objects, arrays, strings, numbers, booleans, `null`을 지원함  
	JS-specific values(methods, `undefined`, symbolic properties)는 무시됨
- property에 circular reference가 존재하면 에러남!

### Tasks
- transformer functions(`replacer`, `reviver`)가 호출되면 wrapper object(`('', this)`)도 argument로 들어오는 것에 주의!
	- object가 트리 형태라고 생각하면,  
		`replacer`는 root(object의 wrapper object)부터 argument로 들어옴(= preorder)  
		`reviver`는 leaf부터 argument로 들어옴(= postorder)
	
	e.g.  
	```javascript
	let room = {
	  number: 23
	};

	let meetup = {
	  title: "Conference",
	  occupiedBy: [{name: "John"}, {name: "Alice"}],
	  place: room
	};

	room.occupiedBy = meetup;
	meetup.self = meetup;

	afterstringify=JSON.stringify(meetup, function replacer(key, value) {
	  alert(`${key} and ${value}`);
	  return (key!='' && value===meetup)?undefined:value;
	}, 2);
	/*
	 and [object Object]
	title and Conference
	occupiedBy and [object Object],[object Object]
	0 and [object Object]
	name and John
	1 and [object Object]
	name and Alice
	place and [object Object]
	number and 23
	occupiedBy and [object Object]
	self and [object Object]
	*/

	alert(JSON.parse(afterstringify, function reviver(key, value) {
	  alert(`${key} and ${value}`);
	  return value;
	}));
	/*
	title and Conference
	name and John
	0 and [object Object]
	name and Alice
	1 and [object Object]
	occupiedBy and [object Object],[object Object]
	number and 23
	place and [object Object]
	 and [object Object]
	*/
	```


# Advanced working with functions
## Recursion and stack
### Two ways of thinking
- Iterative
- Recursive

> ※ JS는 maximal recursion depth가 대부분 `100000` 미만으로 제한되어 있음  
> tail call optimization을 사용해서 속도를 향상시킬 수 있음(safari만 지원하고 나머지는 지원하지 않음)

#### Tail call optimization
tail call을 최적화하는 것  
tail recursion을 잘 설계해야 함!
- `return`에서 스택에 메모리를 쓰는 연산자를 사용하면 안됨  
	ternary operator `?`는 스택 메모리를 사용하지 않는 연산자임

#### Example
```javascript
// 1
let facto = (x, acc = 1) => {
  return (x <= 1 ? acc : facto(x - 1, x * acc));
};

// 2
let facto = x => {
  return (x <=1 ? 1 : x * facto(x-1));
};
```
- `// 1`은 `return`에 메모리를 사용하는 연산자가 존재하지 않아서 tail recursion이 실행되고, 최적화될 경우 스택이 쌓이지 않을 수도 있음  
	`// 2`는 `*`를 사용해서 메모리를 사용하기 때문에 스택이 계속 쌓임(일반적인 재귀)

### The execution context and stack
실행되고 있는 함수의 프로세스에 관한 정보는 *execution context*에 저장됨  
Execution context
- 함수의 실행에 관한 detail을 포함하는 내부 자료 구조임
	- control flow가 어디 있는지, 현재 변수, `this`의 정보 등

하나의 함수 호출은 하나의 execution context를 가짐  
함수가 중첩 호출을 가지면 다음과 같이 작동함:
1. 현재 함수가 멈춤
2. 현재 함수와 관련된 execution context가 *execution context stack*에 저장됨
3. 중첩된 호출이 실행됨
4. 중첩된 호출이 끝난 후 원래 execution context가 stack에서 회수된 다음 원래 함수가 재개됨

recursion depth는 stack 안의 최대 context의 개수와 같음

n 번 재귀 호출이 일어나는 경우 n 개의 context가 필요하지만, 반복문 기반으로 바꾸면 한 개의 context만 필요함  
=> 메모리가 절약됨

모든 재귀는 반복문으로 옮길 수 있고, 보통 반복문을 사용하는게 더 효과적임  
하지만 재귀가 복잡할 경우 옮겨도 효율성이 높아지지 않는 경우가 존재함

재귀가 더 짧고 직관적으로 읽히기 때문에 성능이 떨어짐에도 불구하고 많이 사용됨

### Recursive traversals
재귀가 잘 사용되는 곳 중 하나가 순회임  
자식이 있을 경우 재귀를 사용하면 됨

#### Example
```javascript
let company = { // the same object, compressed for brevity
  sales: [{name: 'John', salary: 1000}, {name: 'Alice', salary: 1600 }],
  development: {
    sites: [{name: 'Peter', salary: 2000}, {name: 'Alex', salary: 1800 }],
    internals: [{name: 'Jack', salary: 1300}]
  }
};

// The function to do the job
function sumSalaries(department) {
  if (Array.isArray(department)) { // case (1)
    return department.reduce((prev, current) => prev + current.salary, 0); // sum the array
  } else { // case (2)
    let sum = 0;
    for (let subdep of Object.values(department)) {
      sum += sumSalaries(subdep); // recursively call for subdepartments, sum the results
    }
    return sum;
  }
}

alert(sumSalaries(company)); // 7700
```

### Recursive structures
Recursive structure(재귀 구조)는 자기 자신과 같은 구조를 부분으로 포함하는 구조임  
⇔ 재귀의 정의

#### Linked list
`Array`는 임의의 위치에 원소 삽입, 삭제가 `O(n)`이 걸림  
Linked list는 `O(1)` 만에 수행 가능

JS에서 linked list는 아래와 같이 재귀적으로 구현함:  
```javascript
let list = {
  value: 1,
  next: {
    value: 2,
    next: {
      value: 3,
      next: {
        value: 4,
        next: null
      }
    }
  }
};
```
- 임의의 원소에 대한 접근이 `O(n)`이 걸림
- `prev` property를 추가해서 DLL으로 개선할 수 있음  
	`tail` object를 추가해서 끝에서의 접근을 개선할 수 있음

### Summary
Tail call recursion은 `return`문에 메모리를 사용하는 연산자를 사용하지 않는게 중요함

## Rest parameters and spread syntax
### Rest parameters `...`
함수의 definition에 상관없이 여러 개의 arguments를 사용해서 호출 가능  
=> 필요한 만큼만 사용되고 에러가 나지 않음!  
`...`를 이용하면 나머지 arguments도 버리지 않고 저장 가능:  
```javascipt
function sumAll(...args) {
  let sum = 0;

  for (let arg of args) sum += arg;

  return sum;
}

alert( sumAll(1) ); // 1
alert( sumAll(1, 2) ); // 3
alert( sumAll(1, 2, 3) ); // 6
```
- 항상 마지막에 와야 하고 `...` 뒤에 arguments가 저장될 `Array`의 이름을 적어야 함

### The "arguments" variable
`argumets`는 함수에 존재하는 array-like object임:  
```javascript
function showName() {
  alert( arguments.length );
  alert( arguments[0] );
  alert( arguments[1] );
}

showName("Julius", "Caesar");
// shows: 2, Julius, Caesar

showName("Ilya");
// shows: 1, Ilya, undefined (no second argument)
```
- 모든 arguments를 인덱스를 key로 저장함
- `length` property 존재
- array-like object이면서 iterable이지만, `Array`가 아님  
	=> `Array`의 methods를 사용할 수 없기 때문에 불편함  
	=> 현재는 rest parameter `...`가 더 많이 사용됨

> ※ Arrow functions는 "arguments"가 없음!  
> arrow function에서 `arguments` 객체를 호출하면 바깥의 일반 함수로부터 가져옴  
> ```javascript
> function f() {
>   let showArg = () => alert(arguments[0]);
>   showArg();
> }
>
> f(1); // 1
> ```
> 즉 arrow function은 `this`와 `arguments`를 outer normal function으로부터 가져옴

### Spread syntax
`Array`의 원소들을 `...`를 지원하는 함수에 arguments로 넣기 위해선, rest parameter와 반대로 `Array`를 값 하나하나로 바꿔야 함  
e.g.  
```javascript
alert( Math.max(3, 5, 1) ); // 5, works

let arr = [3, 5, 1];
alert( Math.max(arr) ); // NaN, doesn't work
```
- `arr[0], arr[1], ...`과 같이 인덱스를 이용하면 함수를 호출할 때 일일히 쳐야 함

spread syntax `...`을 사용해서 iterable object를 나열할 수 있음:  
```javascript
let arr = [3, 5, 1];
let arr2 = [8, 9, 15];

let merged = [0, ...arr, 2, ...arr2];
alert(merged); // 0,3,5,1,2,8,9,15
alert(Math.max(10, ...arr, ...arr2)); // 15

// (*)
let str = "Hello";
alert( [...str] ); // H,e,l,l,o
```
- 다른 인자들과 혼합해서 사용 가능
- iterable만 적용 가능
- `(*)`는 iterable을 `Array`로 바꾸는 것으로, `Array.from(obj)` 메소드를 사용할 수도 있음
	- `Array.from(obj)`는 array-like도 지원하기 때문에 `Object`를 `Array`로 바꾸는 작업은 이 메소드를 사용하는게 좋음

### Copy an array/object
`Object.assign(dest[, src1, src2, src3...])`를 사용해서 `Array`나 `Object`를 복사할 수 있지만, spread syntax로도 할 수 있음:  
```javascript
let arr = [1, 2, 3];
let arrCopy = [...arr];

alert(JSON.stringify(arr) === JSON.stringify(arrCopy)); // true
alert(arr === arrCopy); // false (not same reference)

let obj = { a: 1, b: 2, c: 3, d: {name: 'another'} };
let objCopy = { ...obj };
objCopy.d.name='dother';

alert(obj.d.name); // dother
alert(objCopy.d.name); // dother
alert(JSON.stringify(obj) == JSON.stringify(objCopy)); // true
```
- `JSON.stringify`로 객체를 비교할 수 있음!
- `Object.assign`과 마찬가지로 shallow copy되기 때문에 조심해야 함!

> ※ `Object.assign([], src...)`, `Object.assign({}, src...)` 둘 다 `src`의 properties를 `dest`로 추가하는 것임  
> `Array`도 `Object`에 속함(build-in object 중에 하나임)!

### Summary
`...`는 rest parameter, spread syntax로 사용됨
- L-value로 사용되면 rest parameter로 사용된 것임
- R-value로 사용되면 spread syntax로 사용된 것임

함수 안에서 `arguments`로도 인자들에 접근할 수 있지만, `Array` type이 아니기 때문에 잘 쓰이지 않음

## Variable scope, closure
JS는 function-oriented language로, 어디서든 함수를 만들고 호출할 수 있음  
만약 함수가 생성된 다음 전역변수의 값이 바뀌면? - 호출 시의 값 이용  
함수가 argument로 전달된 다음 실행된다면 외부 변수에 접근할 수 있나? - 호출 시의 위치 이용

> ※ `let/const` 변수들을 다룸  
> `var`은 `let/const`로 대체되었기 때문에 여기선 다루지 않음

### Code blocks
변수가 code block `{...}` 안에서 선언되었다면, 그 안에서만 사용 가능함:  
```javascript
{
  // show message
  let message = "Hello";
  alert(message);
}

{
  // show another message
  let message = "Goodbye";
  alert(message);
}
```
- 같은 블록 안에서 이미 선언된 변수를 `let`으로 다시 선언하는 경우 에러가 남
- `for(...){...}`은 `()`안의 변수도 `{}` 안에서 사용 가능

### Nested functions
JS에서 nested fucntion은 return될 수 있음  
=> 어디서 사용되든 선언된 곳에서의 outer variable에 대해 접근 가능:  
```javascript
function makeCounter() {
  let count = 0;
  alert(count);
  return function() {
    return count++;
  };
}

let counter = makeCounter(); // 0

alert(counter()); // 0
alert(counter()); // 1
alert(counter()); // 2

makeCounter(); // 0
alert(counter()); // 3
```
- `counter`를 여러 개 만들면 각각 독립적인가?  
	=> 독립적임

### Lexical Environment
#### Step 1. Variables
JS에서 모든 실행중인 함수, code block `{...}`, script 전체는 내부에 숨겨진 object인 *Lexical Environment*를 가짐  
Lexical Environment는 두 부분으로 나뉨:
1. *Environment Record*(환경 레코드) : 모든 local variables를 properties로 저장하는 object
2. A reference to the *outer Lexical Environment* : 바깥의 코드와 관련됨

**Variable** : property of **Environment Record**  
변수를 사용하거나 바꾸는 것은 환경 레코드의 property를 사용하거나 바꾸는 것을 의미함

전체 script와 관련된 Lexical Environment를 *global* Lexical Environment라고 함  
global Lexical Environment는 outer reference가 없음!

script가 실행되면 문장이 실행되기 전에 Lexical Environment가 먼저 준비됨  
이때 Environment Record에는 변수들이 미리 등록되어 있지만, 초기화되지 않은 상태임

|![js-lexical-environment1](https://github.com/siriyaoff/MDN-note/blob/master/images/js-lexical-environment1.PNG?raw=true)|
|:---:|
|javascript.info 참고|

- 직사각형이 Environment Record, 화살표가 outer reference를 뜻함
	- global Lexical Environment는 outer reference가 `null`로 향함
- `let` 이전까지 변수가 초기화되지 않은 상태였다가 `let`으로 선언된 뒤에는 `undefined`가 들어감

> ※ Lexical Environment는 specification object로, 이론적으로만(language specification 안에서) 존재함  
> 따라서 이 객체에 접근하거나 수정할 수 없음  
> JS의 엔진들은 specification을 준수하면서 고유한 방법으로 Lexical Environment를 최적화함(사용하지 않는 변수를 버려서 메모리를 절약하는 등)

#### Step 2. Function Declarations
함수도 변수와 같이 하나의 값이지만, function declaration으로 선언된 함수들은 Lexical Environment가 생성되는 동시에 초기화됨(`<uninitialized>`가 들어가는게 아니라 `function`이 들어감)  
=> 함수의 정의 위에서도 함수 호출이 가능함  
cf. `let`으로 선언되는 변수들은 선언문이 실행되기 전까지 사용할 수 없음

Function expression은 이에 해당하지 않음에 주의!

#### Step 3. Inner and outer Lexical Environment
함수가 호출되면 새로운 Lexical Environment가 자동으로 생성됨  
=> 지역 변수와 파라미터를 저장하고, 함수를 호출한 Lexical Environment가 (outer) reference로 설정됨

코드에서 변수에 접근할 때, **inner Lexical Environment를 먼저 살피고 점점 outer로 나가면서 조사함**  
=> 끝에는 global Lexical Environment를 조사함

만약 변수가 어디에도 없다면 strict mode에서는 에러가 발생함  
(non-strict에서는 존재하지 않는 변수로의 대입 연산이 새로운 global variable을 생성함, 오래된 코드와의 호환을 위해)

#### Step 4. Returning a function
모든 **함수**들은 `[[Environment]]`라는 숨겨진 property가 존재함
- 함수가 만들어진 Lexical Environment으로의 reference가 저장됨
- 함수가 생성될 때 한 번 저장되고 변하지 않음

```javascript
function makeCounter() {
  let count = 0;
  
  return function() { // (*)
    return count++;
  };
}

let counter = makeCounter();

alert( counter() ); // 0
alert( counter() ); // 1
alert( counter() ); // 2
```
- `counter`의 `[[Environment]]`는 `let counter = makeCounter();`가 실행될 때 호출된 `makeCounter()`의 Lexical Environment으로의 reference임  
- outer reference는 항상 `[[Environment]]`에 저장된 reference임!!  
	=> `counter()`가 호출될 때마다 생기는 Lexical Environment의 outer reference는 global이 아니라 `counter.[[Environment]]`에 저장된 reference임!  
	
	이 예제에서는 `makeCounter()`의 Lexical Environment이기 때문에 그 안의 변수 `count`를 공유함!

> ※ Closure  
> - outer Lexical Environment의 위치를 기억하고 접근할 수 있는 함수를 뜻함
> - 프로그래밍에서 전반적으로 사용되는 용어
> - 일부 언어에서는 이 자체가 불가능하지만, JS에서는 `new Function` syntax를 제외하면 모든 함수들은 기본적으로 closure임!
> 	- `[[Environment]]` property가 자동으로 생성되기 때문

### Garbage collection
보통 Lexical Environment는 함수 호출이 끝난 다음 모든 변수들과 함께 지워짐  
∵ 다른 JS의 객체와 같이, reachable 할 때만 메모리에 보존되기 때문

하지만, 함수의 종료 후에도 reachable한 nested function이 존재한다면 nested function의 `[[Environment]]` property에 원래 함수의 Lexical Environment로의 레퍼런스가 저장됨  
=> 함수가 끝난 후에도 함수의 Lexical Environment가 reachable하기 때문에 살아있게 됨!

#### Example
```javascript
function f() {
  let value = 123;

  return function() {
    alert(value);
  }
}

let g = f(); // (1)
```
- `g.[[Environment]]`는 `// (1)`에서 호출된 `f()`의 Lexical Environment의 reference가 저장됨
- Lexical Environment도 unreachable하게 되었을 때 지워짐  
	e.g. `g`에 `null`을 저장해서 reference를 없앴을 경우

#### Real-life optimizations
이론적으로, 함수가 살아있는 동안, 모든 외부의 변수들도 유지됨  
실제로는 JS 엔진들이 코드를 읽어서 사용되지 않는 외부 변수들은 지워버리는 최적화를 실행함  
=> 최적화에 의해 제거된 변수들은 디버깅 모드에서도 사용하지 못한다는 부작용이 존재함(Chrome, Edge, Opera 등의 V8 엔진에서)

```javascript
let value = "Surprise!";

function f() {
  let value = "the closest value";

  function g() {
    debugger; // in console: type alert(value); Surprise!
  }

  return g;
}

let g = f(); // (1)
g();
```
- 외부 변수 `g`가 실행되면서 만들어진 `f()`의 Lexical Environment는 `// (1)`이 끝난 후에도 유지됨  
	(∵ `g`에 들어가는 `g()`의 outer reference가 참조하고 있기 때문)  
	하지만, `f()`의 변수 `value`는 함수 `g()`에서 사용되지 않기 때문에 최적화에 의해 삭제됨  
	
	따라서 마지막에 `g();`를 실행해서 나온 디버깅 모드에서 `alert(value)`를 실행하면 `f()`의 Lexical Environment에 저장된 `value`인 `"the closest value"`가 출력되지 않고 `"Surprise!"`가 출력됨!

> ※ V8 엔진에서만 나타나는 현상임!

### Summary
함수, code block, script 전체는 Lexical Environment를 가짐
- 내부에 숨겨진 object로, 두 부분으로 나뉨:
	- Environment Record : local variables, function들을 property로 저장
		- 변수들은 선언되어 있지만, 초기화되지 않은 상태
		- function declaration으로 정의된 함수들은 초기화된 상태
	- A reference to the outer Lexical Environment

함수가 호출될 때 그 함수의 Lexical Environment가 생성됨(code block도 마찬가지)

모든 함수들의 Lexical Environment들은 `[[Environment]]`라는 숨겨진 property를 가짐
- 함수가 만들어진, 외부 Lexical Environment로의 reference가 저장됨
- 함수가 생성될 때(외부 Lexical Environment의 Environment record에 등록될 때) 한 번 저장되고 변하지 않음
- 이후 그 함수가 호출될 때마다 Lexical Environment의 outer reference는 `[[Environment]]`에 저장된 reference가 들어감
	- JS의 대부분의(`new Function` syntax 제외) 함수들이 closure인 이유임

Lexical Environment는 다른 객체들과 마찬가지로 reachable 하지 않으면 메모리에서 제거됨  
reachable하더라도 JS 엔진의 최적화에 의해, 살아있지만 내부에서도 사용되지 않는 외부 변수가 존재한다면 지워질 수 있음(V8 엔진의 최적화 방법임)

### Tasks
```javascript
function makeWorker() {
  let name = "Pete";

  return function() {
    alert(name);
  };
}

let name = "John";

// create a function
let work = makeWorker();

// call it
work(); // what will it show?
```
- `work`의 outer reference는 `makeWorker()`의 Lexical Environment로의 reference기 때문에 `"Pete"`를 참조함

```javascript
let x = 1;

function func() {
  alert(x); // (1)
  let x = 2;
}

func();
```
- "uninitialized"와 "non-existing"의 차이임!
	- `(1)`을 실행하는 시점에서 `func()`의 Lexical Environment에 `x`가 `<uninitialized>` 상태로 존재하기 때문에 사용하려 하면 에러가 발생함!
	- 뒤의 `let x=2;`를 지우면 `func()`의 Lexical Environment에는 `x`가 존재하지 않기 때문에 outer reference인 global으로 가서 `x`(= `1`)을 참조함

"ready to use" filters 만들기:  
```javascript
function inBetween(a, b) {
  return function(v) {
    if(a<=v && v<= b) return true;
    else return false;
  };
}

function inArray(arr) {
  return function(v) {
    return arr.includes(v);
  };
}

let arr = [1, 2, 3, 4, 5, 6, 7];

alert( arr.filter(inBetween(3, 6)) ); // 3,4,5,6

alert( arr.filter(inArray([1, 2, 10])) ); // 1,2
```

Army of functions:  
```javascript
function makeArmy() {
  let shooters = [];

  let i = 0;
  while (i < 10) {
    let shooter = function() { // create a shooter function,
      alert( i ); // that should show its number
    };
    shooters.push(shooter); // and add it to the array
    i++;
  }

  // ...and return the array of shooters
  return shooters;
}

let army = makeArmy();

// all shooters show 10 instead of their numbers 0, 1, 2, 3...
army[0](); // 10 from the shooter number 0
army[1](); // 10 from the shooter number 1
army[2](); // 10 ...and so on.
```
- `army`의 원소들은 모두 `makeArmy()`의 Lexical Environment를 outer reference로 가지기 때문에 실행이 끝나 `i`에 `10`이 들어간 상태로 `i`를 출력해서 같은 숫자가 나옴
- `while` 안에서 local variable `j`를 추가해서 해결 가능
- 반복문을 `for`로 바꾸기만 해도 해결됨:  
	```javascript
	function makeArmy() {
	  let shooters = [];

	  for(let i=0;i<10;i++) {
		let shooter = function() {
		  alert( i );
		};
		shooters.push(shooter);
	  }

	  return shooters;
	}
	```
	- `while`의 loop control variable인 `i`는 `makeArmy()`의 Lexical Environment에 속해있지만, `for`의 loop control variable은 `for` 안에 들어가기 때문에 `for`의 code block의 Lexical Environment 안에 `i`가 저장됨!!

## The old "var"
`var` declaration은 `let`과 비슷함  
대부분의 경우 `var`, `let`을 서로 바꿔서 사용 가능

하지만 `var`은 내부적으로 매우 다르게 동작함

### "var" has no block scope
```javascript
if (true) {
  var test = true; // use "var" instead of "let"
}

alert(test); // true, the variable lives after if
```

function-level로만 scope가 존재함:  
```javascript
function sayHi() {
  if (true) {
    var phrase = "Hello";
  }

  alert(phrase); // works
}

sayHi();
alert(phrase); // ReferenceError: phrase is not defined
```
- 오래 전에는 code block이 Lexical Environment를 생성하지 않았기 때문  
	`var` 자체가 이런 환경에서 사용되었기 때문에 code block은 상관없이 선언됨

### "var" tolerates redeclarations
`var`로 정의된 변수는 `var`로 재정의해도 에러가 나지 않음:  
```javascript
var user = "Pete";
var user = "John";

alert(user); // John
```
- 값은 정상적으로 대입됨

### "var" variables can be declared below their use
`var`을 사용하는 정의는 함수(global일 경우 script가) 시작될 때 처리됨  
=> `var`은 definition의 위치에 상관없이 호출할 수 있음:  
```javascript
function sayHi() {
  phrase = "Hello";

  alert(phrase);

  var phrase;
}
sayHi();

/*------------------------------*/

function sayHi() {
  phrase = "Hello"; // (*)

  if (false) {
    var phrase;
  }

  alert(phrase);
}
sayHi();
```
- 두 번째 예제도 정상적으로 실행됨  
	∵ code block은 무시되고 함수가 호출될 때 `phrase`의 선언이 이루어지기 때문
- *Hoisting*이라고도 함
	declaration은 호이스팅이 되지만, assignment는 그렇지 않음!  
	```javascript
	function sayHi() {
	  alert(phrase);
	  var phrase = "Hello";
	}
	
	sayHi();
	```
	- 선언은 되었지만, 값이 없는 상태이기 때문에 `undefined`가 출력됨

> ※ definition == declaration + assignment라고 생각하면 됨

### IIFE
Immediately-invoked function expressions : block-level visibility가 지원되지 않던 옛날에 이를 구현하기 위해서 만듦:  
```javascript
(function() {
  alert("Parentheses around the function");
})();

(function() {
  alert("Parentheses around the whole thing");
}());

!function() {
  alert("Bitwise NOT operator starts the expression");
}();

+function() {
  alert("Unary plus starts the expression");
}();
```
- 함수 레벨의 scope는 존재했기 때문에 `{...}` 대신 사용한 것임
	- JS는 function이라는 코드를 읽으면 function declaration의 시작이라고 인식하기 때문에 앞에 `(`나 `!`, `+` 등을 붙여서 function expression이라고 인식시킴  
		∵ function declaration으로 정의할 경우 function name이 반드시 필요하고, 정의하면서 바로 호출할 수 없기 때문
- 현재는 사용하지 않는 legacy code임!!

### Summary
`var`의 특징:
1. block scope가 존재하지 않고, 함수, global scope만 존재
2. `var`의 declaration은 함수나 script가 시작할 때 처리됨

block scope가 존재하지 않아서 현재는 잘 사용하지 않음

## Global object
global object를 사용하면 어디서든 사용 가능한 변수와 함수를 만들 수 있음  
global object는 보통 언어에 내장되어 있음  
브라우저에서는 `window`, Node.js에서는 `global` 등으로 명명됨  
최근에는 `globalThis`가 global object의 표준화된 이름으로 추가됨(대부분의 browser에서 지원됨)  
이 article에서는 `window`를 사용함

```javascript
alert("Hello");
// is the same as
window.alert("Hello");

var gVar = 5;
alert(window.gVar); // 5
```
- browser 환경에서, `var`을 사용해서 정의된 전역 함수와 변수들은 global object의 property가 됨
	- function declaration으로 global scope에서 정의된 함수도 동일하게 global object의 property가 됨
	- 모듈을 사용하는 최신의 JS에서는 일어나지 않고, 호환성을 위해서 존재하는 기능임

global available하게 만드려면 아래와 같이 global object의 property가 되도록 추가하면 됨:  
```javascript
window.currentUser = {
  name: "John"
};

alert(currentUser.name);  // John
alert(window.currentUser.name); // John
```
- 되도록 사용하지 않는게 좋음!
- 사용하게 될 경우 `window`를 붙여서 global object의 property임을 확실히 명시하는게 좋음

### Using for polyfills
최신 기능을 지원하는지 테스트하기 위해 global object를 사용할 수 있음:  
```javascript
if (!window.Promise) {
  window.Promise = ... 
}
```
- 지원하지 않을 경우 직접 polyfills를 추가할 수 있음

## Function object, NFE
JS에서 함수는 `Object` 타입으로 취급됨
- 호출, property 추가/제거, 레퍼런스로 만들어 전달 등이 가능함
- built-in properties가 존재함

### The "name" property
`name` property는 함수의 이름을 저장함:  
```javascript
let sayHi = function() {
  alert("Hi");
};

alert(sayHi.name); // sayHi

/*--------------------------------------*/

function f(sayHi = function() {}) {
  alert(sayHi.name); // sayHi
}

f();

/*--------------------------------------*/

let arr = [function() {}];

alert( arr[0].name ); // <empty string>
```
- `name` property는 specification에서 "contextual name"이라고 불림
	- 함수의 이름이 직접 제공되지 않아도, context에서 이름을 가져옴
	- 맨 마지막 예시처럼 이름을 추론할 수 없는 상황도 존재하지만, 대부분의 경우 함수는 이름을 가짐

### The "length" property
`length` property는 함수의 parameter의 개수를 리턴함:  
```javascript
function f1(a) {}
function f2(a, b) {}
function many(a, b, ...more) {}

alert(f1.length); // 1
alert(f2.length); // 2
alert(many.length); // 2
```
- rest parameter는 `length`의 개수에 포함되지 않음

아래 예제와 같이 호출할 함수의 파라미터 개수에 따라서 알맞는 함수를 호출할 때(= type introspection) 사용 가능함:  
```javascript
function ask(question, ...handlers) {
  let isYes = confirm(question);

  for(let handler of handlers) {
    if (handler.length == 0) {
      if (isYes) handler();
    } else {
      handler(isYes);
    }
  }

}

// for positive answer, both handlers are called
// for negative answer, only the second one
ask("Question?", () => alert('You said yes'), result => alert(result));
```
- polymorphism의 예시임
	- arguments를 그들의 type(이 예시의 경우, `length`)에 따라서 다르게 처리하는 것

### Custom properties
custom property도 추가 가능:  
```javascript
function sayHi() {
  alert("Hi");

  sayHi.counter++;
}
sayHi.counter = 0;

sayHi();
sayHi();
alert( `Called ${sayHi.counter} times` ); // Called 2 times
sayHi.counter = 10;
alert( `Called ${sayHi.counter} times` ); // Called 10 times
```
- function property와 variable은 연관이 없음
	- `sayHi.counter = 0`은 local variable이 아님
- function property `counter`는 함수 바깥에 저장됨  
	안에 저장하면 호출될 때마다 초기화되기 때문
- closure는 function property로 대체 가능함

Closure을 이용한 버전:  
```javascript
function makeCounter() {
  function counter() {
    return counter.count++;
  };

  counter.count = 0;

  return counter;
}

let counter = makeCounter();
alert( counter() ); // 0
alert( counter() ); // 1
counter.count = 10;
alert( counter() ); // 10
```
- `makeCounter()`의 Lexical Environment가 변수 `counter`에 의해 유지되면서 `count` property가 증가함
- `count`가 완전히 외부가 아닌 중간의 `makeCounter()`의 Lexical Environment에 저장됨  
	=> 외부에서 `counter.count`를 접근하지 못하지만, 이 경우에는 `makeCounter()`가 `counter()`를 반환하기 때문에 외부의 변수 `counter`에 `counter()`가 저장되고 이 변수로 `counter()`의 property를 접근 가능!

`count`에 대한 외부의 접근을 제한한 버전:  
```javascript
function makeCounter() {

  function counter() {
    return count++;
  };

  count = 0;

  return counter;
}

let counter = makeCounter();

alert( counter() ); // 0
alert( counter() ); // 1
alert( counter() ); // 2
```
- 외부에서는 `count`에 접근할 수 없음  
	오직 `counter()`으로만 접근 가능  
	cf. function property를 이용하면 외부에서도 함수에 대한 reference만 있으면 접근 가능  
	
	=> 목적에 따라 구현 방법을 선택하면 됨

### Named Function Expression
```javascript
let sayHi = function func(who) {
  if (who) {
    alert(`Hello, ${who}`);
  } else {
    func("Guest"); // use func to re-call itself
  }
};

sayHi(); // Hello, Guest

func(); // Error, func is not defined (not visible outside of the function)
```
- function expression에 이름을 추가한 것임
	- 이름을 추가한다고 function declaration이 되진 않음
	- 정상적으로 호출 가능함
- NFE의 기능:
	- 함수가 내부에서 자신을 호출 가능하게 만듦
	- 함수 바깥에서는 호출할 수 없음
- 함수의 이름으로 호출하는 경우:  
	```javascript
	let sayHi = function(who) {
	  if (who) {
		alert(`Hello, ${who}`);
	  } else {
		sayHi("Guest"); // Error: sayHi is not a function
	  }
	};

	let welcome = sayHi;
	welcome(); // Hello, Guest
	
	sayHi = null;
	welcome(); // Error, the nested sayHi call doesn't work any more!
	```
	- 외부에서 sayHi가 수정될 경우 에러가 발생할 수 있음!  
		=> NFE를 사용해서 해결

> ※ function declaration에서 함수 이름을 사용하는건 recursion  
> NFE 같이 internal name이 필요하지 않음(확실한 함수 이름이 존재함)

### Summary
- 함수는 `name`, `length`(parameter의 개수) 등의 built-in property를 가짐
- custom property를 추가할 수도 있음
	- closure으로 대체 가능  
		closure으로 구현하는 경우 외부에서의 접근 불가
- function expression에 이름을 추가할 수 있음(NFE)  
	=> function expression으로 선언되는 함수의 property 호출, 재귀 등을 지원 가능  
	
	lodash library에서는 `_` 함수 안에 helper function들을 선언해서 global space의 낭비를 줄이고 이름 충돌의 가능성을 줄임

### Tasks
`sum` 함수를 아래 예시와 같이 구현하기:  
```
alert( sum(1)(2) ); // 3
alert( sum(5)(-1)(2) ); // 6
alert( sum(6)(-1)(-2)(-3) ); // 0
alert( sum(0)(1)(2)(3)(4)(5) ); // 15

// (1) using closure + function property
function sum(val) {
  function f(cur) {
    f.cursum+=cur;
    return f;
  }
  
  f.cursum=val;
  f.toString = function(){
    return f.cursum;
  };
  return f;
}

// (2) using closure
function sum(val) {
  let cursum = val;
  function f(cur) {
    cursum+=cur;
    return f;
  }
  
  f.toString = function(){
    return cursum;
  };
  
  return f;
}
```
- function property는 항상 함수 안이나 함수가 선언된 영역, 두 곳 모두에서 선언 가능
	- closure로 사용된 함수도 function property를 선언해서 사용 가능함
		- closure 안에서 선언하면 호출될 때마다 새로 선언됨  
			outer Lexical Environment에서 선언되면 초기화되지 않음
		- 아예 밖에서는 closure의 property 호출 불가
- `f`를 재귀로 만들기 위해선 parameter `acc`를 넣어야 하기 때문에 예시와 맞지 않음
- `f`가 더 이상 호출되지 않을 때 출력을 위해 `f`의 `toString` method를 정의해야 함!
- `(1)`의 `f.cursum`은 `f`의 reference가 있으면 외부에서도 수정할 수 있지만, `(2)`의 `cursum`은 외부에서 접근 불가능

> ※ closure에서 자신을 리턴하는 것은 재귀가 아님!!  
> 위의 코드에서 `f()` 안에서 `return f`는 재귀가 아님  
> cf. `return f()`였으면 재귀지만, 호출하지 않았으므로 그냥 함수를 반환하는 것 뿐임!

## The "new Function" syntax
`new Function`으로도 함수를 생성할 수 있음  
잘 쓰이지 않지만, 이 방법으로만 해결할 수 있는 상황이 존재함

### Syntax
```javascript
let func = new Function ([arg1, arg2, ...argN], functionBody);

new Function('a', 'b', 'return a + b'); // basic syntax
new Function('a,b', 'return a + b'); // comma-separated
new Function('a , b', 'return a + b'); // comma-separated with spaces

/*-------------example--------------*/

let sum = new Function('a', 'b', 'return a + b');
alert( sum(1, 2) ); // 3

let sayHi = new Function('alert("Hello")');
sayHi(); // Hello
```
- `functionBody`에 있는 string 그대로 함수를 구현함  
	=> run time에 함수를 정의할 수 있음  
	e.g. 서버로부터 함수 코드를 받는 등의 상황에서 사용

### Closure
`new Function`으로 생성된 함수들은 `[[Environment]]`가 global Lexical Environment로 설정됨  
=> closure으로 사용되어도 outer Lexical Environment에 존재하는 properties를 사용할 수 없음:  
```javascript
function getFunc() {
  let value = "test";
  let func = new Function('alert(value)');

  return func;
}

getFunc()(); // error: value is not defined
```
- 구조적으로 더 안전함  
	∵ `new Function`으로 생성되는 함수들은 프로그램이 실행 중에 정의되는데, 이 때는 이미 minifier에 의해 변수들 이름이 내부적으로 단축된 이후이기 때문에 변수명을 알 수 없음  
	
	=> `new Function`은 외부 변수에 접근하면 안됨  
	`[arg1, arg2, ...argN]`과만 상호작용 해야 함

### Summary

|code|description|
|:---|:---|
|`let func = new Function ([arg1, arg2, ...argN], functionBody);`|`new Function`을 이용한 함수 정의|

- `new Function`들은 `[[Environment]]`가 global Lexical Environment로 설정됨  
	=> 외부 변수들을 건드릴 수 없음  
	
	global variables는 사용 가능함

## Scheduling: setTimeout and setInterval
함수를 일정 시간 이후에 실행하는 것을 "scheduling a call"이라고 함  
두 가지 method로 구현할 수 있음:
- `setTimeout` : 일정 시간 후에 함수를 실행시킬 수 있음
- `setInterval` : `setTimeout`을 반복하는 것과 같음(일정 시간 후에 함수 실행을 반복)

JS specification에 명시되어 있지 않지만, 대부분의 browser와 Node.js 등의 환경에서 지원됨

### setTimeout
```javascript
let timerId = setTimeout(func|code[, delay[, arg1, arg2, ...]]);

/*-------------example--------------*/

function sayHi(phrase, who) {
  alert( phrase + ', ' + who );
}
setTimeout(sayHi, 1000, "Hello", "John"); // Hello, John

setTimeout(() => alert('Hello'), 1000);
```
- `func|code` : 실행시킬 함수나 코드
	- 코드도 허용은 되지만 보안상 사용하지 않는게 좋음
- `delay` : 실행시키기 전에 delay, `ms` 단위
	- default : 0ms
- `arg1`, `arg2`... : 함수에 필요한 arguments
- 타이머를 식별하기 위해 만들어진 ID(숫자)가 반환됨  
	=> `clearTimeout` method로 실행을 취소시킬 수 있음:  
	```javascript
	let timerId = setTimeout(...);
	clearTimeout(timerId);
	```
	
	cf. Node.js에서는 `timeId`가 timer object를 반환함

### setInterval
```javascript
let timerId = seInterval(func|code[, delay[, arg1, arg2, ...]]);

/*-------------example--------------*/

let timerId = setInterval(() => alert('tick'), 2000);

setTimeout(() => { clearInterval(timerId); alert('stop'); }, 5000);
```
- `setTimeout`과 문법, 사용 방법이 같음
- `setTimeout`은 한 번만 실행하지만, `setInterval`은 interval을 계속 반복함
- `clearInterval(timerID)`로 취소시킬 수 있음
- 위 예시에서는 2초마다 `alert`를 반복하지만, 5초가 지나면 중지하도록 구현됨  
	Scheduling과 관련된 method들은 function declaration처럼 미리 초기화되고 한꺼번에 실행되는 듯

> ※ `alert`가 실행되고 있을 때도 timer의 시간은 계속 계산됨  
> => `setInterval(() => alert('tick'), 2000);`을 실행하면 사용자가 확인을 누르는 시간도 `2000ms`에 포함되기 때문에 사용자가 느끼는 `alert`가 반복되는 시간은 더 짧음!

### Nested setTimeout
반복적으로 무언가를 실행하는 것은 두 가지 방법으로 구현 가능함  
`setInterval`을 사용하거나 `setTimeout`을 중첩하는 것임:  
```javascript
let timerId = setInterval(() => alert('tick'), 1000);

let timerId = setTimeout(function tick() {
  alert('tick');
  timerId = setTimeout(tick, 1000);
}, 1000);
```
- `setTimeout`을 중첩해서 사용하는 것이 더 유용한 코드를 만들 수 있음  
	- interval을 늘려야 할 경우 안에서 수정 가능함  
	- 정확하게 `delay` 만큼 지연되는게 보장됨
		- `setInterval`은 함수를 실행시킨 시점부터 시간을 재지만, nested `setTimeout`은 함수가 끝난 시점부터 시간을 재기 때문  
			(확실하지 않음)

> ※ `setInterval`, `setTimeout`의 Garbage collection  
> `clearInterval`, `clearTimeout`이 호출되기 전까지 `func`의 reference도 유지되기 때문에 garbage collect되지 않음  
> outer Lexical Environment를 참조하는 함수가 존재하면 `setInterval`이 실행되는 동안에는 그 Lexical Environment도 garbage collect되지 않기 때문에 주의해야 함  
> 사용이 끝나면 `setInterval`으로 취소하는게 메모리 부하를 막음

### Zero delay setTimeout
`setTimeout(func,0)`이나 `setTimeout(func)`로 `delay` 없이 사용하면 현재 script가 끝난 직후 `func`을 실행하게 됨  
browser에서는 zero-delay timeout을 활용해서 event loop를 설정 가능

#### Example
```javascript
setTimeout(() => alert("World"));
alert("Hello");
alert("Hello");
```
- `"Hello"`가 두 번 출력된 다음 `"World"`가 출력됨

> ※ zero delay가 실제로 지연 시간이 없지는 않음  
> HTML5의 경우, timer가 5번 이상 중첩될 경우, 반복되는 구간은 최소 4ms 이상으로 조정됨  
> `setTimeout` 뿐만 아니라 `setInterval`에도 적용됨  
> 지연 없이 구현해놓아도 처음에만 지연 없이 실행되다가 나중에는 지연시간이 생김  
> e.g. `0, 0, 0, 0, 8, 6, 5 ms`  
> 예전에 생긴 specification에 명시되어 있는데, legacy code 중에서 이 조항을 고려해서 구현된게 많음  
> 서버에서는 이런 제한이 없고, 즉각적인 비동기 작업을 구현하는 다른 방법들이 존재함  
> 즉, 이 제한은 browser에 한정됨

### Summary

|code|description|
|:---|:---|
|`setTimeout(func|code[, delay[, arg1, arg2, ...]])`|`delay` ms 만큼 기다린 후에 `func`를 실행시킴<br>현재 timerId를 반환함(숫자)|
|`clearTimeout(timerId)`|`timerId`에 해당하는 타이머를 취소시킴|
|`seInterval(func|code[, delay[, arg1, arg2, ...]])`|`delay` ms 만큼 기다린 후에 `func`를 실행시키는 작업을 반복<br>현재 timerId를 반환함(숫자)|
|`clearInterval(timerId)`|`timerId`에 해당하는 타이머를 취소시킴|

- scheduling method들은 현재 script가 끝난 다음 한꺼번에 실행됨!  
	e.g. 2초마다 출력, 5초에 2초 타이머 취소가 있으면, 출력이 2번 되고 1초 후에 2초의 타이머가 취소됨  
	cf. `Date`의 method(`Date.now()` 등)들은 다른 statements와 같이 순서대로 실행됨(`alert`가 앞에 있으면 확인이 눌러진 다음 실행됨)
- nested `setTimeout`이 `delay` 만큼 지연되는 것이 보장되고 더 유연한 구현이 가능함  
	cf. `setInterval`은 `func`을 실행하는데 소요되는 시간도 timer에 포함됨
- zero-delay scheduling은 browser 환경에서 5번의 호출 이후 지연 시간이 최소 4ms 이상으로 조절됨
- timer의 최소 지연 시간은 300ms ~ 1000ms까지 늘어남(browser나 OS의 설정에 따라 다름)

### Tasks
1초마다 증가하는 숫자 출력:  
```javascript
function printNumbers(from, to) {
  let current = from;
  setTimeout(function go(){
    alert(current);
    if(current<to) setTimeout(go, 1000);
    current++;
  }, 1000);
}

function printNumbers2(from, to) {
  let current = from, tid=setInterval(function() {
    alert(current);
    if(current == to) clearInterval(tid);
    current++;
  }, 1000);
  
}
```
- `clearInterval`도 `function()`의 다른 script가 끝난 다음 비교되기 때문에 이렇게 구현 가능

## Decorators and forwarding, call/apply
JS는 함수를 다루는데 유연함  
함수를 인자로 넘기거나 객체로 사용할 수 있고, *forwarding*, *decorating*도 가능함

### Transparent caching
CPU를 많이 사용하지만, 결과가 stable한(항상 일정한 결과가 나옴) 함수 `slow(x)`가 있다고 가정하자  
이 함수가 자주 호출된다면, 결과를 캐싱하는게 나음  
하지만 `slow()` 안에 캐시를 추가하는 것보다, wrapper function을 추가하는게 더 좋음

#### Example
```javascript
function slow(x) {
  // there can be a heavy CPU-intensive job here
  alert(`Called with ${x}`);
  return x;
}

function cachingDecorator(func) {
  let cache = new Map();

  return function(x) {
    if (cache.has(x)) {    // if there's such key in cache
      return cache.get(x); // read the result from it
    }

    let result = func(x);  // otherwise call func

    cache.set(x, result);  // and cache (remember) the result
    return result;
  };
}

slow = cachingDecorator(slow);

alert( slow(1) ); // slow(1) is cached and the result returned
alert( "Again: " + slow(1) ); // slow(1) result returned from cache

alert( slow(2) ); // slow(2) is cached and the result returned
alert( "Again: " + slow(2) ); // slow(2) result returned from cache
```
- `Map`을 이용해서 caching 가능
- `slow(x)`를 호출하면, `slow()`가 호출되는 대신, `cachingDecorator`에 의해 반환된 caching wrapper가 호출됨  
	=> `cachingDecorator`가 *decorator*임!
	- 다른 함수를 가져와서 그것의 작동을 바꿈(이 예시에서는 caching을 추가)  
		decorator 안에 cache를 만들어서 함수의 code도 더 간단해짐
	- `cachingDecorator(func)` 안의 closure `function(x)`는 `func(x)`의 wrapper라고도 함
	- `slow()`의 기능은 동일하고, caching만 추가됨
- caching decorator를 사용하면 아래와 같은 장점이 있음:
	- `cachingDecorator`는 reusable함 => 어느 함수에든 적용 가능
	- caching logic이 분리되어 `slow()` 자체의 복잡성이 증가하지 않음
	- 필요하면 여러 개의 decorator를 조합할 수 있음

### Using "func.call" for the context
object method는 decorator를 사용하기에 적합하지 않음  
(∵ method 안에서 `this`를 호출하는 부분이 존재하면, decorator로 옮겨졌을 때 `this`가 `undefined`를 반환하기 때문)

#### Example
```javascript
let worker = {
  someMethod() {
    return 1;
  },

  slow(x) {
    // scary CPU-heavy task here
    alert("Called with " + x);
    return x * this.someMethod(); // (*)
  }
};

function cachingDecorator(func) {
  let cache = new Map();
  return function(x) {
    if (cache.has(x)) {
      return cache.get(x);
    }
    let result = func(x); // (**)
    cache.set(x, result);
    return result;
  };
}

alert( worker.slow(1) ); // the original method works

worker.slow = cachingDecorator(worker.slow); // now make it caching

alert( worker.slow(2) ); // Whoops! Error: Cannot read property 'someMethod' of undefined
```
- `(**)`에서 원래 method인 `slow()`를 호출  
	=> `slow()`가 실행되고 `(*)`에서 `this`를 호출  
	=> `undefined`가 반환되어 `undefined.someMethod()`를 호출하기 때문에 에러가 남
- caching decorator가 아닌 다른 wrapper로 옮겨서 호출해도 같은 결과가 나옴:  
	```javascript
	let func = worker.slow;
	func(2);
	```
	∵ `this`는 함수가 실행될 때 값이 계산됨

`Array`의 method들은 `thisArg`를 사용해서 해결 가능하지만, 일반적인 method들은 `thisArg`가 parameter에 없는 경우가 많음  
=> 내장 method인 `func.call([context[, ...args]])`를 사용해서 해결 가능
- `context` : `thisArg`와 같은 역할로, 함수 내 `this`가 가리키는 것을 지정함

#### Example
```javascript
function sayHi() {
  alert(this.name);
}

let user = { name: "John" };

sayHi.call( user ); // John
```
- argument 없이 실행할 수도 있음

위의 decoration에 `func.call(thisArg)`를 사용:  
```javascript
function cachingDecorator(func) {
  let cache = new Map();
  return function(x) {
    if (cache.has(x)) {
      return cache.get(x);
    }
    let result = func.call(this, x); // "this" is passed correctly now
    cache.set(x, result);
    return result;
  };
}
```
- `worker.slow = cachingDecorator(worker.slow);`가 실행될 때 method `worker.slow`가 `func`로 들어감  
	=> `func` 자체가 `worker.slow`라는 method이기 때문에 `func.call(this, x)`를 호출하면 `this`가 점 앞의 객체인 `worker`가 됨

즉, decorator를 사용할 때 decorate할 `func`가 `this`를 사용한다면, `wrapper` 안에서 `func`를 호출할 때 `func.call(this, ...args)`로 호출하면 됨!

### Going multi-argument
argument가 여러 개인 함수도 caching을 시킬 수 있을까?  
argument가 하나일 때는 `(x, res)`를 `Map`에 넣어서 caching을 구현했지만, `Map`이 key로 하나의 값만 저장 가능하기 때문에 인자가 여러 개일 경우 이 방법이 불가능함

가능한 방법들:
1. multi-key가 허용되는 map-like 자료 구조를 구현
2. nested map을 사용  
	e.g. `cache.get(arg1).get(arg2)`
3. hashing 등으로 두 개의 값을 하나로 만듦

세 번째 방법이 주로 사용됨

`func.call()`에 여러 인자를 넣기 위해서 모든 함수에 존재하는 array-like object `arguments`와 spread syntax `...` 이용:  
```javascript
let worker = {
  slow(min, max) {
    alert(`Called with ${min},${max}`);
    return min + max;
  }
};

function cachingDecorator(func, hash) {
  let cache = new Map();
  return function() {
    let key = hash(arguments); // (*)
    if (cache.has(key)) {
      return cache.get(key);
    }

    let result = func.call(this, ...arguments); // (**)

    cache.set(key, result);
    return result;
  };
}

function hash(args) {
  return args[0] + ',' + args[1];
}

worker.slow = cachingDecorator(worker.slow, hash);

alert( worker.slow(3, 5) ); // works
alert( "Again " + worker.slow(3, 5) ); // same (cached)
```
- 이제 `worker.slow`는 임의의 개수의 인자를 넣어도 작동함(`hash`는 수정해야 함)
- `(*)`에서 `hash()`를 사용해서 `key`를 만듦  
	`(**)`에서 `this`와 `...arguments`를 사용해서 `result`를 만들고 cache에 넣음

### func.apply
`func.call([this[, ...arguments]])` 대신 `func.apply(this[, arguments])`를 사용 가능
`func.call`과의 차이점:  
- `func.apply`에서는 array-like `args`만 허용됨  
	cf. `func.call`에서는 argument로 iterable `args`가 `...`로 인해 나열되어서 들어감

=> `Array` 같이 array-like이면서 iterable인 객체의 경우 `apply`와 `func` 두 곳 모두에 들어갈 수 있지만, array-like가 더 최적화가 잘 되어있기 때문에 `apply`에 넣는게 실행 속도가 더 빠름

context(`this`)와 모든 arguments를 같이 다른 함수로 넘기는 것을 *call forwarding*이라고 함:  
```javascript
let wrapper = function() {
  return func.apply(this, arguments);
};
```
- decorator는 closure 안에서 call forwarding을 사용함
	주로 closure와 함께 사용될 듯(single responsibility principle + 보안)
- `wrapper`를 호출해서 `func`를 실행하는 것과 `func`를 호출하는 것은 구분할 수 없음

### Borrowing a method
위의 hashing function은 두 개의 arguments에 대해서만 작동함  
*method borrowing*을 이용해서 이것을 개선할 수 있음:  
```javascript
function hash() {
  alert( [].join.call(arguments) ); // 1,2
}
```
- `arguments`는 iterable이면서 array-like이지만, `Array`가 아니기 때문에 `Array`의 method인 `arr.join()`을 사용할 수 없음  
	=> `func.call()`을 사용해서 method `join`을 빌릴 수 있음!
- `call()`의 `this`에 `arguments`를 넣은 것임  
	`join()`이 `this[0...n]`을 추가하도록 구현되어있기 때문에 가능함
- 이 경우에는 `Array.from()`을 사용해도 될 듯

### Decorators and function properties
original function이 function property를 가지고 있을 경우 decorator로 함수를 바꾸면 function property는 지원되지 않음  
function property를 유지하는 decorator를 만들기 위해선 `Proxy` object를 사용해야 함!

### Summary

|code|description|
|:---|:---|
|`func.call([context[, ...args]])`|`this`를 `context`로 설정하고 `...args`를 argument로 받는 `func` 실행|
|`func.apply(context[, arguments])`|`this`를 `context`로 설정하고 array-like `arguments`를 argument의 리스트로 받는 `func` 실행|
|`tempobj.method.call(arguments)`|method borrowing|

- argument가 많을 경우 `call` 보다는 `apply`가 더 빠름  
	∵ array-like가 최적화가 더 잘 되어있기 때문
- call forwarding : context와 arguments를 다른 함수로 넘기는 것  
	call forwarding의 기본적인 구조:  
	```javascript
	let wrapper = function() {
	  return original.apply(this, arguments);
	};
	```
- method borrowing : method를 사용하기 위해 빈 객체를 임시로 만들고 method를 사용하는 것
- decorator는 어떤 함수를 argument로 받아서 그 함수의 동작을 바꾸는 wrapper임
	- 함수 자체(주 기능과 복잡성, 코드)는 그대로 유지되어야 함
	
	caching decorator의 기본적인 구조:
	```javascript
	function cachingDecorator(func, hash) {
	  let cache = new Map();
	  return function() { // (1)
		let key = hash(arguments); // (2)
		if (cache.has(key)) {
		  return cache.get(key);
		}

		let result = func.apply(this, arguments); // (3)

		cache.set(key, result);
		return result;
	  };
	}

	function hash(args) {
	  return [].join.call(args); // (4)
	}
	```
	- `(1)`에서 closure 사용  
		cache storage를 구현하기 위함
	- `(2)`에서 object `arguments` 사용  
		`func`의 arguments가 많을 때 key의 생성을 위함
	- `(3)`에서 call forwarding  
		`func`가 `this`를 사용하고 arguments가 많은 method일 경우 대비
	- `(4)`에서 method borrowing  
		array-like `arguments`는 `join()` method를 호출할 수 없기 때문
- array-like `arguments`를 다룰 때 method borrowing을 많이 사용함  
	`Array`인 rest parameter를 대안으로 사용 가능

### Tasks
#### Spy decorator
```javascript
function spy(func) {
  function wrapper(...args) {
    wrapper.calls.push(args);
    return func.apply(this, args);
  }

  wrapper.calls = [];

  return wrapper;
}

work = spy(work);

work(1, 2); // 3
work(4, 5); // 9

for (let args of work.calls) {
  alert( 'call:' + args.join() ); // "call:1,2", "call:4,5"
}
```
- function expression에는 function property를 추가할 수 없음

#### Delaying decorator
```javascript
function delay(f, ms) {
  return function() {
	// return setTimeout(f.apply(this, arguments), ms); // (1)
	return setTimeout(() => f.apply(this, arguments), ms); // (2)
  };
}

let f1000 = delay(f, 1000);
let f1500 = delay(f, 1500);

f1000("test"); // shows "test" after 1000ms
f1500("test"); // shows "test" after 1500ms
```
- `setTimeout`에는 실행시킬 함수가 들어가야 함  
	expression이 들어갈 경우 계산된 결과가 `setTimeout`의 argument로 들어감
	- `(1)`은 `f.apply`를 실행한 반환값을 호출하는 것이기 때문에 의도한대로 작동하지 않음  
		`(2)`는 arrow function이 하나의 함수이기 때문에 `ms` ms가 지난 후 `f.apply`가 호출됨  
		(+ arrow function에서 `this`를 사용하면 outer function의 `this`가 사용되기 때문에 function expression의 `this`가 제대로 들어감)  
		=> `f`가 method여도 정상적으로 실행됨
	
	아래와 같이 구현해도 됨:  
	```javascript
	function delay(f, ms) {
	  return function(...args) {
		let savedThis = this;
		setTimeout(function() {
		  f.apply(savedThis, args);
		}, ms);
	  };
	}
	```

#### Debounce decorator
`f`가 호출되면, 가장 마지막 호출 기준으로 `ms` ms 이후에 그 호출만 실행되게 만듦:  
```javascript
let f = debounce(alert, 1000);

f("a");
setTimeout( () => f("b"), 200);
setTimeout( () => f("c"), 500);

function debounce(func, ms) {
  let timeout;
  return function() {
    clearTimeout(timeout);
    timeout = setTimeout(() => func.apply(this, arguments), ms);
  };
}
```
- 이 예제에서는 `f()`를 on time, 200ms, 500ms에 호출하기 때문에, 1500ms 이후에 `f("c")`를 호출해야 함  
	=> `f`가 호출될 때마다 이전의 `setTimeout`을 취소하고 시간을 바꿔서 새로 호출함
- `f("a")`가 `alert`를 직접 호출하는게 아님에 주의!!  
	이것도 바로 실행하지 않고 `ms` ms 이후에 실행되도록 예약됨

#### Throttle decorator
`f`가 호출되면, `ms` ms 이내에 최대 한 번만 호출되게 만듦:  
```javascript
function f(a) {
  alert(a);
}

let f1000 = throttle(f, 1000);

f1000(1); // shows 1
f1000(2); // (throttling, 1000ms not out yet)
f1000(3); // (throttling, 1000ms not out yet)
// when 1000 ms time out...
// ...outputs 3, intermediate value 2 was ignored

function throttle(func, ms) {
  let isthrottled=false, cargs, cthis;
  function wrapper() {
    if(isthrottled) {
      cargs=arguments;
      cthis=this;
      return;
    }
    isthrottled=true;
    
    func.apply(this, arguments);
    setTimeout(function() {
      isthrottled=false;
      if(cargs) {
        wrapper.apply(cthis, cargs);
        cargs=cthis=null;
      }
    }, ms);
  }
  return wrapper;
}
```
- `isthrottled`가 `true`이면 현재 throttling되고 있음(`ms` ms 이내의 시간이므로 무시되는 중)  
	
	`false`라면 첫 실행이거나 다시 작동시켜야 하는 상황이기 때문에 `true`로 바꾸고 `func` 실행  
	이후 `isthrottled`를 `false`로 바꾸고 `wrapper`를 다시 호출하는 함수를 `ms` ms 이후에 호출  
	이 때 `cargs`가 `null`이 아니면 중간에 무시된 호출이 있다는 뜻이기 때문에 가장 마지막 인자들로 `wrapper`를 호출함(`func`를 호출하지 않고 `wrapper`를 호출하는 이유는 이 호출도 `ms` 안에 최대 한 번 실행되어야 하는 제한이 적용되어야 하기 때문)

> #### ※ debounce와 throttle의 차이
> debounce는 모든 호출을 무시한 뒤 마지막 호출을 `ms` 뒤에 실행되게 만듦
> throttle은 `ms` 이내에 최대 한 번 실행되게 만듦

## Function binding
method를 callback으로 보낼 경우, 실행될 때 `this`를 제대로 찾지 못한다는 문제가 있음

### Losing "this"
```javascript
let user = {
  firstName: "John",
  sayHi() {
    alert(`Hello, ${this.firstName}!`);
  }
};

setTimeout(user.sayHi, 1000); // Hello, undefined!
```
- `user.sayHi`가 object와 떨어져서 호출되어 `this.firstName`을 찾지 못했기 때문에 `undefined`가 출력됨
- 브라우저에 구현된 `setTimeout`는 `this`를 `window`로 설정함(Node.js는 `this`가 timer object가 됨)  
	=> `this.firstName`이 `undefined`가 됨  
	cf. `setTimeout` 이외의 다른 경우에는 `this` 자체가 아예 `undefined`가 되어버림
- wrapper나 binding을 사용해서 context에 맞게 함수를 호출할 수 있음

### Solution 1: a wrapper
```javascript
setTimeout(function() {
  user.sayHi(); // Hello, John!
}, 1000);
```
- `user.sayHi`를 `setTimeout`의 argument로 넘기면 이 함수의 코드만 넘어가지만, wrapper를 이용하면 `user`의 method `sayHi()`가 실행됨  
	```javascript
	setTimeout(() => user.sayHi(), 1000); // Hello, John!
	```
	도 같은 이유로 정상적으로 실행됨
	
	`setTimeout`이 실행되기 전에 `user`의 정보가 바뀐다면 예상과 다른 결과가 나올 수 있음!  
	=> bind로 해결 가능

### Solution 2: bind
```javascript
let boundFunc = func.bind(context);

/*-------------example--------------*/

let user = {
  firstName: "John",
  say(phrase) {
    alert(`${phrase}, ${this.firstName}!`);
  }
};

let say = user.say.bind(user); // (*)

say("Hello"); // Hello, John

setTimeout(() => say("Hello"), 1000); // Hello, John!

user = {
  say() { alert("Another user in setTimeout!"); }
};
```
- `(*)`에서 `user.say()`를 `user`에 bind함  
	=> `say`가 bound function가 됨  
	=> 어디서 호출되든, `user`의 정보가 바뀌든 context가 bind될 당시의 `user`로 고정됨
- `user.say()`가 바뀌더라도 bind될 당시의 `user.say()`가 실행됨  
	`setTimeout`안의 arrow function은 `say()`에 argument를 넣기 위한 것임(wrapper를 이용한 것이 아님)

> Binding all methods  
> 한 객체의 모든 method를 bind해야 할 때 아래와 같이 구현 가능:  
> ```javascript
> for (let key in user) {
>   if (typeof user[key] == 'function') {
>     user[key] = user[key].bind(user);
>   }
> }
> ```
> 
> lodash의 `_.bindAll(obj, methodNames)`와 같이 함수를 제공하기도 함

### Partial functions
The full syntax of bind:  
```javascript
let bound = func.bind(context, [arg1], [arg2], ...);

/*-------------example--------------*/

function mul(a, b) {
  return a * b;
}

let double = mul.bind(null, 2);

alert( double(3) ); // = mul(2, 3) = 6
alert( double(4) ); // = mul(2, 4) = 8
alert( double(5) ); // = mul(2, 5) = 10
```
- `mul`의 parameter `a`를 `2`로 bind함  
	`context`가 필수기 때문에 사용하지 않는 경우 `null`을 넣어줌
- 이렇게 기존의 함수의 parameter를 조절해서 새로운 함수를 만드는 것을 *partial function application*이라고 함
	- 함수의 이름을 다시 지을 수 있음  
	- bind한 parameter는 호출할 때마다 넣어주지 않아도 됨  
		=> generic한 함수를 고쳐서 편의성을 높일 수 있음  
		
		e.g. `send(from, to, text)`를 이용해서 `sendTo(to, text)`를 만들 수 있음

### Going partial without context
`bind`를 사용하면 context도 반드시 넣어야 하므로 `partial` 함수를 따로 구현해놓는 것도 좋음:  
```javascript
function partial(func, ...argsBound) {
  return function(...args) {
    return func.call(this, ...argsBound, ...args);
  }
}

/*-------------example--------------*/

let user = {
  firstName: "John",
  say(time, phrase) {
    alert(`[${time}] ${this.firstName}: ${phrase}!`);
  }
};

user.sayNow = partial(user.say, new Date().getHours() + ':' + new Date().getMinutes());

user.sayNow("Hello"); // [10:00] John: Hello!
```
- `bind`를 사용하지 않고 wrapper로 구현
- lodash에는 `_.partial` 함수가 따로 존재

### Summary

|code|description|
|:---|:---|
|`let bound = func.bind(context, [arg1], [arg2], ...);`|`func`의 context와 arguments를 `context`, `arg1...`로 bind한 새로운 함수 반환|

- context와 arguments 일부를 bind한 함수를 bound function이라고 부름
	- 주로 method를 callback으로 전달하기 위해 사용
- context 말고 arguments만 bind한 함수를 partial function이라고 부름
	- 따로 wrapper로 구현해야 함
- 둘 다 lodash에 `_.bindAll(obj, methodNames)`, `_.partial`로 존재함

### Tasks
```javascript
function f() {
  alert(this.name);
}

f = f.bind( {name: "John"} ).bind( {name: "Ann" } );

f(); // John
```
- 한 번 bound된 함수는 다시 bound될 수 없음!!  
	처음 bound된 context로 고정됨

```javascript
function sayHi() {
  alert( this.name );
}
sayHi.test = 5;

let bound = sayHi.bind({
  name: "John"
});

alert( bound.test ); // undefined
```
- `bind`는 아예 새로운 함수를 반환하기 때문에 function property가 공유되지 않음
- strict mode가 아닐 때 `this`가 정의되지 않으면 `globalThis`를 가리키는 듯

