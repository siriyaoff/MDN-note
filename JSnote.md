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
- `0`이 자동으로 `"0"`(`string`)으로 바뀜
- `obj["0"]`, `obj[0]` 두 가지 방식으로 호출할 수 있음  

***************
객체 배열을 선언하면 그것과는 구별을 어떻게 하나?
***************

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

Integer property : `"1"`, `"41"`과 같이 property name을 Integer로 변환했다가 다시 `string`으로 변환해도 값이 같은 property(`"+41"`, `"1.2"`는 같지 않음)
⇔ `name == String(Math.trunc(Number(name)))`

"for...in"으로 key를 나열하면, 
- Integer property인 경우 크기 순으로 나열됨
- 아닌 경우 생성된 순으로 나열됨

※ 숫자들을 key로 사용하고 싶지만 생성된 순으로 나열되기 하고 싶을 때는 `"+49"`와 같이 선언하고 출력할 때 `number`로 변환해서 출력하면 됨!!

### Summary
`Array`, `Date`, `Error` 등의 다양한 `object`들이 존재함(나중에 배울 예정)

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
	
	(2) : 위의 `for...in`을 이용한 방법이랑 같은 방법임

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

### A simple example
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

## Symbol type
specification에 따르면, object property key는 `string` type이거나 `symbol` type임  

### Symbols
`Symbol()`을 사용해서 unique identifier을 만들 수 있음:  
```javascript
// id is a symbol with the description "id"
let id = Symbol("id");

let id1 = Symbol("id");

alert(id == id1); // false
```
- 같은 description을 써서 생성하더라도 둘은 다른 `symbol`들임

※ symbol들은 자동으로 `string`으로 변환되지 않음!!  
```javascript
let id = Symbol("id");
alert(id); // TypeError: Cannot convert a Symbol value to a string
alert(id.toString()); // Symbol(id), now it works
alert(id.description); // id
```
- `symbol`과 `string`은 근본적으로 다르기 때문에 `symbol`은 아예 다른 형으로 변환되는 것이 막혀있음
- `symbol`을 출력하기 위해서는 `toString()`을 이용하거나 description을 출력해야 함

### "Hidden" properties
`symbol`을 key로 이용해서 숨겨진 property를 생성할 수 있음  
=> `symbol`을 이용하지 않고는 접근할 수 없음

#### Example
```javascript
let user = { // belongs to another code
  name: "John"
};

let id = Symbol("id");

user[id] = 1;

alert( user[id] ); // we can access the data using the symbol as the key
```
- `symbol`은 항상 다르기 때문에, 다른 곳에서 똑같은 `id`를 `symbol`로 사용하더라도 `user[id]`는 서로 다른 properties가 됨  
	cf. `"id"`를 property name으로 사용할 경우 충돌이 일어남

### Symbols in an object literal
square brackets `[]`를 이용해서 object literal에서도 `symbol`을 사용할 수 있음:  
```javascript
let id = Symbol("id");

let user = {
  name: "John",
  [id]: 123 // not "id": 123
};
```

### Symbols are skipped by for...in
`symbol`로 선언된 property는 심지어 `for...in` 반복문에서도 배제됨:  
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
global symbol을 이용해서 다른 곳에서 같은 `symbol`을 사용할 수 있음  
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
- 모든 `symbol`들은 `description` property를 가짐!  
	global symbol도 key가 description이기 때문에 `.description`으로 출력 가능함

### System symbols
system symbols가 존재함:
- Symbol.hasInstance
- Symbol.isConcatSpreadable
- Symbol.iterator
- Symbol.toPrimitive
	- object to primitive conversion에 필요함

### Summary
|function|description|
|:---|:---|
|`Symbol([description])`|`symbol` 생성|
|`sym.description`|`sym`의 description 출력|
|`Symbol.for(key)`|global symbol 생성|
|`Symbol.keyFor(sym)`|global symbol의 key|

`Object.getOwnPropertySymbols(obj)`를 사용하면 properties 뿐만 아니라 symbol들까지 알 수 있음  
`Reflect.ownKeys(obj)`를 사용하면 symbolic properties를 포함해서 모든 properties의 key를 알 수 있음

## Object to primitive conversion
