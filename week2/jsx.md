![jsx](/my-app/static/images/jsx.png)

## React에서 jsx를 사용하는 목적

리액트는 코드만 봐도 희안하게 생긴걸 확인할 수 있다.
```
const element = <h1>Hello, world!</h1>
```
이녀석? 흥미롭게 생겼는걸?
변수에 html? 저렇게 생긴 아이의 이름은 Jsx(javascript XML)라고 한다.

Hello ~ JSX 

놀랍게도 리액트에서 jsx 사용이 필수가 아니라고 한다. (하지만 구글링해서 봤던 리액트는 다 JSX였는걸..?)
필수가 아님에도 대부분의 사람들은 JSX를 사용하고 있는교..? (글쓰다보니 궁금해짐)

1. JS 와 JSX 비교해보니 바로 알겠는걸 (https://babeljs.io/repl에서 확인가능!)
JSX 코드
```
function Greeting({name, age}){
	return (
      <div>
    	<p>Hello, {name}!</p>
      	<p>my age, {age}</p>
      </div>
    )
}
<div>
  <Greeting name="world" age="20"/>
  <button type="submit" onClick="{()=>alert('click!')}">Send</button>
</div>
```
변환된 JS 코드
```
function Greeting({
  name,
  age
}) {
  return React.createElement("div", null, 
    React.createElement("p", null, "Hello, ", name, "!"), 
    React.createElement("p", null, "my age, ", age)
  );
}
React.createElement("div", null, 
    React.createElement(Greeting, {
        name: "world",
        age: "20"
    }), 
    React.createElement("button", {
        type: "submit",
        onClick: "{()=>alert('click!')}"
    }, "Send")
);
```

![StrictMode](/my-app/static/images/strictModeError.png)
++ 아 리액트에서는 <React.Fragment>로 감싸주면 된다! <div>로 감싸줘도 됨!  

코드 가독성이 너무 좋은걸요?
스크립트안에 html를 씀으로써 가독성이 좋아진다!

## Syntactic sugar - 문법적 설탕 - 달달한 문법?
![syntactic-sugar](/my-app/static/images/syntactic-sugar.jpg)
문법적 기능은 그대로인데 그것을 읽는 사람이 직관적으로 쉽게 코드를 읽을 수 있게 만든다. (-> 코드 가독성 향상?)
JSX를 사용하는게 여기에 해당하는 경우

## React.createElement 
javascript에서
```
document.createElement('div');
```
크리에이티드엘리먼트 많이 써봤다.
react에서는 어떻게 쓸까??

```
React.createElement(
  type, // 태그 이름 문자열 | 리액트 컴포넌트 | React.Fragment
  [props], // 리액트 컴포넌트에 넣어주는 데이터 객체
  [ ... children] // 자식으로 넣어주는 요소들
);
```
```
<div>
  <div>
    <h1>주제</h1>
    <ul>
      <li>React</li>
      <li>Vue</li>
    </ul>
   </div>
</div>
```
```
ReactDOM.render(
  React.createElement(
    'div',
    null,
    React.createElement(
      'div',
      null,
      React.createElement('h1', null, '주제'),
      React.createElement(
        'ul',
        null,
        React.createElement('li', null, 'React'),
        React.createElement('li', null, 'Vue')
      )
    )
  ),
  document.querySelector('#root')
);
```


## React Element
엘리먼트는 컴포넌트의 구성요소이며 React앱의 가장 작은 단위다. 엘리먼트는 화면에 표시할 내용을 기술한다.
```
<div id="root"></div>
```
root 안에 들어가는 모든 엘리먼트를 React DOM에서 관리하며 이것을 root DOM 노드라고 부른다. 
일반적으로 React로 구현된 앱은 하나의 Root DOM 노드가 있다.

React 엘리먼트를 root DOM 노드에 렌더링 하려면 ReactDOM.render(element, document.getElementById('root'))에 전달하면된다.

## React StrictMode - 엄격한 모드!
StrictMode는 애플리케이션 내의 잠재적인 문제를 알아내기 위한 도구(개발 모드에서만 활성화) 
UI를 렌더링하지 않으며, 자손들에 대한 부가적인 검사와 경고를 활성화한다라..

자바스크립트에서는 엄격 모드가 있다. 
코드 파일 상단에 "use strict"를 써 놓으면 자바스크립트를 실행할 때 조금 더 엄격하게 코드를 검사한다.
리액트에도 이와 유사한 목적으로 사용하는 <StrictMode />라는 컴포넌트가 있다.

리액트를 가이드라인에 맞추어 사용하는 것이 가장 좋지만 그렇지 않아도 어플리케이션은 그런대로 동작한다. 
이런 결과물은 느리고 불안정할 수 밖에 없는데 문제의 원인을 찾는 것이 좀처럼 어렵다.

Strict 모드를 사용하면 리액트가 자식 컴포넌트를 검사하고 잘못 사용된 부분을 우리에게 알려준다. 

이런 경고 메세지를 보면서 리액트를 사용하면 어플리케이션에 잠재된 문제를 미리 해결할 수 있을 것이다.

일단 사용법
```
import React from 'react';

function ExampleApplication() {
  return (
    <div>
      <Header />
      <React.StrictMode>
        <div>
          <ComponentOne />
          <ComponentTwo />
        </div>
      </React.StrictMode>
      <Footer />
    </div>
  );
}
```

<React.StrictMode></React.StrictMode> 로 엄격히 검사할 영역을 감싸줌!


## VDOM(Virtual DOM)이란?
![ VDOM 트리](/my-app/static/images/virtualDomTree.jpeg)
재조정을 막 하지는 않는다? 유지보수에 좋다?
"이 접근방식이 React의 선언적 API를 가능하게 합니다." <- 이게 VDOM의 핵심!

편지 쓰다 맞춤법 틀리면 찢어버리고 다시 그린다. -> DOM
찢어버리고 싶은거 참고 화이트로 틀린 부분만 수정해서 다시 쓴다. -> VDOM (가상돔은 필요한 부분만 쏙 골라집는다!)

### DOM 이란?
![ DOM 트리](/my-app/static/images/DomTree.webp)
문서 객체 모델(The Document Object Model, 이하 DOM) 은 HTML, XML 문서의 프로그래밍 interface 이다.
DOM은 문서의 구조화된 표현(structured representation)을 제공하며 프로그래밍 언어가 DOM 구조에 접근할 수 있는 방법을 제공하여 
그들이 문서 구조, 스타일, 내용 등을 변경할 수 있게 돕는다. DOM 은 nodes와 objects로 문서를 표현한다. 
이들은 웹 페이지를 스크립트 또는 프로그래밍 언어들에서 사용될 수 있게 연결시켜주는 역할을 담당한다.

(https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/Introduction)

### DOM과 Virtual DOM의 차이
![ DOM과 Virtual DOM의 차이](/my-app/static/images/dom_virtualDom.png)
(https://doqtqu.tistory.com/316)


## Reconciliation(재조정) 과정은 무엇인가?
리액트 공식 사이트에서 정의된 재조정의 정의!

React는 선언적 API를 제공하기 때문에 갱신이 될 때마다 매번 무엇이 바뀌었는지를 걱정할 필요가 없습니다. 
이는 애플리케이션 작성을 무척 쉽게 만들어주지만, React 내부에서 어떤 일이 일어나고 있는지는 명확히 눈에 보이지 않습니다. 
이 글에서는 우리가 React의 “비교 (diffing)” 알고리즘을 만들 때 어떤 선택을 했는지를 소개합니다. 
이 비교 알고리즘 덕분에 컴포넌트의 갱신이 예측 가능해지면서도 고성능 앱이라고 불러도 손색없을 만큼 충분히 빠른 앱을 만들 수 있습니다.

1. 서로 다른 타입의 두 엘리먼트는 서로 다른 트리를 만들어낸다.
2. 개발자가 key prop을 통해, 여러 렌더링 사이에서 어떤 자식 엘리먼트가 변경되지 않아야 할지 표시해 줄 수 있다.

### 비교 알고리즘 (Diffing Algorithm)
두 개의 트리를 비교할 때, React는 두 엘리먼트의 루트(root) 엘리먼트부터 비교합니다. 
이후의 동작은 루트 엘리먼트의 타입에 따라 달라집니다.

- 엘리먼트의 타입이 다른 경우 (아예 이전 트리를 버리고 새로운 트리 구축!)
- DOM 엘리먼트의 타입이 같은 경우 (동일한 내역은 유지하고 변경된 속성들만 갱신, fontWeight 수정 x, color 속성만 수정)
```
<div style={{color: 'red', fontWeight: 'bold'}} />
<div style={{color: 'green', fontWeight: 'bold'}} />
```
- 같은 타입의 컴포넌트 엘리먼트
- 자식에 대한 재귀적 처리