# Event Propagation (이벤트 전파)

## Event Bubbling

특정 화면 요소에서 이벤트가 발생했을 때 해당 이벤트가 더 상위 화면 요소들로 전달되어 가는 특성을 의미한다.

```javascript
div.addEventLostener("click", (event) => {
  console.log(event.currentTarget.className);
});
```

## Event Capture

이벤트 캡쳐는 이벤트 버블링과 반대 방향으로 진행되는 이벤트 전파 방식으로, 이벤트가 발생했을 때 해당 이벤트가 더 하위 화면 요소들로 전달되어 가는 특성을 의미한다.

```javascript
div.addEventLostener(
  "click",
  (event) => {
    console.log(event.currentTarget.className);
  },
  {
    capture: true,
  }
);
```

## 이벤트 전파 방지: event.stopPropagation()

원하는 화면 요소에만 이벤트가 발생하기를 원할 때는 `event.stopPropagation()` Web API를 사용하면 된다.

이벤트 버블링의 경우에는 클릭한 요소의 이벤트만 발생시키고 상위 요소로 이벤트 전달하는 것을 막는다. 이벤트 캡쳐의 경우에는 클릭한 요소의 최상위 요소 이벤트만 동작시키고 하위 요소들로 이벤트를 전달하지 않는다.

```javascript
div.addEventLostener("click", (event) => {
  event.stopPropagation();
  console.log(event.currentTarget.className);
});
```

## Reference

- [이벤트 버블링, 이벤트 캡처 그리고 이벤트 위임까지](https://joshua1988.github.io/web-development/javascript/event-propagation-delegation/) by Captain Pangyo
