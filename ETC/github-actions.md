# GitHub Actions

깃헙 레파지토리 내에서 소프트웨어 개발 개발 단계를 자동화할 수 있도록 도와주는 도구이다. 코드나 콜라보레이터, 풀 리퀘스트, 이슈 등이 추가/변경될 때 무엇을 수행할지 설정할 수 있어서 CI/CD 등을 구축할 수 있다.

## Concept

### workflow

```yaml
name: Greet Everyone

# 트리거 설정
on: [push]

# 하나 이상의 잡으로 구성되어야 한다
jobs:
  build:
    name: Greeting
    runs-on: ubuntu-latest
    steps:
      - name: Hello world
        uses: actions/hello-world-javascript-action@v1
        with:
          who-to-greet: "Mona the Octocat"
        id: hello
      - name: Echo the greeting's time
        run: echo 'The time was ${{ steps.hello.outputs.time }}.'
```

- 소프트웨어 개발 단계를 자동화하는 프로세스로 하나 이상의 job으로 구성된다.
- 이벤트에 의해 트리거되어 실행된다.
- YAML 문법을 사용한다.
- 레파지토리의 `.github/workflows` 디렉터리에 저장해야 한다.

### event

- 워크플로우를 트리거하는 특정 활동이나 규칙이다. GitHub의 특정 활동이나 예약된 시간, 외부 이벤트가 있다.

```yaml
on: push

# 여러 이벤트로 트리거를 설정해주고 싶을 때
on: [push, pull_request]

# 특정 브랜치에만 트리거를 설정해주고 싶을 때
on:
  push:
    branches:
      - master
  pull_request:
    branches:
      - master

# 특정 타입에만 트리거를 설정해주고 싶을 때
on:
  release:
    types:
      - created

# 파일 경로에 따라 트리거를 설정해주고 싶을 때
on:
  push:
    paths:
      - 'test/*'

# 수동 트리거를 설정해주고 싶을 때
on:
  workflow_dispatch:
    inputs:
      name:
        description: 'Person to greet'
        required: true
        default: 'Mona the Octocat'
```

### job

```yaml
jobs:
  my_first_job:
    name: My first job
  my_second_job:
    name: My second job
```

- 하나 이상의 job으로 워크플로우가 구성된다.
- 기본적으로 병렬적으로 실행된다.
- `needs` 키워드를 사용하여 특정 jobs이 끝난 후 수행하도록 설정할 수 있다.

### step

- 여러 task의 집합이다.
- 명령어를 실행시키거나(run) 작업을 설정하고(uses) action을 실행시킬 수 있다.
- 각 step은 runner 환경에서 동작한다.

### action

- 재사용 가능한 코드 묶음이다.
- 직접 구현할 수도 있고 [이미 구현되어 공유되는 것](https://github.com/marketplace?type=actions)을 사용할 수도 있다.

### runner

```yaml
runs-on: ubuntu-latest
```

- 워크플로우의 job이 실행되는 곳이다.
- GitHub이 호스팅해주는 것과 직접 호스팅하는 runner 중 선택할 수 있다.
