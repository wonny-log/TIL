# Vue

## Install

### CDN

1. `index.html` 파일 생성
2. 다음과 같이 Vue 설치

```html
<!-- 개발버전, 도움되는 콘솔 경고를 포함. -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<!-- 상용버전, 속도와 용량이 최적화됨. -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

### Vue CLI

[Vue CLI Document](https://cli.vuejs.org/)

```cli
// Install
$ npm install -g @vue/cli

// Create a project
$ vue create first-project
```

## Hello Vue

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Hello Vue</title>
  </head>
  <body>
    <div id="app">
      {{ message }}
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue"></script>
    <script>
      var app = new Vue({
        el: "#app",
        data: {
          message: "Hello Vue",
        },
      });
    </script>
  </body>
</html>
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

```

```
