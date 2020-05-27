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

이제 `vm.fullName = 'John Doe'`를 실행하면 setter가 호출되고 `vm.firstName`과 `vm.lastName`이 그에 따라 업뎃됨

## watch

대부분 computed 속성이 더 적합하지만 사용자가 만든 watch가 필요한 경우가 있음. Vue는 `watch` 옵션을 통해 데이터 변경에 반응하는 보다 일반적인 방법을 제공함. 데이터 변경에 대한 응답으로 비동기식 또는 시간이 많이 소요되는 조작을 수행하려는 경우에 가장 유용함

```html
<div id="watch-example">
  <p>
    yes/no 질문을 물어보세요:
    <input v-model="question">
  </p>
  <p>{{ answer }}</p>
</div>

<script>
<script src="https://unpkg.com/axios@0.12.0/dist/axios.min.js"></script>
<script src="https://unpkg.com/lodash@4.13.1/lodash.min.js"></script>
<script>
var watchExampleVM = new Vue({
  el: '#watch-example',
  data: {
    question: '',
    answer: '질문을 하기 전까지는 대답할 수 없습니다.'
  },
  watch: {
    // 질문이 변경될 때 마다 이 기능이 실행됩니다.
    question: function (newQuestion) {
      this.answer = '입력을 기다리는 중...'
      this.getAnswer()
    }
  },
  methods: {
    // _.debounce는 lodash가 제공하는 기능으로
    // 특히 시간이 많이 소요되는 작업을 실행할 수 있는 빈도를 제한합니다.
    // 이 경우, 우리는 yesno.wtf/api 에 액세스 하는 빈도를 제한하고,
    // 사용자가 ajax요청을 하기 전에 타이핑을 완전히 마칠 때까지 기다리길 바랍니다.
    // _.debounce 함수(또는 이와 유사한 _.throttle)에 대한
    // 자세한 내용을 보려면 https://lodash.com/docs#debounce 를 방문하세요.
    getAnswer: _.debounce(
      function () {
        if (this.question.indexOf('?') === -1) {
          this.answer = '질문에는 일반적으로 물음표가 포함 됩니다. ;-)'
          return
        }
        this.answer = '생각중...'
        var vm = this
        axios.get('https://yesno.wtf/api')
          .then(function (response) {
            vm.answer = _.capitalize(response.data.answer)
          })
          .catch(function (error) {
            vm.answer = '에러! API 요청에 오류가 있습니다. ' + error
          })
      },
      // 사용자가 입력을 기다리는 시간(밀리세컨드) 입니다.
      500
    )
  }
})
</script>
</script>
```

watch 옵션을 사용하면 비동기 연산을 수행하고 우리가 그 연산을 얼마나 자주 수행하는지 제한하고 최종 응답을 얻을 때까지 중간 상태를 설정할 수 있음.
