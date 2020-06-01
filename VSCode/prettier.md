# Prettier

## What it Prettier?

> An Opinionated code formatter.

기존의 스타일을 전부 지우고 정해진 스타일에 맞춰 코드를 변경하는 코드 포매터입니다. 협업하는 개발자들이 시간과 에너지를 들이지 않고도 동일한 스타일의 코드를 유지할 수 있도록 도와줍니다.

## 설치하기

[VS Code extension](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)에서 설치합니다. 설치가 완료되면 `ctrl` + `commnand` + `P`를 눌러서 파일이나 선택한 코드 스타일을 포매팅할 수 있습니다.

매번 수동으로 포맷하기 귀찮은 경우 파일을 저장할 때 자동으로 포맷팅하도록 설정할 수도 있습니다. VS Code 설정 화면에서 다음과 같이 설정합니다.

```json
{
  // Set the default
  "editor.formatOnSave": false,
  // Enable per-language
  "[markdown]": {
    "editor.formatOnSave": true
  }
}
```

## 설정하기

프로젝트 루트 디렉터리에 `.prettierrc` 파일을 추가하여 설정할 수 있습니다.

```json
{
  "trailingComma": "es5",
  "tabWidth": 4,
  "semi": false,
  "singleQuote": true
}
```

---

# Reference

- [How to use Prettier in VS Code](https://www.robinwieruch.de/how-to-use-prettier-vscode) by Robin Wieruch
