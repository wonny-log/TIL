# computed와 watch

## computed 속성

너무 많은 연산을 템플릿 안에서 하면 코드가 비대해지고 유지보수가 어려우므로 복잡한 로직의 경우 반드시 computed 속성을 사용해야 함

```html
<div id="app">
  <p>origin message: "{{ message }}"</p>
  <p>reverse message: "{{ reversedMessage }}"</p>
</div>

<script>
  var app = new Vue({
    el: "#app",
    data: {
      message: "Hello Vue",
    },
    computed: {
      reversedMessage: function () {
        return this.message.split("").reverse().join("");
      },
    },
  });
</script>
```

일반 속성처럼 computed 속성에도 템플릿에서 데이터 바인딩할 수 있음
Vue는 `vm.reversedMessage`가 `mv.message`에 의존하는 것을 알고 있으므로 `vm.message`가 바뀔 때 `vm.reversedMessage`에 의존하는 바인딩을 모두 업데이트할 것이다. 젤 중요한 것은 우리가 선언적으로 의존 관계를 만들었다는 것이다. computed 속성의 getter 함수는 사이드 이펙트가 없어서 코드를 테스트하거나 이해하기 쉬움

**computed 속성 vs 메소드**

표현식에서 메소드를 호출하여 같은 결과를 얻을 수도 있음

```html
<p>뒤집힌 메시지: "{{ reversedMessage() }}"</p>

<script>
  methods: {
    reversedMessage: function () {
      return this.message.split('').reverse().join('')
    }
  }
</script>
```

결과물은 동일하나 computed 속성은 종속 대상을 따라 저장(캐싱)됨. computed 속성은 해당 속성이 종속된 대상이 변경될 때만 함수를 실행함. 즉 `message`가 변경되지 않는 한 `reversedMessage`를 여러 번 요청해도 계싼을 다시 하지 않고 계산되어 있던 결과를 즉시 반환함

또한 `Date.now()` 처럼 아무 곳에도 의존하지 않는 computed 속성의 경우 절대로 업데이트되지 않는다는 뜻임

```js
computed: {
  now: function() {
    return Date.now()
  }
}
```

이에 비해 메소드를 호출하면 렌더링을 다시 할 때마다 항상 함수를 실행함

**computed 속성 vs watch 속성**

Vue 인스턴스의 데이터 변경을 관찰하고 이에 반응하는 보다 일반적인 watch 속성을 제공함

watch 속성은 감시할 데이터를 지정하고 그 데이터가 바뀌면 이런 함수를 실행하라는 방식으로 소프트웨어 공학에서 이야기하는 명령형 프로그래밍 방식. computed 속성은 계산해야 하는 목표 데이터를 정의하는 방식으로 소프트웨어 공학에서 이야기하는 선언형 프로그래밍 방식

```html
<div id="demo">{{ fullName }}</div>

<script>
  var vm = new Vue({
    el: "#demo",
    data: {
      firstName: "Foo",
      lastName: "Bar",
      fullName: "Foo Bar",
    },
    watch: {
      firstName: function (val) {
        this.fullName = val + " " + this.lastName;
      },
      lastName: function (val) {
        this.fullName = this.firstName + " " + val;
      },
    },
  });
</script>
```

```js
var vm = new Vue({
  el: "#demo",
  data: {
    firstName: "Foo",
    lastName: "Bar",
  },
  computed: {
    fullName: function () {
      return this.firstName + " " + this.lastName;
    },
  },
});
```

### setter 함수

computed 속성은 기본적으로 getter 함수만 가지고 있지만 필요한 겨우 setter 함수를 만들어 쓸 수 있음

```js
// ...
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
// ...
```
