# 2.1 Git 저장소 만들기

# Git 저장소 만들기

Git 저장소 만드는 2가지 방법

1. 버전 관리하기 전인 로컬 디렉토리 하나를 선택해 Git 저장소를 적용
2. 다른 곳에서 Git 저장소를 Clone 하는 방법

## 기존 디렉토리를 Git 저장소로 만들기

1. git 으로 버전 관리할 프로젝트 디렉토리로 이동
    
    ```tsx
    $ cd /Users/user/my_project
    ```
    

1. 아래와 같은 명령 실행
    
    ```tsx
    $ git init
    ```
    
    - 이 명령은 .git이라는 하위 디렉토리를 만든다.
        
        .git 디렉토리는 저장소에 필요한 뼈대 파일이 들어 있다.
        

1. Git이 파일을 관리하기 위해 저장소에 파일을 추가하고 커밋해야 한다.
    
    `git add` 명령으로 파일을 추가, `git commit` 명령으로 커밋
    
    ```tsx
    $ git add *.c
    $ git add LICENSE
    $ git commit -m 'initial project version'
    ```
    
    → Git 저장소를 만들고 파일 버전 관리를 시작
    

## 기존 저장소를 Clone 하기

`git clone`

- 다른 프로젝트에 참여하거나 Git 저장소를 복사하고 싶을 때 사용
- 프로젝트 히스토리를 전부 받아온다.
- 서버에 문제가 생겨도 클라이언트 저장소 중에 하나를 가져다가 복구가 가능

`git clone <URL>`명령으로 저장소를 clone

```tsx
$ git clone https://github.com/libgit2/libgit2
```

- 위 명령은 libgit2라는 디렉토리를 생성하고 그 안에 .git 디렉토리가 생성
- 저장소의 데이터를 모두 가져와 가장 최신 버전을 Checkout해 놓는다.

다른 디렉토리 이름으로 Clone하려면 다음 명령어를 사용

```tsx
$ git clone https://github.com/libgit2/libgit2 mylibgit
```

- mylibgit 디렉토리에 데이터를 가져온다.