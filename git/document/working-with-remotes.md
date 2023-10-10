# 2.5 리모트 저장소

# 리모트 저장소

인터넷이나 네트워크 어딘가에 있는 저장소를 말한다.

저장소는 여러 개가 있다.

- 저장소를 읽기 쓰기 모두 할 수도 있고 읽기만 가능할 수 있다.

협업

→ 리모트 저장소를 관리하면서 데이터를 저장소에 Push하고 Pull하는 것

리모트 저장소 관리

→ 저장소를 추가 삭제, 브랜치를 관리하고 추적 등을 관리

## 리모트 저장소 확인하기

`git remote` 명령

- 현재 프로젝트에 등록된 리모트 저장소를 확인
- 리모트 저장소의 단축 이름을 보여준다.
- 저장소를 Clone하면 origin이라는 리모트 저장소가 자동으로 등록

```tsx
$ git clone https://github.com/schacon/ticgit
Cloning into 'ticgit'...
remote: Reusing existing pack: 1857, done.
remote: Total 1857 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (1857/1857), 374.35 KiB | 268.00 KiB/s, done.
Resolving deltas: 100% (772/772), done.
Checking connectivity... done.
$ cd ticgit
$ git remote
origin
```

`-v` 옵션을 사용하면 단축이름과 URL을 함께 볼 수 있다.

```tsx
$ git remote -v
origin	https://github.com/schacon/ticgit (fetch)
origin	https://github.com/schacon/ticgit (push)
```

만약 리모트 저장소가 여러 개 있으면 위 명령은 등록된 것 모두를 보여준다.

```tsx
$ cd grit
$ git remote -v
bakkdoor  https://github.com/bakkdoor/grit (fetch)
bakkdoor  https://github.com/bakkdoor/grit (push)
cho45     https://github.com/cho45/grit (fetch)
cho45     https://github.com/cho45/grit (push)
defunkt   https://github.com/defunkt/grit (fetch)
defunkt   https://github.com/defunkt/grit (push)
koke      git://github.com/koke/grit.git (fetch)
koke      git://github.com/koke/grit.git (push)
origin    git@github.com:mojombo/grit.git (fetch)
origin    git@github.com:mojombo/grit.git (push)
```

위와 같이 리모트 저장소가 여러 개 등록되어 있으면 다른 사람이 기여한 내용(Contributions)을 쉽게 가져올 수 있다.

(어떤 저장소에는 Push 권한까지 제공하기도 하지만 위에서는 Push 가능 권한을 확인할 수 없다.)

## 리모트 저장소 추가하기

기존 워킹 디렉토리에 새 리모트 저장소를 쉽게 추가할 수 있다.

→ `git remote add <단축이름> <url>` 명령 사용

```tsx
$ git remote
origin
$ git remote add pb https://github.com/paulboone/ticgit
$ git remote -v
origin	https://github.com/schacon/ticgit (fetch)
origin	https://github.com/schacon/ticgit (push)
pb	https://github.com/paulboone/ticgit (fetch)
pb	https://github.com/paulboone/ticgit (push)
```

이제 URL 대신 pb라는 이름을 사용

`ex` 로컬 저장소에는 없지만 Paul의 저장소에 있는 것을 가져오기

```tsx
$ git fetch pb
remote: Counting objects: 43, done.
remote: Compressing objects: 100% (36/36), done.
remote: Total 43 (delta 10), reused 31 (delta 5)
Unpacking objects: 100% (43/43), done.
From https://github.com/paulboone/ticgit
 * [new branch]      master     -> pb/master
 * [new branch]      ticgit     -> pb/ticgit
```

로컬에서 `pb/master` 가 Paul의 master 브랜치 

→ 이 브랜치를 로컬 브랜치 중 하나에 Merge하거나 Checkout해서 브랜치 내용 확인 가능

## 리모트 저장소를 Pull하거나 Fetch하기

```tsx
git fetch <remote>
```

→ 리모트 저장소에서 데이터를 가져오는 명령어

- 이 명령은 로컬에는 없지만, 리모트 저장소에 있는 데이터를 모두 가져옴
    
    → 리모트 저장소의 모든 브랜치를 로컬에서 접근이 가능
    
    - 언제든지 Merge하거나 내용을 살펴볼 수 있다.
    

저장소를 Clone → 자동으로 리모트 저장소를 “origin”이라는 이름으로 추가

그래서 나중에 `git fetch origin`을 하면 Clone한 이후에 수정된 것을 모두 가져온다.

`git fetch` 명령은 리모트 저장소의 데이터를 모두 로컬로 가져오지만, 자동으로 Merge하지 않는다.

→ 그래서 로컬에서 하던 작업을 정리해 수동으로 Merge해야 한다.

`git pull` 

- 리모트 저장소 브랜치의 데이터를 가져올 뿐만 아니라 자동으로 로컬 브랜치와 Merge 시킨다.
- git clone 명령은 자동으로 로컬의 master 브랜치와 리모트 저장소의 master 브랜치를 추적
    
    git pull은 Clone한 서버에서 데이터를 가져오고 그 데이터를 자동으로 현재 작업하는 코드와 Merge
    

 

## 리모트 저장소에 Push하기

프로젝트를 공유할 때 Upstream 저장소에 Push

```tsx
git push <리모트 저장소 이름> <브랜치 이름>
```

`ex` master 브랜치를 origin 서버에 Push

```tsx
$ git push origin master
```

- Clone한 리모트 저장소에 쓰기 권한이 있고, Clone하고 난 후 아무도 Upstream 저장소에 Push하지 않았을 때만 사용 가능
    
    → Clone한 사람이 여러 명 있을 때, 다른 사람이 Push한 후에 Push하려고 하면 Push할 수 없다. 
    
    - 먼저 다른 사람이 작업한 것을 가져와서 Merge한 후 Push 가능

## 리모트 저장소 살펴보기

`git remote show <리모트 저장소 이름>`

- 리모트 저장소의 구체적인 정보를 확인

`ex` origin 이름으로 이 명령을 실행

```tsx
$ git remote show origin
* remote origin
  Fetch URL: https://github.com/schacon/ticgit
  Push  URL: https://github.com/schacon/ticgit
  HEAD branch: master
  Remote branches:
    master                               tracked
    dev-branch                           tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date
```

리모트 저장소의 URL과 추적하는 브랜치를 출력

- git pull 명령을 실행할 때, master 브랜치와 Merge할 브랜치가 무엇인지 보여준다.
    
    git pull 명령은 리모트 저장소 브랜치의 데이터를 모두 가져오고 나서 자동으로 Merge
    
    가져온 모든 리모트 저장소 정보도 출력
    

 

## 리모트 저장소 이름을 바꾸거나 리모트 저장소를 삭제하기

`git remote rename`

- 리모트 저장소의 이름을 변경

`ex` pb를 paul로 변경

```tsx
$ git remote rename pb paul
$ git remote
origin
paul
```

여기서 로컬에서 관리하던 리모트 저장소의 브랜치 이름도 바뀐다.

- pb/master → paul/master

`git remote remove`, `git remote rm`

- 리모트 저장소를 삭제
- 서버 정보가 바뀌었을 때, 별도의 미러가 필요하지 않을 때 사용

```tsx
$ git remote remove paul
$ git remote
origin
```

이 명령을 실행하면 해당 리모트 저장소에 관련된 추적 브랜치 정보나 모든 설정 내용도 함께 삭제