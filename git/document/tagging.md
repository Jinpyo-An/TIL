# 2.6 태그

태그는 보통 릴리즈(공유)할 때 사용

태그를 조회하고 생성하는 법과 태그 종류를 설명

## 태그 조회하기

`git tag` 명령으로 이미 만들어진 태그가 있는지 확인

(-l, --list는 옵션)

```tsx
$ git tag
v0.1
v1.3
```

이 명령은 알파벳 순서로 태그를 보여준다.(순서는 별로 중요하지 않다.)

검색 패턴을 사용해 태그 검색

- Git 소스 저장소는 500여 개의 태그가 있다.

`ex` 1.8.5 버전의 태그들만 검색

```tsx
$ git tag -l "v1.8.5*"
v1.8.5
v1.8.5-rc0
v1.8.5-rc1
v1.8.5-rc2
v1.8.5-rc3
v1.8.5.1
v1.8.5.2
v1.8.5.3
v1.8.5.4
v1.8.5.5
```

**Note**

와일드카드를 사용하여 Tag 리스트를 확인하려면 `-l, --list` 옵션을 지정해줘야 한다.

## 태그 붙이기

Git 태그에는 2가지 종류의 태그가 있다.

- Lightweight 태그
    
    브랜치와 비슷하지만 브랜치처럼 가리키는 지점을 최신 커밋으로 이동시키지 않는다.
    
    → 단순히 특정 커밋에 대한 포인터
    
- **Annotated 태그**
    
    Git 데이터베이스에 태그를 만든 사람 이름, 이메일과 태그를 만든 날짜, 태그 메시지를 저장
    
    GPG(GNU Privacy Guard)로 서명할 수도 있다.
    
    일반적으로 Annotated 태그를 만들어 이 모든 정보를 사용할 수 있도록 하는 것이 좋다.
    
    `but` 임시로 생성한 태그이거나 정보를 유지할 필요가 없는 경우는 Lightweight 태그를 사용할 수 있다.
    

## Annotated 태그

Annotated 태그를 만드는 방법

tag 명령을 실행할 때, `-a` 옵션을 추가

```tsx
$ git tag -a v1.4 -m "my version 1.4"
$ git tag
v0.1
v1.3
v1.4
```

`-m` 옵션으로 태그를 지정할 때 메시지를 함께 저장할 수 있다.

- 메시지를 입력하지 않으면 Git은 편집기를 실행시킨다.

`git show` 명령으로 태그 정보와 커밋 정보를 모두 확인

```tsx
$ git show v1.4
tag v1.4
Tagger: Ben Straub <ben@straub.cc>
Date:   Sat May 3 20:19:12 2014 -0700

my version 1.4

commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    changed the version number
```

커밋 정보를 보여주기 전에, 태그를 만든 사람이 누구인지, 태그를 언제 만들었는지, 그리고 태그 메시지가 무엇인지 보여준다.

## Lightweight 태그

Lightweight 태그는 기본적으로 파일에 커밋 체크섬을 기록할 뿐. 다른 정보 저장X

- `-a, -s, -m` 옵션을 사용하지 않는다. 이름만 달아줄 뿐

```tsx
$ git tag v1.4-lw
$ git tag
v0.1
v1.3
v1.4
v1.4-lw
v1.5
```

git show를 실행하면 태그 정보를 확인할 수 없다.

이 명령은 단지 커밋 정보만을 보여준다.

```tsx
$ git show v1.4-lw
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    changed the version number
```

## 나중에 태그하기

예전 커밋에 대해 태그하기

커밋 히스토리가 아래와 같다고 가정

```tsx
$ git log --pretty=oneline
15027957951b64cf874c3557a0f3547bd83b3ff6 Merge branch 'experiment'
a6b4c97498bd301d84096da251c98a07c7723e65 beginning write support
0d52aaab4479697da7686c15f77a3d64d9165190 one more thing
6d52a271eda8725415634dd79daabbc4d9b6008e Merge branch 'experiment'
0b7434d86859cc7b8c3d5e1dddfed66ff742fcbc added a commit function
4682c3261057305bdd616e23b64b0857d832627b added a todo file
166ae0c4d3f420721acbb115cc33848dfcc2121a started write support
9fceb02d0ae598e95dc970b74767f19372d61af8 updated rakefile
964f16d36dfccde844893cac5b347e7b3d44abbc commit the todo
8a5cbc430f1a9c3d00faaeffd07798508422908a updated readme
```

“updated rakefile” 커밋을 v1.2로 태그하지 못했다고 해도 나중에 태그를 붙일 수 있다.

특정 커밋에 태그

→ 명령의 끝에 커밋 체크섬을 명시

```tsx
$ git tag -a v1.2 9fceb02
```

만든 태그 확인

```tsx
$ git tag
v0.1
v1.2
v1.3
v1.4
v1.4-lw
v1.5

$ git show v1.2
tag v1.2
Tagger: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Feb 9 15:32:16 2009 -0800

version 1.2
commit 9fceb02d0ae598e95dc970b74767f19372d61af8
Author: Magnus Chacon <mchacon@gee-mail.com>
Date:   Sun Apr 27 20:43:35 2008 -0700

    updated rakefile
...
```

## 태그 공유하기

`git push`는 자동으로 서버에 태그를 전송하지 않는다.

- 로컬에 태그를 만들었으면 서버에 별도로 Push 해야 함

`git push origin <태그 이름>`

```tsx
$ git push origin v1.5
Counting objects: 14, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (12/12), done.
Writing objects: 100% (14/14), 2.05 KiB | 0 bytes/s, done.
Total 14 (delta 3), reused 0 (delta 0)
To git@github.com:schacon/simplegit.git
 * [new tag]         v1.5 -> v1.5
```

한 번에 태그를 여러 개 Push

→ `--tags` 옵션을 추가해 `git push` 명령 실행

→ 리모트 서버에 없는 태그를 모두 전송

```tsx
$ git push origin --tags
Counting objects: 1, done.
Writing objects: 100% (1/1), 160 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To git@github.com:schacon/simplegit.git
 * [new tag]         v1.4 -> v1.4
 * [new tag]         v1.4-lw -> v1.4-lw
```

이제 누군가 저장소에 Clone하거나 Pull을 하면 모든 태그 정보도 함께 전송

## 태그를 Checkout하기

`ex` 태그가 특정 버전을 가리키고 있고, 특정 버전의 파일을 체크아웃해서 확인하고 싶다면 다음 명령어를 실행

- 단지 태그를 체크아웃하면(브랜치 체크아웃X) “detached HEAD(떨어져 나온 HEAD)” 상태가 되며 일부 Git 관련 작업이 브랜치에서 작업하는 것과 다르게 동작할 수 있다.

```tsx
$ git checkout 2.0.0
Note: checking out '2.0.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch>

HEAD is now at 99ada87... Merge pull request #89 from schacon/appendix-final

$ git checkout 2.0-beta-0.1
Previous HEAD position was 99ada87... Merge pull request #89 from schacon/appendix-final
HEAD is now at df3f601... add atlas.json and cover image
```

“detached HEAD” 상태

- 작업을 하고 커밋을 만들면, 태그는 그대로 있으나 새로운 커밋이 하나 생성
    
    새 커밋에 도달할 수 있는 방법이 따로 없게된다.
    
- 특정 태그 상태에서 새로 작성한 커밋이 의미있도록 하려면 반드시 브랜치를 만들어 작업
    
    ```tsx
    $ git checkout -b version2 v2.0.0
    Switched to a new branch 'version2'
    ```
    
    브랜치를 만든 후 `version2` 브랜치에 커밋하면 브랜치는 업데이트
    
    `but` `v2.0.0` 태그는 가리키는 커밋이 변하지 않으므로 두 내용이 가리키는 커밋이 다르다는 것을 알 수 있다.