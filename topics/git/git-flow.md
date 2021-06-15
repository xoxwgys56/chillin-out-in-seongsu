# Git flow

2021-06-16, [Dan](https://github.com/xoxwgys56)

> git flow가 무엇인지에 대해 다룹니다.

## Summary

### 다루지 않는 내용

- what is git
- git add
- git commit
- git merge
- git rebase
- html

### 다루는 내용

- git branch
- pull request (also called, merge request)
- git flow (main topic !)

## git flow 무엇인가?

git flow에 대해 다루기 앞서서 github flow를 살펴보겠습니다.  
github flow가 좀 더 단순한 형태이기 때문입니다.  
또한 우리는 여기서 git의 몇가지 명령에 대해서도 다룰 것 입니다.

> 이 챕터의 대부분의 내용은 아래의 url에 기반해 있습니다.
>
> https://guides.github.com/introduction/flow/

간단한 실습을 통해 어떻게 github flow가 동작하는지 알아보겠습니다.  
빈 저장소를 생성해 clone 하겠습니다. 처음 생성된 저장소엔 `main` 브랜치만 존재할 것 입니다.

> 이 문서는 github을 기준으로 합니다. gitlab의 경우 `master` 브랜치가 생성됩니다.  
> 왜 이름이 다른지에 관하여 [Git의 기본 브랜치를 master에서 main으로 변경하기](https://blog.outsider.ne.kr/1503) 글을 참고하면 도움이 될 것 입니다.

아래의 내용들은 제가 출력 내용을 보여드리기 위해 생성한 [저장소](https://github.com/xoxwgys56/gitflow-practice)의 실행 결과입니다.  
예제 프로젝트는 html로 구현한 프로젝트에 대해 다룹니다.  

### start from main branch

생성된 저장소에는 `main` 브랜치만 존재합니다. 일반적으로 `main` 브랜치는 언제나 배포하여 상용 가능한 버전이어야 합니다.  
이 예시에서는 chillin-out-seongsu를 소개하는 웹페이지를 만드려고 합니다.  

```shell
$ git branch

* main
(END)
```

미리 `main` 브랜치에 빈 html을 생성했습니다. `develop` 브랜치를 생성하고 해당 브랜치로 이동하겠습니다.

```shell
$ git checkout -b develop
```

브랜치를 이동해도 바뀌는 것은 없습니다. 같은 내용의 코드가 `main`(상용화 가능 버전) `develop`(개발 버전)으로 나뉘어져있을 뿐입니다.

### start develop with develop branch

`develop` 브랜치에 새로운 개발 사항을 적용해보겠습니다.

> 빈 html은 이쁘지 않으니, [materialize cdn](https://materializecss.com/getting-started.html)을 추가하고 또한 시각적으로 확인하기 위해 nav tag도 추가하겠습니다.  

개발이 적용된 사항을 커밋하고, `develop` 브랜치에 푸시합니다.

```shell
$ git add src
$ git commit
$ git push

fatal: 현재 브랜치 develop에 업스트림 브랜치가 없습니다.
현재 브랜치를 푸시하고 해당 리모트를 업스트림으로 지정하려면
다음과 같이 하십시오.

    git push --set-upstream origin develop

$ git push --set-upstream origin develop

# finished push develop branch with new commit !
```

### PR merge

이제 저장소 페이지로 가봅시다.

![gh pr request](./gh_pr_request.png)

이제 우리는 PR (Pull Request)를 만들 수 있습니다. 버튼을 눌러 PR을 생성합니다.  

> Pull Request는 무엇일까요? git merge 명령과 비슷하다고 생각하시면 됩니다.  
> git merge 명령과의 차이는 Pull Request는 로컬 환경에서 Merge하는 것이 아닙니다. 로컬 환경에서 Merge를 진행하게 된다면 누가 Merge를 했고, 코드는 검사되었는지 확인할 수 없을 것 입니다. (아마도?)  
> 하지만 Pull Request를 통해 Merge한다면, 코드를 리뷰받고 Merge된 기록을 commit이 아닌 형태로 남길 수 있습니다.

![gh pr open](./gh_pr_open.png)

사진에서 pull request의 몇가지 포인트를 화살표로 지정했습니다. 번호 순서대로 설명드리겠습니다. (번호.. 알아보시겠죠..?)

1. 우리는 `develop` 브랜치에서 `main` 브랜치로 Merge하고자 합니다. 비교 대상이 되는 compare=`develop`, Merge 결과가 남는 base는 `main` 브랜치입니다.
2. 제목과 내용이 있는데, 여기에 생성되는 기본 정보는 커밋 메세지에서 가져오는 정보를 기반으로 합니다. 제목으로 작성된 `feat: add materialze cdn`은 제가 작성한 커밋 메세지입니다.
3. 어떤 커밋들을 Pull Request에 포함시켰는지 다룹니다. 이 PR은 하나의 커밋만 포함되어 있네요.
4. 이 중 _Reviewers_에 대해서만 다루겠습니다. 지정된 reviewer에게 리뷰를 받기 위함입니다.

`PR`을 생성하면 아래와 같은 화면이 보입니다.

![gh pr merge](./gh_pr_merge.png)

> 이 저장소에는 저 혼자라 리뷰할 사람이 없군요.. 😿 리뷰 과정은 생략하겠습니다.

이제 `Merge pull request` 버튼을 눌러서 Merge합니다.

![gh pr after merge](./gh_pr_after_merge.png)

Merge를 하고 나면 생성한 `PR`은 `Merged`로 표기됩니다. 또한 Merge된 브랜치를 삭제할 것인지 물어봅니다. 이 예시에서는 삭제하지 않을 것 입니다.  




## 그래서 무엇인가?

[A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)이라는 [Vincent Driessen](https://nvie.com/about/)이 작성한 블로그에서 처음 소개된 개념이라고 알려져 있습니다.  
아래의 사진이 git flow를 나타낸 그림으로 유명합니다.
앞서 github flow를 먼저 다룬 이유는 `Vincent Driessen`가 권장하기 때문입니다.

> 그는 이렇게 말하고 있습니다.
>
> > I would suggest to adopt a much simpler workflow (like GitHub flow) instead of trying to shoehorn git-flow into your team.

![git flow](https://nvie.com/img/git-model@2x.png)

## 회사에서 어떻게 쓰고 있는가?

dev, test, production

---

## References

- [published issue](https://github.com/xoxwgys56/chillin-out-in-seongsu/issues/3)
- git flow
  - https://nvie.com/posts/a-successful-git-branching-model/ who mentioned
  - https://woowabros.github.io/experience/2017/10/30/baemin-mobile-git-branch-strategy.html
  - https://danielkummer.github.io/git-flow-cheatsheet/index.ko_KR.html
  - https://jeong-pro.tistory.com/196
  - https://guides.github.com/introduction/flow/
- example repo
  - https://github.com/xoxwgys56/gitflow-practice
- git review
  - https://github.com/im-d-team/Dev-Docs/issues/11
  - https://devlog-wjdrbs96.tistory.com/231