# 브라우저 동작 과정

브라우저의 핵심 기능은 사용자가 원하는 웹페이지를 서버에 요청하고 응답을 받아 브라우저에 표시하는 것이다. 이 동작 과정을 알아보자.

## 개요

![](/_Images/render-tree-construction.png)

[이미지 출처](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction?hl=ko)

1. 서버로부터 HTML, CSS JavaScript, 이미지 파일 등을 응답받는다.
2. HTML 마크업을 처리하고 DOM 트리를 빌드한다.
3. CSS 마크업을 처리하고 CSSOM 트리를 빌드한다.
4. DOM 및 CSSOM을 결합하여 렌더 트리를 형성한다.
5. 렌더 트리에서 레이아웃을 실행하여 각 노드의 기하학적 형태를 계산한다.
6. 개별 노드를 화면에 페인트한다.

## Reference

- [5.4 Javascript Environment 브라우저 동작 원리](https://poiemaweb.com/js-browser) by Poiemaweb
- [브라우저 동작 원리](https://juunone.github.io/browser/) by Juunone
- [[자바스크립트] 브라우저 렌더링](https://12bme.tistory.com/140)
- [브라우저 렌더링 과정 - Reflow Repaint, 그리고 성능 최적화](https://boxfoxs.tistory.com/408) by 박스여우
- [브라우저는 어떻게 동작하는가?](https://d2.naver.com/helloworld/59361) by NAVER D2
- [렌더링 트리 생성, 레이아웃 및 페인트](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction?hl=ko) by Google
