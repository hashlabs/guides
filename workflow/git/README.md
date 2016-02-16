# Git

## Maintain a Repo

* Avoid including files in source control that are specific to your development machine or process.
* Delete local and remote feature branches after merging.
* Perform work in a feature branch.
* Rebase frequently to incorporate upstream changes.
* Create pull requests when you finish your work
* Try not to work on more than 1 feature per branch/pull request

## Write a Feature

Create a local feature branch based off master. Our convention for
branch names is:

`<your initials>/<ticket number>`

For example. My name is Orlando Del Aguila, so my initials are **od**.
My branch name for ticket EX-123 should be `od/ex-123`

```
git checkout master
git pull upstream
git checkout -b <branch-name>
```

Rebase from master instead of pulling

```
git checkout master
git pull
git checkout -
git rebase master
```

Squash non important commits using `git rebase -i`

Once your feature is done, push to the main repository to a new branch

```
git push upstream od/EX-123
```

Create a pull request and ask for a code review to the team members
