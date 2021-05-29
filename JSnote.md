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
JS에서의 `string` 표현 방법 3가지:
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
`boolean`은 `true`, `false` 두 가지 값만 가질 수 있음  
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
반면 `object`는 더 복잡한 데이터를 저장함

`symbol`은 `object`의 identifier를 생성할 때 사용함

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
result=promprt(title, [default]);
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
예를 들어 `alert`는 자동으로 값을 `string`으로 바꿔서 출력하고 mathematical operations는 값을 숫자로 바꿈

`object`에 대해서는 나중에 object to primitive conversion을 살펴볼 예정

### String Conversion
`String(value)` function을 이용해서 `string`으로 conversion 가능

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
|`string`|Trim 후 남아있는 string이 없으면 `0`, 아니면 숫자를 읽음, string에 숫자만 있는게 아니면 `NaN` 리턴|

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
- `+` 연산자의 경우 `string`, `number` type이 둘 다 존재하면 concatenation으로 취급됨
	- 계산 순서에 유의(교환법칙 성립하지 않음!)
- 다른 수학 연산자들은 모두 `string`이 `number`로 conversion된 후 계산됨

### Numeric conversion, unary `+`
`number` 타입에 대해서는 아무런 영향이 없지만, 다른 타입들에 대해선 `number`로 conversion을 실행함  
`Number(...)` function과 동일  
아래와 같이 `string`으로 표현된 숫자들을 더할 때 유용함  
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
비교하는 값들의 type이 다를 경우 값들을 `number`로 변환해서 비교함  

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
- `string`과 `number`를 비교할 때는 `string`을 캐스팅하지 않아도 됨(`number`이 있어서 자동으로 변환됨)

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
	