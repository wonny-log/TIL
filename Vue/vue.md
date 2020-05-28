# Vue

## Install

### `<script>`에 직접 설치하기

이 방법으로 설치하는 경우 `Vue`가 전역 변수로 등록됩니다.

[다운로드 링크](https://vuejs.org/v2/guide/installation.html#Direct-lt-script-gt-Include)

개발 중에는 일반적인 실수에 대한 경고를 받아볼 수 있도록 개발 버전을 사용해야 합니다.

### CDN

```html
<!-- 프토로타이핑이나 학습이 목적인 경우 아래 CDN 사용, 최신 버전을 사용하게 됨 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<!-- 프로덕션의 경우, 특정 버전을 명시적으로 지정하여 새로운 버전으로 인한 사이드 이펙트 방지하는 것이 좋음 -->
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.11"></script>

<!-- 네이티브 ES 모듈을 사용하는 경우, ES 모듈 호환 빌드 -->
<script type="module">
  import Vue from "https://cdn.jsdelivr.net/npm/vue@2.6.11/dist/vue.esm.browser.js";
</script>
```

### NPM

대규모 애플리케이션의 경우에는 NPM로 설치할 것을 권장합니다. Webpack이나 Browserify와 같은 모듈 번들러와 궁합이 좋습니다. 모듈 번들러를 활용하여 `.vue` 확장자를 가진 싱글 파일 컴포넌트를 생성하는 도구도 제공합니다.

```shell
$ npm install vue
```

### CLI

SPA를 빠르게 구축할 수 있는 [공식 CLI](https://github.com/vuejs/vue-cli)를 제공합니다. 모던 프론트엔드 워크플로우를 위해 사전 구성된 빌드 세팅을 제공합니다. 몇 분 안에 핫 리로드, 저장 시 린트 체크, 프로덕션 준비가된 빌드를 시작하고 실행할 수 있습니다.

[Vue CLI Document](https://cli.vuejs.org/)

```cli
// Install
$ npm install -g @vue/cli

// Create a project
$ vue create first-project
```

만일 Node.js 기반의 빌드 도구에 대한 사전 지식이 없다면 CLI 대신 [이 가이드](https://vuejs.org/v2/guide/)를 추천합니다.

### 체험하기

Vue를 빠르고 쉽게 체험해보기 위한 두 가지 방법이 있습니다.

- [codesandbox Vue 프로젝트](https://codesandbox.io/s/github/vuejs/vuejs.org/tree/master/src/v2/examples/vue-20-hello-world)
- `index.html` 파일 생성하여 다음 코드 추가하기 (참고: [`index.html`](https://github.com/vuejs/vuejs.org/blob/master/src/v2/examples/vue-20-hello-world/index.html))

```html
<!-- 개발 버전, 유용한 콘솔 경고를 포함 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
or:

<!-- 프로덕션 버전, 크기와 속도가 최적화됨 -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

## 조건문

```html
<div id="pratice-if">
  <p v-if="seen">Now you see me</p>
</div>

<script>
  var practiceIf = new Vue({
    el: "#pratice-if",
    data: {
      seen: true,
    },
  });
</script>
```

## for문

```html
<div id="practice-for">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>

<script>
  var practiceFor = new Vue({
    el: "#practice-for",
    data: {
      todos: [
        { text: "Learn JavaScript" },
        { text: "Learn Vue" },
        { text: "Build Something Awesome" },
      ],
    },
  });
</script>
```

## 사용자 입력 핸들링

### 메소드 호출: `v-on`

```html
<div id="practice-model">
  <p>{{ message }}</p>
  <input v-model="message" />
</div>

<script>
  var practiceMethod = new Vue({
    el: "#practice-method",
    data: {
      message: "Hello Vue",
    },
    methods: {
      reverseMessage: function () {
        this.message = this.message.split("").reverse().join("");
      },
    },
  });
</script>
```

### 데이터 양방향 바인딩: `v-model`

```html
<div id="practice-model">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Reserve Message</button>
</div>

<script>
  var practiceModel = new Vue({
    el: "#practice-model",
    data: {
      message: "Hello Vue",
    },
  });
</script>
```

## 컴포넌트

### 컴포넌트 생성

```html
<div id="app">
  <ol>
    <todo-item></todo-item>
  </ol>
</div>

<script>
  Vue.component("todo-item", {
    template: "<li>This is a Todo</li>",
  });

  var app = new Vue({
    el: "#app",
  });
</script>
```

### prop

```html
<div id="app">
  <ol>
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id"
    ></todo-item>
  </ol>
</div>

<script>
  Vue.component("todo-item", {
    props: ["todo"],
    template: "<li>{{ todo.text }}</li>",
  });

  var app = new Vue({
    el: "#app",
    data: {
      groceryList: [
        { id: 0, text: "Vegetables" },
        { id: 1, text: "Cheese" },
        { id: 2, text: "Whateever else humans are supposed to eat" },
      ],
    },
  });
</script>
```
