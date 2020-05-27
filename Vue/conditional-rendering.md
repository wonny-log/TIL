# 조건부 렌더링

## `v-if`, `v-else`

```html
<h1 v-if="ok">Yes</h1>
<h1 v-else>No</h1>
```

`v-else` 엘레먼트는 `v-if` 또는 `v-else-if` 엘리먼트 바로 뒤에 있어야 함

## `<template>`에 `v-if`을 갖는 조건부 그룹 만들기

하나 이상의 엘리먼트를 트랜지션 하기 위해서는 보이지 않는 레퍼 역할을 하는 `<template>` 엘리먼트를 사용하면 됨. 최종 렌더링 결과에서는 안보임

```html
<template v-if="ok">
  <h1>Title</h1>
  <h2>Sub Title</h2>
</template>
```

### `v-else-if`

```html
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```

### `key`를 이용한 재사용 가능한 엘리먼트 제어

효율적으로 렌더링하기 위해 처음부터 다시 렌더링하지 않고 재사용함

```html
<template v-if="loginType === 'username'">
  <label>사용자 이름</label>
  <input placeholder="사용자 이름을 입력하세요" />
</template>
<template v-else>
  <label>이메일</label>
  <input placeholder="이메일 주소를 입력하세요" />
</template>
```

위 코드에서 `loginType`을 바꾸어도 사용자가 이미 입력한 내용은 지워지지 않음. 두 템플릿 모두 같은 요소를 사용하므로 `<input>`은 대체 되지 않고 단지 `placeholder`만 변경됨

이 두 엘리먼트는 완전히 별개이므로 다시 사용하지 말라고 해줄 때 `key`를 유니크 값으로 추가

```html
<template v-if="loginType === 'username'">
  <label>사용자 이름</label>
  <input placeholder="사용자 이름을 입력하세요" key="username-input" />
</template>
<template v-else>
  <label>이메일</label>
  <input placeholder="이메일 주소를 입력하세요" key="email-input" />
</template>
```

`key`가 없는 `<label>` 엘리먼트의 경우 여전히 재사용됨

### `v-show`

```html
<h1 v-show="ok">안녕하세요!</h1>
```

`v-show`가 있는 엘리먼트는 항상 렌더링되고 DOM에 남아 있음. `v-show`는 단순히 엘리먼트에서 `display` CSS 속성을 토글함

> `v-show`는 `<template>` 구문을 지원하지 않으며 `v-else`와도 작동하지 않음

### `v-if` vs `v-show`

**`v-if`**

조건부 블럭 안의 이벤트 리스너와 자식 컴포넌트가 토글하는 동안 적절하게 제거되고 다시 만들어지기 때문에 진짜 조건부 렌더링임
게으르기 때문에 초기 렌더링에서 조건이 거짓이면 아무것도 안함. 조건 블록이 처음으로 참이 될 때까지 렌더링되지 않음

**`v-show`**

훨씬 단순. CSS 기반 토글만으로 초기 조건에 관계 없이 엘리먼트 항상 렌더링됨

`v-if`는 토글 비용이 높고 `v-show`는 초기 렌더링 비용이 높음. 자주 바꾸면 `v-show`, 런타임 시 조건이 바뀌지 않으면 `v-if` 권장

### `v-if` 와 `v-for`

`v-if`와 함께 사용하는 경우 `v-for`가 더 높은 우선순위를 가짐
