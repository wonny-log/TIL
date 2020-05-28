# Vue List Rendering

## `v-for`

- 부모 스코프 속성에 대한 모든 권한이 있음

```html
<ul id="app">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>

<script>
  var app = new Vue({
    el: "#app",
    data: {
      parentMessage: "Parent",
      items: [{ message: "Foo" }, { message: "bar" }],
    },
  });
</script>
```

`in` 대신 `of` 구분자도 사용 가능

```html
<div v-for="item of items"></div>
```

## `v-for`와 객체

```html
<ul id="app" class="demo">
  <li v-for="(value, name, index) in object">
    {{ index }}. {{ name }} : {{ value }}
  </li>
</ul>

<script>
  var app = new Vue({
    el: "#app",
    data: {
      object: {
        title: "How to do lists in Vue",
        author: "Jane Doe",
        publishedAt: "2020-04-01",
      },
    },
  });
</script>
```

## state 유지하기

`v-for`에서 렌더링된 엘리먼트 목록을 갱신할 때 'in-place patch' 전략을 사용함. 데이터 항목 순서가 변경될 때 DOM 요소를 이동하는 것이 아니라 각 요소를 적절한 위치에 패치하고 해당 인덱스에서 렌더링할 내용을 반영하는지 확인함

이 기본 모드는 효율적이지만 목록의 출력 결과가 하위 컴포넌트 상태 또는 임시 DOM 상태(예: 폼 input)에 의존하지 않는 경우에 적합함

개별 DOM 노드들을 추적하고 기존 엘리먼트를 재사용, 재정렬하기 위해서 `key` 속성을 제공해야 함. 의도적인 성능 향상 등의 이유가 아닌 다음에는 가능한 `key` 추가하는 게 좋음

```html
<div v-for="item in items" v-bind:key="item.id">
  <!-- content -->
</div>
```

## 배열 변경 감지

감시중인 배열의 변이 메소드를 래핑하며 뷰 갱신을 트리거함

래핑된 메소드

- push()
- pop()
- shift()
- unshift()
- splice()
- sort()
- reverse()

### 배열 대체

위의 변이 메소드는 호출된 원본 배열을 변경하지만 아래와 같은 메소드는 원본 배열을 변형하지 않고 항상 새 배열을 반환함

- filter()
- concat()
- slice()

이런 경우 Vue가 기존 DOM을 버리고 전체 목록을 리랜더링 할 것 같지만 다행히 Vue는 스마트한 휴리스틱을 실행하여 DOM 엘리먼트의 재사용을 극대화한다 그래서 일치하는 객체를 포함한 다른 배열을 대체하여 아주 효율적인 연산을 함!

### 주의

JS 한계 때문에 Vue가 배열이나 객체에서 발견하지 못하는 몇 가지 변경사항이 있다. 이후에 후술

## 필터링/정렬된 결과 표시하기

원본 데이터를 실제로 변경하지 않고 배열의 필터링/정렬된 버전을 표시해야 할 대가 있음 이 경우 computed 속성 사용

```html
<li v-for="n in evenNumbers">{{ n }}</li>

<script>
  data: {
    numbers: [ 1, 2, 3, 4, 5 ]
  },
  computed: {
    evenNumbers: function () {
      return this.numbers.filter(function (number) {
        return number % 2 === 0
      })
    }
  }
</script>
```

computed 속성을 실행할 수 없는 상황 (중첩된 `v-for` 루프 내부)에서는 다음 방법 가능

```html
<li v-for="n in even(numbers)">{{ n }}</li>

<script>
  data: {
    numbers: [ 1, 2, 3, 4, 5 ]
  },
  methods: {
    even: function (numbers) {
      return numbers.filter(function (number) {
        return number % 2 === 0
      })
    }
  }
</script>
```

## `v-for` 범위

v-for는 숫자 사용 가능

```html
<div>
  <span v-for="n in 10">{{ n }} </span>
</div>
```

### 템플릿

```html
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider" role="presentation"></li>
  </template>
</ul>
```

### `v-for` with `v-if`

이 두 가지를 한 번에 사용하는 것을 권장하지 않음. 자세한건 스타일 가이드 ㄱㄱ

동일한 노드에 두 가지 모두 있다면 `v-for`가 `v-if`보다 높은 우선순위를 가짐. 즉, `v-if`는 루프가 반복될 때마다 실행됨. 이는 일부 항목만 렌더링하는 경우에 유용함

```html
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo }}
</li>
```

위 방법 대신 실행을 조건부로 하는 것이 목적이라면 레퍼 엘리먼트 또는 템플릿 사용 권장

```html
<ul v-if="todos.length">
  <li v-for="todo in todos">
    {{ todo }}
  </li>
</ul>
<p v-else>No todos left!</p>
```
