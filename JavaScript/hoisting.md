# Hoisting

JavaScript에서 `var` 키워드 변수 선언이 위로 끌어올려지는 것. 변수가 함수 내에서 정의된 경우 선언이 함수 최상위로, 함수 바깥에서 정의되었을 경우 전역 컨텍스트의 최상위로 변경된다.

JavaScript 엔진은 코드를 인터프리팅 하기 전에 그 코드를 먼저 컴파일한다. `var a=2;`를 하나의 구문으로 생각할 수도 있지만, JavaScript는 `var a;`와 `a=2;`, 두 개의 구문으로 분리한다. 즉, 변수 선언 단계와 초기화 단계를 나누고 선언 단계에서는 그 선언이 소스코드의 어디에 위치하든 해당 스코프의 컴파일 단계에서 처리해버리는 것이다.

## 우선순위

변수 선언 > 함수 선언 > 변수 할당