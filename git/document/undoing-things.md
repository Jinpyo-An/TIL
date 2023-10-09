# 2.4 되돌리기

# 되돌리기

우리가 한 일을 되돌리는 방법을 살펴본다.(한 번 되돌리면 복구할 수 없기에 주의)

→ Git에서 되돌린 것은 복구할 수 없다.

완료한 커밋을 수정

- 다시 커밋하기 위해 파일 수정 작업을 하고 Staging Area에 추가한 다음 `**--amend` 옵션**을 사용해 커밋을 재작성
    
    ```tsx
    git commit --amend
    ```
    
    이 명령은 Staging Area를 사용해 커밋
    
    `if` 마지막으로 커밋하고 나서 수정한 것이 없다면(커밋하자마자 바로 이 명령을 실행)
    
    → 조금 전에 한 커밋과 모든 것이 같고 커밋 메시지만 수정한다.
    

편집기가 실행되면 이전 커밋 메시지가 자동으로 포함

만약 메시지를 수정하지 않고 그대로 커밋해도 기존의 커밋을 덮어쓴다.

만약 커밋을 했는데 Stage하는 것을 깜빡하고 빠트린 파일이 있으면 아래와 같이 실행

```tsx
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```

→ 실행한 명령어 3개는 모두 한 커밋으로 기록, 두 번째 커밋은 첫 번째 커밋을 덮어쓴다.

**Note**

`--amend` 옵션으로 커밋을 고치는 작업

- 추가 작업을하고 이전의 커밋을 완전히 새로 고쳐서 새 커밋으로 변경하는 것을 의미
    
    → 이전의 커밋은 일어나지 않은 일이 되고 당연히 히스토리에도 남지 않는다.
    
- 장점
    - 커밋 작업에서 빠뜨린 것을 넣거나 변경하는 것을 새 커밋으로 분리하지 않고 하나의 커밋에서 처리 → 커밋을 새로 만들지 않는다.

## 파일 상태를 Unstage로 변경하기

Staging Area와 워킹 디렉토리 사이를 넘나드는 방법

두 영역의 상태를 확인할 때마다(git status) 변경된 상태를 되돌리는 방법을 알려준다.

`ex` 파일 2개를 수정하고 따로 커밋을 하려 했지만, 실수로 모두 Stage Area에 넣어버렸을 때

```tsx
$ git add *
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    renamed:    README.md -> README
    modified:   CONTRIBUTING.md
```

메시지 `“git reset HEAD <file>...”`

→ 이 명령으로 Unstaged 상태로 변경할 수 있다.

[CONTRIBUTING.md](http://CONTRIBUTING.md) 파일을 **Unstaged 상태**로 변경하기

```tsx
$ git reset HEAD CONTRIBUTING.md
Unstaged changes after reset:
M	CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    renamed:    README.md -> README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```

→ [CONTRIBUTING.md](http://CONTRIBUTING.md) 파일이 Unstaged 상태가 된걸 확인할 수 있다.

**Note**

`git reset` 명령은 매우 위험

- `--hard` 옵션과 함께 사용하면 더욱 위험하다.
- 하지만 옵션없이 사용하면 워킹 디렉토리의 파일을 건드리지 않는다.

## Modified 파일 되돌리기

[CONTRIBUTING.md](http://CONTRIBUTING.md) 파일을 수정하고 되돌리는 방법

(최근 커밋된 버전으로 되돌리기)

→ `git status` 명령을 확인

위의 예제 **Unstaged** 부분 살펴보기

```tsx
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```

checkout을 통해 최근 커밋으로 되돌아가보기

```tsx
$ git checkout -- CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    renamed:    README.md -> README
```

→ 복원된 것을 확인할 수 있다.

**Note**

git checkout --<file> 명령은 위험한 명령이다.

→ 원래 파일로 덮어썼기 때문에 수정한 내용은 전부 사라진다.

변경한 내용을 쉽게 버릴 수 없지만 당장 되돌려야 한다면?

→ Stash와 Branch를 사용