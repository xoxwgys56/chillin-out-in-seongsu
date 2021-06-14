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

아래의 내용은 제가 출력 내용을 보여드리기 위해 생성한 [저장소](https://github.com/xoxwgys56/gitflow-practice)의 실행 결과입니다.

```shell
git branch
```

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
- https://woowabros.github.io/experience/2017/10/30/baemin-mobile-git-branch-strategy.html
- https://nvie.com/posts/a-successful-git-branching-model/
- https://danielkummer.github.io/git-flow-cheatsheet/index.ko_KR.html
- https://jeong-pro.tistory.com/196
- https://guides.github.com/introduction/flow/
- https://github.com/xoxwgys56/gitflow-practice
