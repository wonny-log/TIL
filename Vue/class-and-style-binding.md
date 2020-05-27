# Vue Class and Style binding

## HTML 클래스 바인딩

### 객체 구문

**클래스를 동적으로 토글하기**

```html
<div v-bind:class="{ active: isActive }"></div>
```

위 구문은 `active` 클래스 존재 여부가 데이터 속성 `isActive`의 속성에 의해 결정됨

**여러 클래스 및 일반 `class`와 공존 가능**

```html
<div
  class="static"
  v-bind:class="{ active: isActive, 'text-danger': hasError }"
></div>

<script>
  data: {
  isActive: true,
  hasError: false
  }
</script>

<!-- Result: <div class="static active"></div> -->
```

바인딩 된 객체는 인라인일 필요 없이 다음과 같이도 가능하다

```html
<div v-bind:class="classObject"></div>

<script>
  data: {
      classObject: {
          active: true,
          'text-danger': false
      }
  }
</script>
```

computed 속성에도 바인딩할 수 있음

```html
<div v-bind:class="classObject"></div>

<script>
  data: {
    active: true,
    'text-danger': false
  },
  computed: {
      classObject: function() {
          return {
              active: this.isActive && !this.error,
              'text-danger': this.error && this.error.type === 'fatal'
          }
      }
  }
</script>
```

### 배열 구문

```html
<div v-bind:class="[activeClass, errorClass]"></div>

<script>
  data: {
    activeClass: 'active',
    errorClass: 'text-danger'
  }
</script>

<!-- Result: <div class="active text-danger"></div> -->
```

조건부 토글은 삼항 연산자

```html
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
```

여러 조건부 클래스가 있으면 코드가 복잡해지니까 배열 구문 내에서 객체 구문 사용 가능

```html
<div v-bind:class="[{ active: isActive }, errorClass]"></div>
```

## 인라인 스타일 바인딩

### 객체 구문

```html
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>

<script>
  data: {
    activeColor: 'red',
    fontSize: 30
  }
</script>
```

스타일 객체 직접 바인딩

```html
<div v-bind:style="styleObject"></div>

<script>
  data: {
    styleObject: {
      color: 'red',
      fontSize: '13px'
    }
  }
</script>
```

### 배열 구문

```html
<div v-bind:style="[baseStyles, overridingStyles]"></div>
```

### 자동 접두사

`v-bind:style`에 브라우저 벤더 접두어가 필요한 CSS 속성 (예: transform)을 사용하면 Vue는 자동으로 해당 접두어를 감지하여 스타일을 적용합니다

### 다중 값 제공

```html
<div v-bind:style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
```

브라우저가 지원하는 배열의 마지막 값만 렌더링합니다. 이 예제에서는 flexbox의 접두어가 붙지않은 버전을 지원하는 브라우저에 대해 display : flex를 렌더링합니다.
