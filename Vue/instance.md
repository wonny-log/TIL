# Vue Instance

## Vue 인스턴스 만들기

모든 Vue 앱은 `Vue` 함수로 새 Vue 인스턴스를 만드는 것부터 시작함

```html
<script>
  // 관례적으로 vm(ViewModel의 약자)를 사용함
  var vm = new Vue({
    // options
  });
</script>
```

## 데이터와 메소드

Vue 인스턴스가 생성될 때 Vue의 반응형 시스템은 `data` 객체에 있는 모든 속성을 추가하고, 속성값이 바뀔 때 뷰는 새 값에 맞춰 업데이트됨

```js
var data = { a: 1 };

var vm = new Vue({
  data: data,
});

vm.a == data.a; // => true

vm.a = 2;
data.a; // => 2

data.a = 3;
vm.a; // => 3
```

데이터가 변경되변 뷰는 리랜더링 됨

`data`에 있는 속성들은 인스턴스가 생성될 때 존재하는 값에 대해서만 반응형이므로 `vm.b = 'hi'` 와 같이 새 속성을 추가하고 `b`가 변경되어도 화면이 갱신되지 않음

만일 어떤 속성이 나중에 필요할 것이라고 생각되며, 빈 값이거나 존재하지 않는 상태로 시작한다면 아래와 같이 초기값을 지정할 필요가 있음

```js
data: {
  newTodoText: "",
  visitCount: 0,
  hideCompletedTodos: false,
  todos: [],
  error: null,
}
```

### `Object.freeze()`

예외는 `Object.freeze()`를 사용하는 경우인데 이는 기존 속성이 변경되는 것을 막아서 반응성 시스템이 추적할 수 없음을 의미함

```js
var obj = {
  foo: "bar",
};

Object.freeze(obj);

new Vue({
  el: "#app",
  data: obj,
});
```

### `$`

다른 사용자 정의 속성과 구분하기 위해 `$` 접두어를 사용함

```js
var data = { a: 1 };
var vm = new Vue({
  el: "#app",
  data: data,
});

vm.$data === data; // => true
vm.$el === document.getElementById("app"); // => true

// $watch는 인스턴스 메소드
vm.$watch("a", function (newVal, oldVal) {
  // `vm.a`가 변경되면 호출됨
});
```

## 라이프사이클 훅

- `created`, `mounted`, `updated`, `destroyed` 있음
- 모든 라이프싸이클 훅은 Vue 인스턴스를 가리키는 `this` 컨텍스트를 활용하여 호출됨

```js
new Vue({
  data: {
    a: 1,
  },
  created: function () {
    console.log("a is: " + this.a);
  },
});
// => a is: 1
```

> options 속성이나 콜백에 화살표 함수 사용 지양 ex) created: () => console.log(this.a)
> 화살표 함수들은 부모 컨텍스트에 바인딩되기 때문에 `this` 컨텍스트가 호출하는 Vue 인스턴스에서 사용할 경우 오류가 발생함

## 라이프싸이클 다이어그램

![](/_Images/vue-lifecycle.png)
