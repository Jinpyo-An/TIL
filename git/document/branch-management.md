# 3.3 브랜치 관리

# 브랜치 관리

`git branch` 명령

- 아무런 옵션 없이 실행하면 브랜치의 목록을 보여준다.

```tsx
$ git branch
  iss53
* master
  testing
```

- `*`  기호가 붙어 있는 master 브랜치는 현재 checkout해서 작업하는 브랜치

`git branch -v` 명령을 실행하면 브랜치마다 마지막 커밋 메시지도 함께 보여준다.

```tsx
$ git branch -v
  iss53   93b412c fix javascript issue
* master  7a98805 Merge branch 'iss53'
  testing 782fd34 add scott to the author list in the readmes
```

현재 브랜치 기준으로 `--merged`와 `--no-merged` 옵션을 사용해 Merge된 브랜치인지 아닌지 확인해 볼 수 있다.

`git branch --merged` 명령으로 이미 Merge한 브랜치 목록을 확인

```tsx
$ git branch --merged
  iss53
* master
```

- iss53 브랜치는 앞에서 이미 Merge 했기 때문에 목록에 나타난다.
    
    `*`  기호가 붙어 있지 않은 브랜치는 git branch -d 명령으로 삭제해도 되는 브랜치
    
    → 이미 다른 브랜치와 Merge 했기 때문에 삭제해도 정보를 잃지 않는다.
    

`git branch --no-merged` 명령을 사용해 현재 브랜치에서 Merge하지 않은 브랜치를 확인

```tsx
$ git branch --no-merged
  testing
```

→ 아직 Merge하지 않은 커밋을 담고 있기 때문에 `git branch -d` 명령으로 삭제되지 않는다.

```tsx
$ git branch -d testing
error: The branch 'testing' is not fully merged.
If you are sure you want to delete it, run 'git branch -D testing'.
```

Merge하지 않은 브랜치를 강제로 삭제하려면 -D 옵션으로 삭제

위 명령을 사용할 때 특정 브랜치 기준으로 Merge되거나 혹은 Merge되지 않은 브랜치 정보를 확인하려면 명령에 브랜치 이름을 지정

`ex` master 브랜치에 아직 Merge되지 않은 브랜치 확인

```tsx
$ git checkout testing
$ git branch --no-merged master
  topicA
  featureB
```