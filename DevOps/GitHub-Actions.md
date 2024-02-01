# GitHub Actions
GitHub Actions는 CI/CD를 위한 도구이다.

GitHub Actions는 리포지토리에 특정 이벤트(event)가 발생했을 때나 주기적으로 미리 정의해 놓은 `workflow`를 실행시켜 원하는 작업을 자동으로 처리할 수 있다.

## GitHub Actions의 구성 요소
![Alt text](https://docs.github.com/assets/cb-25535/mw-1440/images/help/actions/overview-actions-simple.webp)

### Workflows
`workflow`는 <u>**하나 이상의 작업을 실행하는 설정가능한 자동화된 프로세스**</u>이다.

`workflow`는 리포지토리의 `.github/workflows` 경로에 위치한 YAML 파일로 정의할 수 있으며,  하나의 리포지토리에 여러 개의 `workflow`를 생성할 수 있다.

또한 각각의 `workflow`는 서로 다른 작업들을 수행할 수 있다.

예를 들어, 하나의 리포지토리에는  Pull Request에 대해 빌드하고 테스트하는 `workflow`를 가지거나 릴리스가 생성될 때 마다 애플리케이션을 배포하는 `workflow`를 가질 수 있다.

### Events
`event`는 `workflow`를 실행하게 만드는 <u>**리포지토리에서 발생하는 특정 활동**</u>이다. 

예를 들어, Pull Request를 생성하거나, 리포지토리에 커밋을 푸시하는 활동들이 있다.

```YAML
on:
    push:
        branches: [main]
```
 위와 같이 작성하게 되면, 리포지토리 `main` 브랜치에 `push` 이벤트가 발생할 때 마다 `workflow`를 실행한다.

 ```YAML
 on:
    schedule:
        - cron: "0 0 * * *"
 
 ```
 위와 같이 작성하게 되면,
 크론 표현식에 따라 정해진 시각에 `workflow`가 실행된다.

### Jobs
`job`은 <u>**동일한  `runner`에서 실행되는 `step`의 집합**</u>이다.

`step`은 커맨드(command)나 스크립트(script)가 될 수 있고 `action`이 될 수도 있다.

`step`들은 서로 종속적이고 순서대로 실행되는데, 각 `step`은 같은 `runner` 위에서 실행되기 때문에 현재 단계에서 다음 단계로 데이터를 공유할 수 있다.

기본적으로 모든 `job`은 의존 관계가 없기 때문에 동시에 실행된다.

만약 의존 관계를 설정한다면, `job`의 실행 순서를 제어할 수 있다.

```YAML
jobs:
    job1: # Job의 이름
        runs-on: ubuntu-latest # 실행 환경 (필수)
        steps:
            - uses: actions/checkout@v4
            - run: npm install
```
위와 같이 `workflow` 내에서 `jobs` 속성을 통해 `job`에 대한 내용을 정의할 수 있다.

`steps` 속성에서 작업의 순서를 정의할 수 있다.

`uses`는 `action`을 사용할 때 쓰이고, `run`은 커맨드나 스크립트를 사용할 때 쓰인다.

### Actions
`action`은 <u>**복잡하지만 자주 반복되는 작업을 수행하는 커스텀 애플리케이션**</u>이다. 

`action`는 하나의 리포지토리 내에서 `workflow` 간에서 공유를 할 수 있을 뿐 아니라, 공개 리포지토리를 통해 `action`을 공유하면 GitHub의 모든 리포지토리에서 사용이 가능하다.

### Runners
`runner`는 <u>**`workflow`를 실행하는 가상 머신**</u>이다.

각 `runner`는 한 번에 하나의 `job`을 실행할 수 있다.

GitHub는 `workflow`들을 실행할 수 있는 다양한 OS `runner`를 지원한다.                                                                                                       