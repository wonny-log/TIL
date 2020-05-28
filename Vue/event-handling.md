# Vue Event Handling

## 이벤트 리스닝

```html
<div id="example-1">
  <button v-on:click="counter += 1">Add 1</button>
  <p>위 버튼을 클릭한 횟수는 {{ counter }} 번 입니다.</p>
</div>

<script>
  var example1 = new Vue({
    el: "#example-1",
    data: {
      counter: 0,
    },
  });
</script>
```

## 여러 이벤트 핸들러 로직은 복잡하므로 js를 `v-on` 속성 값으로 보관하는 것은 간단하지 않기에 `v-on`이 호출하고자 하는 메소드의 이름을 받음

```html
<div id="example-2">
  <!-- `greet`는 메소드 이름으로 아래에 정의되어 있습니다 -->
  <button v-on:click="greet">Greet</button>
</div>

<script>
  var example2 = new Vue({
    el: "#example-2",
    data: {
      name: "Vue.js",
    },
    // 메소드는 `methods` 객체 안에 정의합니다
    methods: {
      greet: function (event) {
        // 메소드 안에서 사용하는 `this` 는 Vue 인스턴스를 가리킵니다
        alert("Hello " + this.name + "!");
        // `event` 는 네이티브 DOM 이벤트입니다
        if (event) {
          alert(event.target.tagName);
        }
      },
    },
  });

  // 또한 JavaScript를 이용해서 메소드를 호출할 수 있습니다.
  example2.greet(); // => 'Hello Vue.js!'
</script>
```
