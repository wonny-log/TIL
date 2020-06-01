# ESLint

## What is ESLint?

JavaScript 문법 검사를 수행하고 잘못된 코드를 고쳐주는 도구입니다.

## 설치하기

[VSCode ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)에서 설치합니다.

혹은 `npm install eslint -g`로 설치합니다.

## 설정하기

자동으로 코드가 수정되도록 다음과 같이 설정해줍니다.

```json
"editor.codeActionsOnSave": {
    "source.fixAll": true
}
```

`eslint --init`를 실행하고 프로젝트 루트 디렉터리에 `.eslintrc.{js,yml,json}` 파일을 추가합니다. 이 파일 안에 몇 가지 규칙을 설정할 수 있습니다.

```json
{
  "rules": {
    "semi": ["error", "always"],
    "quotes": ["error", "double"]
  }
}
```

다음과 같이 다른 사람이 만든 규칙으로 설정할 수 있습니다.

```json
{
  "extends": "eslint:recommended"
}
```

---

# Reference

- [ESLint](https://eslint.org/docs/user-guide/getting-started)
