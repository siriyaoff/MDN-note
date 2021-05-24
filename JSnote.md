Part 1: The JavaScript language
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
	- Ruby와 같이 사용됨