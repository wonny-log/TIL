# Prettier

# What is Prettier?

> An Opinionated code formatter

정해진 규칙에 따라 코드 스타일을 변환해주는 도구입니다. 기존 스타일링을 완전히 제거하고 정해진 규칙에 따라 코드를 재작성하는 방식으로 동작합니다.

# Why use Prettier?

큰 에너지나 시간을 들이지 않고 여러 개발자가 통일된 코드 스타일로 개발할 수 있습니다.

# How to use Prettier?

## Install

### yarn

```shell
yarn add prettier --dev --exact
# or globally
yarn global add prettier
```

### npm

```shell
$ npm install --save-dev --save-exact prettier
# or globally
$ npm install --global prettier
```

### npx

```shell
npx prettier@2.0.5 . --write
```

공식 문서에서는 새 버전에서 스타일이 변경될 수 있기 때문에 `package.json`에 특정 버전의 prettier를 설치하는 것을 권장합니다.

## 실행하기

```shell
prettier --write .
```

위 명령어를 실행하면 현재 디렉터리들과 하위 디렉터리들에 있는 모든 파일을 변경시켜줍니다.

## 설정하기

프로젝트 루트 경로에 `.prettierrc` 파일을 추가하여 옵션을 추가할 수 있습니다.

```json
{
  "semi": false,
  "overrides": [
    {
      "files": "*.test.js",
      "options": {
        "semi": true
      }
    },
    {
      "files": ["*.html", "legacy/**/*.js"],
      "options": {
        "tabWidth": 4
      }
    }
  ]
}
```

## Ignore

몇 가지 설정을 통해 Prettier 적용을 제외시킬 수 있습니다.

### 파일 단위

파일 단위로 prettier 적용을 제외하고 싶다면 프로젝트 루트 경로에 `.prettierignore` 파일을 혹은 `--ignore-path` CLI 옵션에 제외할 파일을 설정할 수 있습니다.

### JavaScript

자바스크립트에서는 `// prettier-ignore` 주석을 통해 AST의 다음 노드를 제외시킬 수 있습니다.

# VS Code에 설치하기

VS Code Extension인 [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)를 설치할 수 있습니다.

## 실행하기

1. CMD + Shift + P -> Format Document
   OR
1. Select the text you want to Prettify
1. CMD + Shift + P -> Format Selection

## 저장 시 자동으로 실행시키기

매번 수동으로 실행하기 귀찮다면 VS Code 설정을 통해 저장할 때마다 자동으로 실행되도록 설정할 수 있습니다.

```json
"editor.formatOnSave": true,
// Enable per-language
"[javascript]": {
    "editor.formatOnSave": true
}
```

---

# Reference

- [Prettier 공식 홈페이지](https://prettier.io/)
