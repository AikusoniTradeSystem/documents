# 브랜치 관리 전략
- 기본적인 기능 개발이 완료되어 최초 배포버전이 만들어지면 [git flow](https://techblog.woowahan.com/2553/) 또는 [github flow](https://docs.github.com/ko/get-started/using-github/github-flow)와 유사한 형태로 진행합니다.
### 필수 브랜치
- main : 메인 브랜치
- develop : 개발 브랜치
### 선택 브랜치
작업에 따라 유연하게 작성하나 다음과 같이 알아 볼 수 있게 명명해야 합니다.
- feature : 기능 개발 브랜치 (예: feature/기능명_이슈번호_작업시작날짜)
- fix : 기존 기능에 대한 버그 수정 브랜치 (예: fix/기능명_이슈번호_작업시작날짜)
