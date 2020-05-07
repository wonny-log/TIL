# React

## React를 사용하는 이유

1. 자바스크립트 프레임워크, 라이브러리 중에서 가장 인기가 많기에 제일 큰 생태계를 가지고 있다. 생태계가 클수록 참고할 수 있는 자료가 많아서 시행착오를 덜 겪을 수 있고, 이는 곳 개발 생산성을 향상시킨다.
2. 컴포넌트 기반이기 때문에 작은 단위로 UI를 구현할 수 있어 재사용성과 유지보수성이 높다.
3. 단방향 데이터 흐름을 가지고 있기 때문에 유지보수성이 높다. 양방향인 경우 데이터 흐름을 추적하기 어려워서 규모가 커질수록 유지보수가 어렵다.

## Virtual DOM

DOM을 업데이트 하기 위해서는 비용이 많이 든다. DOM을 조작할 때마다 엔진이 웹 페이지를 새로 그리기 때문이다. 리액에서는 Virtual DOM 방식을 사용하여 DOM 업데이트를 추상화하여 DOM 처리 횟수를 최소화하여 성능을 개선하고자 했다.

Virtual DOM을 사용하면 실제 DOM에 접근하여 조작하는 대신 이를 추상화한 자바스크립트 객체를 구성하여 사용한다. 그래서 데이터가 업데이트 되면 전체 UI를 Virtual DOM에 리렌더링하고 이전 Virtual DOM에 있던 내용과 현재 내용을 비교한다. 비교한 후 바뀐 부분만 실제 DOM에 적용한다.

## HOC(High-Order-Component)

컴포넌트 로직을 재사용하기 위한 패턴이다. 컴포넌트를 받아서 컴포넌트를 반환하는 함수를 이용하여 구현한다.

## Flux

단방향 데이터 흐름의 아키텍쳐이다. Dispatcher > Store > View 흐름으로 데이터가 흐른다. 유저가 액션을 하면 Dispatcher를 사용하여 Store에 변경을 일으켜서 변경사항을 View에 반영하도록 한다.

## Redux

Flux 아키텍처를 기반으로한 단방향 데이터 흐름 상태 관리 라이브러리이다. Reducer > Store > View 흐름으로 데이터가 흐른다.

### 규칙

- 단일 스토어
- 읽기 전용 상태: 상태를 직접 접근하여 변경하지 않고 새로운 객체를 생성해줘야 한다.
- 리듀서는 순수 함수

> 리덕스에서 불변성을 유지해야 하는 이유
> 내부적으로 데이터가 변경되는 것을 감지하기 위해 얕은 비교 검사를 하기 때문이다. 객체의 변화를 감지할 때 객체의 깊숙한 안쪽까지 비교하는 것이 아니라 겉핥기 식으로 비교하여 좋은 성능을 유지할 수 있다.

### 미들웨어

액션과 리듀서 사이의 중간자이다. 액션을 디스패치했을 때 리듀서에서 이를 처리하기에 앞서 사전에 지정된 작업들을 실행한다.

**비동기 작업 관련 미들웨어 라이브러리**

- redux-thunk: 객체가 아닌 함수 형태의 액션을 디스패치할 수 있게 해줍니다.
- redux-saga: 특정 액션이 디스패치되었을 때 정해진 로직에 따라 다른 액션을 디스패치시키는 규칙을 작성하여 비동기 작업을 처리할 수 있게 해줍니다.