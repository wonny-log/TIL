# Prettier Intergrate with Linters


기존 린트 툴을 사용하여 Prettier를 워크플로우에 통합할 수 있습니다. 우리가 이전에 작성한 [Prettier와 Linter 비교하기](https://prettier.io/docs/en/comparison.html) 글에서 요약한 것처럼 Prettier를 코드 포매팅 문제에 사용하고 Linter를 코드 퀄리티 문제에 사용할 수 있습니다.

통합하고자 하는 린트 툴이 무엇이든 과정은 대체로 비슷합니다. 우선 Prettier가 코드를 포맷하려는 규칙과 충돌할 수 있는 린터에 있는 기존 포맷팅 규칙을 비활성화하세요. 그러면 Prettier를 사용하여 파일을 포맷하기 위해 린트 툴에 익스텐션을 추가할 수 있습니다. 그러면 파일을 포맷하거 린터를 동작시키고 별도의 단계로 Prettier를 실행시킬 때 명령어 하나만 필요하거나 각 과정에서 린터를 동작시킬 수 있습니다.

여기있는 방법은 이미 `prettier`를 `devDependencies`에 설치했음을 가정하고 쓰여졌습니다.

# ESLint

## 포맷팅 규칙 비활성화

`eslint-config-prettier`는 Prettier와 충돌되는 규칙들을 비활성화하는 설정입니다. `devDependencies`에 추가하고 `eslintrc`에서 이를 사용하도록 설정하세요. `extends` 배열 마지막에 놓아야 다른 설정을 오버라이드합니다.

```shell
$ yarn add --dev eslint-config-prettier
```

그 다음 `.eslintrc.json` 에서는:

```json
{
    "extends": ["prettier"]
}
```

## Prettier를 실행하기 위해 ESLint 사용하기

`eslint-plugin-prettier`는 Prettier를 사용하여 내용을 포맷하는 규칙을 추가하는 플러그인입니다. `devDependencies`에 추가하면 플러그인과 규칙을 활성화할 수 있습니다.

```shell
$ yarn add --dev eslint-plugin-prettier
```

그 다음 `.eslintrc.json` 에서는:

```json
{
    "plugins": ["prettier"],
    "rules": {
        "prettier/prettier": "error"
    }
}
```

## 권장하는 설정

`eslint-plugin-prettier`는 `eslint-plugin-prettier`와 `eslint-config-prettier`를 하나의 단계로 설정하기를 권장합니다. `eslint-plugin-prettier`와 `eslint-config-prettier`를 개발자 디펜던시에 추가하고 권장하는 설정을 확장하세요.

```shell
$ yarn add --dev eslint-config-prettier eslint-plugin-prettier
```

그 다음 `.eslintrc.json` 에서는:

```json
{
    "extends": ["plugin:prettier/recommended"]
}
```