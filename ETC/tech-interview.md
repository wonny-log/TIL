# Tech Interview

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

## HTML

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

### Event Loop

한 번에 하나의 작업만 처리할 수 있는 단일 스레드 언어인 JavaScript에서 동시성(concurrency) 처리를 지원하기 위해 사용하는 컨셉.

JavaScript 엔진은 Call Stack을 통해 요청된 task를 순차적으로 실행할뿐, 실질적으로 동시성을 지원하기 위한 Event Loop는 JavaScript가 동작하는 환경(브라우저, Node.js 등)이 담당한다.

JavaScript 엔진은 Call Stack과 Heap 영역으로 나뉨. Call Stack은 요청된 작업을 FIFO 형태의 배열로 쌓아서 순차적으로 실행한다. 그러므로 JavaScript는 실행하고 있는 작업이 종료되기 전까지는 다른 어떤 작업도 수행할 수 없음(Run to Completion 방식). Heap은 동적으로 생성된 객체 인스턴스가 할당된다.

Call Stack 내에서 현재 실행중인 작업이 있는지 확인하여 Call Stack이 비워질 때 Event Queue에서 작업을 꺼내와서 Call Stack으로 보낸다.

- Reference
  - [자바스크립트와 이벤트 루프 | TOAST](https://meetup.toast.com/posts/89)
  - [이벤트 | Poiemaweb](https://poiemaweb.com/js-event)

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

### Scope

변수나 함수 이름 충돌을 피하기 위해 정의한 규칙. 함수 레벨과 블록 레벨의 렉시컬 스코프(소스코드가 작성된 그 문맥에서 결정되는 것) 규칙을 따른다.

- 함수 레벨 스코프: `var` 키워드로 선언된 변수, 함수 선언식으로 만들어진 함수
- 블록 레벨 스코프: `let`, `const` 키워드로 선언된 변수와 함수

- Reference
  - [자바스크립트의 스코프와 클로저 | TOAST](https://meetup.toast.com/posts/86)

### Hoisting

JavaScript에서 `var` 키워드 변수 선언이 위로 끌어올려지는 것. 변수가 함수 내에서 정의된 경우 선언이 함수 최상위로, 함수 바깥에서 정의되었을 경우 전역 컨텍스트의 최상위로 변경된다.

우선순위: 변수 선언 > 함수 선언 > 변수 할당

// TODO: 아래 내용 채우기

### Closure

## React

### React란?

### React의 특징

## 웹

### 브라우저 동작 과정
