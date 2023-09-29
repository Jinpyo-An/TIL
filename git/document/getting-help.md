# 1.7 도움말 보기

명령어에 대한 정보가 필요할 때, 보는 방법은 2가지로 동일한 결과를 볼 수 있다.

```tsx
$ git help <verb>
$ man git-<verb>
```

`ex` 다음과 같이 git config 명령에 대한 정보를 볼 수 있다.

```tsx
git help config
```

-h, --help 옵션을 사용하면 다음과 같이 Git 명령에서 사용할 수 있는 옵션들에 대한 정보 출력

```tsx
$ git add -h
usage: git add [<options>] [--] <pathspec>...

    -n, --dry-run         dry run
    -v, --verbose         be verbose

    -i, --interactive     interactive picking
    -p, --patch           select hunks interactively
    -e, --edit            edit current diff and apply
    -f, --force           allow adding otherwise ignored files
    -u, --update          update tracked files
    -N, --intent-to-add   record only the fact that the path will be added later
    -A, --all             add changes from all tracked and untracked files
    --ignore-removal      ignore paths removed in the working tree (same as --no-all)
    --refresh             don't add, only refresh the index
    --ignore-errors       just skip files which cannot be added because of errors
    --ignore-missing      check if - even missing - files are ignored in dry run
    --chmod <(+/-)x>      override the executable bit of the listed files
```