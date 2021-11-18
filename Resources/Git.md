# Discard ALL Changes
```shell
git reset --hard
git clean -f -d
```

# Rewrite author
```shell
git filter-branch -f --env-filter "GIT_AUTHOR_NAME='Sepp'; GIT_AUTHOR_EMAIL='info@sepp.dev'; GIT_COMMITTER_NAME='Sepp'; GIT_COMMITTER_EMAIL='info@sepp.dev';" HEAD
```