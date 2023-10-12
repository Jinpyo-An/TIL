# 2.7 Git Alias

# Git Alias

Git의 명령을 전부 입력하는 게 귀찮다면 `git config`를 사용해 각 명령의 Alias를 쉽게 만들 수 있다.

```tsx
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
```

→ 이제 git commit 대신 git ci만으로 커밋을 할 수 있다.

이미 있는 명령을 새로운 명령으로 만들어 사용할 수 있다.

`ex` 파일을 Unstaged 상태로 변경하는 명령을 만들기

→ unstage라는 Alias 생성

```tsx
$ git config --global alias.unstage 'reset HEAD --'
```

아래 두 명령은 동일한 명령어가 되었다.

```tsx
$ git unstage fileA
$ git reset HEAD -- fileA
```

last 명령 만들기

```tsx
$ git config --global alias.last 'log -1 HEAD'
```

이제 최근 커밋을 간편하게 확인할 수 있다.

```tsx
$ git last
commit 66938dae3329c7aebe598c2246a8e6af90d04646
Author: Josh Goebel <dreamer3@example.com>
Date:   Tue Aug 26 19:48:51 2008 +0800

    test for current head

    Signed-off-by: Scott Chacon <schacon@example.com>
```