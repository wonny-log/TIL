# Vue Template

## Interpolation

### 문자열

데이터 바인딩의 가장 기본 형태는 Mustache 구문(이중 중괄호)를 사용한 텍스트 보간임

```html
<span>Message: {{ message }}</span>
```

`v-once` 디렉티브를 사용하여 데이터 변경 시 업데이트 되지 않는 일회성 보간을 수행할 수 있지만, 같은 노드의 바인딩에도 영향을 미치므로 주의해야 함

```html
<span v-once>This will never change: {{ message }}</span>
```

### 원시 HTML

Mustaches 는 HTML이 아닌 일반 텍스트로 데이터를 해석하므로 실제 HTML을 출력하려면 `v-html` 디렉티브를 사용해야 함

```html
<p>Using mustaches: {{ rawHtml }}</p>
<p>Using v-html directive: <span> v-html="rawHtml"></span></p>
```

`span`의 내용은 `rawHtml`로 대체되고 데이터 바인딩은 무시됨

Vue는 문자열 기반 템플릿 엔진이 아니기 때문에 `v-html`을 이용해 템플릿을 사용할 수 없음. 이와 달리 컴포넌트는 UI 재사용 및 구성을 위한 기본 단위로 사용하는 것을 추천함

### 속성

Mustaches는 HTML 속성에서 사용할 수 없고, 대신 `v-bind` 디렉티브를 사용해야 함

```html
<div v-bind:id="dynamicId"></div>
```

boolean 속성 사용 시 단순히 `true`인 경우 `v-bind`는 조금 다르게 동작함

```html
<button v-bind:disabled="isButtonDisabled">Button</button>
```

`isButtonDisabled`가 `null`, `undefined` 또는 `false`의 값을 가지면 `disabled` 속성은 렌더링 된 `<button>` 엘리먼트에 포함되지 않음

### JavaScript 표현식 사용

Vue는 모든 데이터 바인딩 내에서 JavaScript 표현식의 모든 기능을 지원함

```html
{{ number + 1 }} {{ ok ? 'YES' : 'NO' }} {{ message.split('').reverse().join('')
}}
<div v-bind:id="'list-' + id'"></div>
```

이 표현식은 Vue 인스턴스 데이터 범위 내에서 JavaScript로 계산됨

한가지 제한사항은 각 바인딩에 하나의 단일 표현식만 포함될 수 있으므로 아래처럼 작성하면 안됨

```html
<!-- 아래는 구문이지 표현식이 아님 -->
{{ var a = 1 }}

<!-- 조건문은 작동하지 않음. 삼항 연산자를 사용해야 함 -->
{{ if (ok) { return message } }}
```

템플릿 표현식은 샌드박스 처리되며 `Math`와 `Date` 같은 전역으로 사용 가능한 것에만 접근할 수 있음. 템플릿 표현식에서 사용자 정의 전역에 엑세스 하지 않아야 함

## 디렉티브

`v-` 접두사가 있는 특수 속성임. 디렉티브 속성값은 단일 JavaScript 표현식이 됨 (`v-for`은 예외)

디렉티브 역할은 표현식의 값이 변경될 때 사이드이펙트를 반응적으로 DOM에 적용하는 것임

```html
<p v-id="seen">Now you see me</p>
```

### Argument

일부 디렉티브는 콜론으로 표시되는 전달인자(argument)를 사용할 수 있음

`v-bind` 디렉티브는 반응적으로 HTML 속성을 갱신하는데 사용됨

```html
<a v-bind:href="url">...</a>
```

여기서 `href`은 전달인자로 엘리먼트의 `href` 속성을 표현식 `url`의 값에 바인드하는 `v-bind` 디렉티브에 알려줍니다.

### 동적 전달인자

JavaScript 표현식을 대괄호로 묶어 디렉티브의 아규먼트로 사용하는 것도 가능해짐

```html
<a v-bind:[attributeName]="url">...</a>
```

여기서 `attributeName`은 JavaScript 형식으로 동적 변환되어 그 변환 결과가 전달인자의 최종적인 밸류로 사용됨. 가령 Vue 인스턴스에 `"href"`라는 값을 가진 `attributeName` 데이터 속성을 가진 경우 이 바인딩은 `v-bind:href`와 동등함

**제약사항**

- 값의 제약: 동적 전달인자는 `null`을 제외하고는 문자열로 변환될 것으로 예상함. 특수 값인 `null`은 명시적으로 바인딩을 제거하는데 사용되고 그 외의 경우 문자열이 아닌 값은 경고를 출력함
- 형식의 제약: 스페이스와 따옴표같은 몇몇 문자는 HTML의 속성명으로 적합하지 않음.

```html
<a v-bind:['foo' + bar]="value"> ... </a>
```

이를 피하는 방법은, 스페이스나 따옴표를 포함하지 않는 형식을 사용하거나 복잡한 표현식을 계산된 속성(computed)으로 대체하는 것이다. in-DOM 템플릿을 사용할 때에는 (템플릿이 HTML 파일에 직접 쓰여진 경우) 브라우저가 모든 속성명을 소문자로 만드는 관계로 대문자의 사용을 피하는 것이 좋음

```html
<a v-bind:[someAttr]="value"> ... </a>
```

### 수식어

수식어는 점으로 표시되는 특수 접미사로 디렉티브를 특별한 방법으로 바인딩 해야 함을 나타낸다. 예를 들어 `.prevent` 수식어는 트리거된 이벤트에서 `event.preventDefault()`를 호출하도록 `v-on` 디렉티브에게 알려줌

```html
<form v-on:submit.prevent="onSubmit">...</form>
```

## 약어

`v-` 접두사는 템플릿의 Vue 특정 속성을 식별하기 위한 시각적인 신호 역할을 함. 대체로 유용하지만 장황하다고 느껴질 수 있음. 특히 Vue가 모든 ㅌ메플릿을 관리하는 SPA를 만들 때 `v-` 접두어의 필요성이 떨어지므로 가장 자주 사용하는 `v-bind` 와 `v-on`에 대해 약어를 제공

```html
<a v-bind:href="url"> ... </a>
<a :href="url"> ... </a>
<a :[key]="url"> ... </a>

<a v-on:click="doSomething"> ... </a>
<a @click="doSomething"> ... </a>
<a @[event]="doSomething"> ... </a>
```
