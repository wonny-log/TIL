# Tech Interview

## 질문 출처

- [프론트엔드 면접 질문 모음](https://velog.io/@honeysuckle/%EC%8B%A0%EC%9E%85-%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%EB%A9%B4%EC%A0%91-%EC%A7%88%EB%AC%B8-%EB%AA%A8%EC%9D%8C)
  - [프론트엔드 직군 웹개발자 면접질문 모음 답변 달아보기](https://blex.me/@yoyounn18/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%A7%81%EA%B5%B0-%EC%9B%B9%EA%B0%9C%EB%B0%9C%EC%9E%90-%EB%A9%B4%EC%A0%91%EC%A7%88%EB%AC%B8-%EB%AA%A8%EC%9D%8C-%EB%8B%B5%EB%B3%80-%EB%8B%AC%EC%95%84%EB%B3%B4%EA%B8%B0)
- [Interview_Question_for_Beginner](https://github.com/JaeYeopHan/Interview_Question_for_Beginner)
  - [React 면접 내용](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/issues/68)
- [React / Node.js Fullstack 개발직군 면접 후기](https://yoon.site/react-node-js-fullstack-%EA%B0%9C%EB%B0%9C%EC%A7%81%EA%B5%B0-%EB%A9%B4%EC%A0%91-%ED%9B%84%EA%B8%B0/)

## 목차

- [HTML](#HTML)
  - [article vs section vs div](#article-vs-section-vs-div)
- [CSS](#CSS)
  - [padding vs margin](#padding-vs-margin)
  - [CSS 우선순위](#CSS-우선순위)
- [JavaScript](#JavaScript)
  - [Event Loop](#Event-Loop)
  - [마이크로 테스트](#마이크로-테스트)
  - [Callback Function](#Callback-Function)
  - [Promise](#Promise)
  - [Async/Await](#AsyncAwait)
  - [ES6 문법](#ES6-문법)
  - [Scope](#Scope)
  - [Hoisting](#Hoisting)
  - [Closure](#Closure)
  - [This](#This)
  - [이벤트 전파](#이벤트-전파)
- [React](#React)
  - [React란?](#React란)
  - [Next.js](#Nextjs)
  - [Hooks](#Hooks)
  - [Context API](#Context-API)
  - [Flux](#Flux)
  - [MobX vs Redux](#MobX-vs-Redux)
- [웹](#웹)
  - [브라우저 동작 과정](#브라우저-동작-과정)
- [함수형 프로그래밍](#함수형-프로그래밍)
  - [함수형 프로그래밍이란?](#함수형-프로그래밍이란)
  - [순수 함수](#순수-함수)
- [OOP](#OOP)
  - [OOP 특징](#OOP-특징)
- [TypeScript](#TypeScript)

---

### article vs section vs div

- article: 블로그 글, 뉴스 기사와 같이 독립적으로 사용할 수 있는 구획을 나타날 때 사용하는 요소. 각 아티클을 식별하기 위해 헤딩 요소(h1-h6)를 반드시 포함해야 한다.
- section: 관계가 있는 내용을 묶고 싶을 때 사용하는 요소.
- div: 의미적으로 관계가 없지만 내용을 묶고 싶을 때 사용하는 요소.

## CSS

### padding vs margin

- padding: content와 border 사이 안쪽 여백을 설정하는 요소.
- margin: border 바깥 여백을 설정하는 요소.

### CSS 우선순위

1. !important가 붙은 속성
2. inline으로 지정한 속성
3. 선택자가 #id인 속성
4. 선택자가 .class 및 pseudo 클래스(:hover 같은 것)인 속성
5. 선택자가 tag인 속성

같은 우선순위를 가지는 경우 나중에 선언한 속성의 우선순위가 높다.

## JavaScript

### [Event Loop](/JavaScript/event-loop.md)

### 마이크로 테스트

일반 테스크보다 높은 우선순위를 갖는 테스크. 그러므로 Event Queue에 작업이 있더라도 마이크로 테스크가 먼저 됨. 대표적으로 프라미스가 마이크로 테스크를 사용한다.

### Callback Function

비동기 처리를 위해 다른 함수의 파라미터로 넘겨주는 함수로 원하는 시점에 호출할 수 있다.

### Promise

비동기 처리를 위해 사용되는 객체로 Pending(대기), Fulfilled(이행), Rejected(실패) 상태를 가진다.

### Async/Await

비동기 처리에 사용되는 문법으로 Promise를 반환하는 함수 앞에 async 키워드를, Promise를 반환하는 비동기 처리 메서드 앞에 await를 사용한다. await 키워드는 async 함수 안에서만 사용할 수 있다. await 키워드를 만나면 Promise가 처리될 때까지 기다린다.

### ES6 문법

ES6 문법에는 화살표 함수, 클래스, let과 const, 제너레이터, 프라미스, async/await, 스프래드 연산자 등이 있다.

### [Scope](/JavaScript/scope.md)

### Hoisting

JavaScript에서 `var` 키워드 변수 선언이 위로 끌어올려지는 것. 변수가 함수 내에서 정의된 경우 선언이 함수 최상위로, 함수 바깥에서 정의되었을 경우 전역 컨텍스트의 최상위로 변경된다.

우선순위: 변수 선언 > 함수 선언 > 변수 할당

### Closure

함수와 그 함수가 선언됐을 때의 렉시컬 환경과의 조합. 함수가 자신이 속한 렉시컬 스코프를 참조할 수 있는 것이다.

자신을 포함하고 있는 외부함수보다 내부함수가 더 오래 유지되는 경우, 외부 함수 밖에서 내부함수가 호출되더라도 외부함수의 지역 변수에 접근할 수 있는데 이러한 함수를 클로저라고 부른다.

현재 상태를 기억하고 이 상태가 변경되어도 최신 상태를 유지해야 하는 상황에 유용하다. 만일 클로저라는 기능이 없다면 상태를 유지하기 위해 전역 변수를 사용해야 하는데 전역 변수는 누구나 접근하고 변경할 수 있기에 많은 부작용을 유발하므로 사용을 자제해야 한다.

### This

JavaScript의 모든 함수는 실행될 때마다 함수 내부에 `this`라는 객체가 추가된다. 함수가 호출된 상황에 따라 `this`가 달라진다.

- 객체의 메서드를 호출할 때: 함수를 실행할 때 함수를 소유하고 있는 객체를 참조
- 함수를 호출할 때: 전역 객체를 참조
- 생성자 함수를 통해 객체를 생성할 때: 객체 자신를 참조
- apply, call, bind를 통한 호출
  - bind: 함수를 선언할 때 this와 파라미터 지정
  - call: 함수를 호출할 때 this와 파라미터 지정
  - apply: 함수를 호출할 때 this와 파라미터 지정, 배열 형태로 파라미터를 넘겨준다.

### [이벤트 전파](/JavaScript/event-propagation.md)

## React

### React란?

페이스북에서 개발하고 관리하는 사용자 인터페이스를 구현하기 위한 JavaScript 라이브러리.

데이터 변화에 따라 뷰를 어떻게 업데이트할지 고려하지 않고 바뀐 데이터로 일단 뷰를 그리고 바뀐 부분만 찾아서 업데이트 해주는 방식이다.

### Next.js

서버 사이드 렌더링, 페이지 기반 라우팅 시스템, 코드 스플릿팅 등을 지원하는 리액트 프레임워크.

### Hooks

리액트 v16.8에 새로 도입된 기능으로 함수형 컴포넌트에서도 상태 관리를 할 수 있게 해준다.

컴포넌트로부터 상태와 관련된 로직을 추상화하여 재사용할 수 있게 해준다.

기존 라이프 싸이클 메서드에서는 상태 관련 로직이 한 메서드에 다 모여있어야 해서 관리하기 어려웠다. 그래서 라이프 싸이클이 아닌 로직에 기반을 둔 함수로 나눌 수 있게 해준다.

### Context API

전역 상태 관리를 위한 기능. 각 컴포넌트들이 부모 컴포넌트를 거치지 않고 직접적으로 데이터를 공유할 수 있게 해준다.

### Flux

양방향으로 데이터가 흐르는 MVC 패턴에서 애플리케이션 규모가 커질수록 관리의 복잡성이 높아져서 단방향으로 데이터가 흐르는 Flux 패턴을 도입했다.

데이터는 항상 Dispatcher -> Store -> View 으로 흐른다.

### MobX vs Redux

- Redux: 함수형 프로그래밍 패러다임 따름, 불변성 필수
- MobX: 객체지향형 프로그래밍 패러다임 따름, 불변성 유지 필요 없음

## 웹

### 브라우저 동작 과정

- URL을 통해 서버에서 HTML와 같은 자원을 요청해서 받아온다.
- DOM 트리 구축을 위해 HTML을 파싱한다.
- 태그를 모두 DOM 노드로 변환한다.
- 스타일 요소를 파싱해서 CSS 객체 모델 생성
- Render Tree 생성
- Render Tree 배치
- Render Tree 그리기

## 함수형 프로그래밍

### 함수형 프로그래밍이란?

함수를 이용해서 사이드 이펙트가 없도록 선언형 프로그래밍을 이용하는 것이다.

### 순수 함수

동일한 인풋에는 항상 같은 값을 반환한다. 함수의 실행은 프로그램 실행에 영향을 미치지 않는다.

## OOP

### OOP 특징

- 추상화: 각 객체들의 공통된 특성을 뽑아냄
- 캡슐화: 데이터를 은닉하고 데이터의 기능을 노출시키지 않음
- 상속성: 하나의 클래스가 가진 특징을 그대로 다른 클래스에 물려줌
- 다형성: 같은 함수를 받아도 각자 다른 일을 함

## TypeScript

JavaScript의 대체 언어 중 하나로 정적 타이핑을 지원하는 JavaScript의 확장 언어이다.
