# Discard ALL Changes
```shell
git reset --hard
git clean -f -d
```

# Rewrite author
```shell
git filter-branch -f --env-filter "GIT_AUTHOR_NAME='Sepp'; GIT_AUTHOR_EMAIL='info@sepp.dev'; GIT_COMMITTER_NAME='Sepp'; GIT_COMMITTER_EMAIL='info@sepp.dev';" HEAD
```

# Conditional Includes
- Properties defined in this file will override existing properties defined in the `.gitconfig` in the user's home directory.
- If the pattern ends with /, ** will be automatically added. For example, the pattern foo/ becomes foo/ . In other words, it matches "foo" and everything inside, recursively.
- More info on this topic can be found here: [git-scm.com](https://git-scm.com/docs/git-config#_conditional_includes)

1. Create a `.gitconfig` file in the parent directory of the git repositories you want this config to apply:
```gitconfig
[user]
	name = Sepp
	email = info@sepp.dev
```

2. Add the condition include to your main `.gitconfig` in the users home directory
```gitconfig
[includeIf "gitdir:~/personal/"]
    path = ~/personal/.gitconfig
```