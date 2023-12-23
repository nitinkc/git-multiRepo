# Multi repo project
- Bitbucket Repo : https://nitinc@bitbucket.org/nitinc/git-tests-bb.git
- Github Repo : https://github.com/nitinkc/git-multiRepo.git

(https://nitinkc.github.io/git/multi-repo-push/)[https://nitinkc.github.io/git/multi-repo-push/]

# Critical Features
- Add Another Remote Repo (Bitbucket Repo with bb as remote repo name)

```shell
git remote add bb https://nitinc@bitbucket.org/nitinc/git-tests-bb.git
```
- Should be able to Push/pull from Bitbucket (bb) with `git push bb <branch name>`

```shell
git remote set-url --add --push bb https://nitinc@bitbucket.org/nitinc/git-tests-bb.git
```

- Should also be able to Push or Pull from at `git pull` (From at least one of the Repo)

```shell
git remote add origin https://github.com/nitinkc/git-tests.git
git remote set-url --add --push origin https://github.com/nitinkc/git-multiRepo.git
```

- Should be able to push and pull to both repo simultaneously with one custom command `git push both <branch_name>`
```shell
# Add the remote with fetch URL
git remote add both https://github.com/nitinkc/git-multiRepo.git
git remote add both https://nitinc@bitbucket.org/nitinc/git-tests-bb.git

# Add an additional URL for push
git remote set-url --add --push both https://github.com/nitinkc/git-multiRepo.git
git remote set-url --add --push both https://nitinc@bitbucket.org/nitinc/git-tests-bb.git
```
if remote add for the second url gives error, add the entry manually into `gitconfig`. If not added, then also, the `--push`
switch of `remote set-url` takes care of pushing the code into both the repo. the only difference will be in pulling the code. The code
will be pulled on;y from the repo thats `remote add` first.

```editorconfig
[remote "both"]
	url = https://github.com/nitinkc/git-multiRepo.git
	url = https://nitinc@bitbucket.org/nitinc/git-tests-bb.git
	fetch = +refs/heads/*:refs/remotes/both/*
	pushurl = https://nitinc@bitbucket.org/nitinc/git-tests-bb.git
	pushurl = https://github.com/nitinkc/git-multiRepo.git
```

# Secondary features
- git hooks for github. Do not allow push into main or Develop branch


- try pre commit to avoid accidental commits on develop branch
