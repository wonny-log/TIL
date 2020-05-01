# Event Loop

## JavaScript 엔진

JavaScript 엔진은 Call Stack과 Heap 영역으로 나뉘어 있다.

- Call Stack: 요청된 작업을 FIFO 형태의 배열로 쌓아서 순차적으로 실행하는 영역이다.
  - JavaScript는 단 하나의 Call Stack을 가지기 때문에 실행하고 있는 작업이 종료되기 전까지는 다른 어떤 작업도 수행할 수 없다. 이를 Run to Completion 방식이라고도 부른다.
- Heap: 동적으로 생성된 객체 인스턴스가 할당되는 영역이다.

## Event Loop란?

한 번에 하나의 작업만 처리할 수 있는 단일 스레드 언어인 JavaScript에서 동시성(Concurrency) 처리를 지원하기 위해 사용하는 컨셉이다.

> 컴퓨터 공학에서 이벤트 루프란 이벤트나 메시지를 대기하고 있다가 처리해주는 프로그래밍 구조체 혹은 디자인 패턴을 의미한다.

Call Stack 내에서 현재 실행중인 작업이 있는지 확인하여 Call Stack이 비워질 때 Event Queue에서 작업을 꺼내와서 Call Stack으로 보냄으로 동시성을 지원한다.

## Event Loop는 어디에 있나요?

JavaScript 엔진은 Call Stack을 통해 요청된 task를 순차적으로 실행할뿐, 실질적으로 동시성을 지원하기 위한 Event Loop는 JavaScript가 동작하는 환경(브라우저, Node.js 등)이 담당한다.

## 예시

```javascript
function delay() {
  for (var i = 0; i < 100000; i++);
}
function foo() {
  delay();
  bar();
  console.log("foo!");
}
function bar() {
  delay();
  console.log("bar!");
}
function baz() {
  console.log("baz!");
}

setTimeout(baz, 10);
foo();

// result: bar! -> foo! -> baz!
```

## Reference

- [자바스크립트와 이벤트 루프 | TOAST](https://meetup.toast.com/posts/89)
- [이벤트 | Poiemaweb](https://poiemaweb.com/js-event)
