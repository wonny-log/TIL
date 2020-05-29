# Vue Component

## Overview

```js
Vue.component("button-counter", {
  data: function () {
    return {
      count: 0,
    };
  },
  template:
    '<button v-on:click="count++">You clicked me {{ count }} times.</button>',
});
```

컴포넌트는 이름을 가진 재사용가능한 Vue 인스턴스입니다. `new Vue`으로 생성하는 루트 Vue 인스턴스 안에서 커스텀 엘레멘트로 사용할 수 있습니다.

```html
<div id="components-demo">
  <button-counter></button-counter>
</div>
```

```js
new Vue({ el: "#components-demo" });
```

`el`와 같이 루트에만 사용하는 옵션을 제외한 모든 옵션과 라이프싸이클 훅을 사용할 수 있습니다.

## 컴포넌트 재사용하기

컴포넌트를 재사용할 수 있는데 이때 컴포넌트의 `data`는 객체를 직접 넣어주는 것이 아니라 함수여야 합니다. 그렇지 않으면 해당 컴포넌트 전부가 하나의 객체만을 참고하여 각각의 상태를 가질 수 없습니다.

```js
data: function () {
  return {
    count: 0
  }
}
```

## 컴포넌트 구성하기

컴포넌트는 전역과 로컬에 등록할 수 있습니다.

**전역**

전역 컴포넌트는 루트 Vue 인스턴스 템플릿 안에서

```js
Vue.component("my-component-name", {
  // ... options ...
});
```
