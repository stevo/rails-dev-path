# GIT Best practices

## Secured branches

- `master` branch should be secured against force-pushing
- default strategy for merging should be `rebase`
- merge should only be allowed after successful build on CircleCI

## Working with branches

* Keep repository history flat by continuosly rebasing feature branches.
* It is recommended to prefix branch names with owner initials, i.e. `bk-logic-for-accepting-external-events`

### New feature branch

```zsh
git checkout master
git pull
git checkout -b xx-feature-name
```

### Rebase with master (do it often and always before submitting PR)

```zsh
git checkout xx-feature-name
git rebase -i HEAD~10 # squash/rename/reorder commits
git pull --rebase origin master
git push origin HEAD -f
```

### Integrate branch with master from console

```zsh
# First rebase feature branch with master (look above)
git checkout master
git pull
git merge xx-feature-name --ff-only
git push origin master
git branch -d xx-feature-name
git push origin :xx-feature-name
```

## Hotfixing

* Hotfixes are commits that can be applied directly into master branch
* If hotfix cannot be applied directly to master branch and is critical, it can be applied direactly to heroku's master branch.
* Any hotfix not applied directly to master branch should undergo regular PR (review + CI) process
* It is recommended to prefix hotfix commit message with `[HOTFIX]`


## Other

* Always integrate with master through accepted (reviewed) pull request
  * [This is why](http://blog.smartbear.com/code-review/pros-and-cons-of-code-review-methods-infographic/)
* Only integrate directly with master when adding hot-fixes or not executable code (readme, docs etc.)
  * Not to skip code review
* Only merge with master through rebase to keep history flat
  * [This is why](http://www.bitsnbites.eu/a-tidy-linear-git-history/)
* Do merge/fixup/cleanup/rename feature branch commits to some clean state before integrating with master
  * Keeps history tidy and easy to browse
* Keep you Pull Requests small
  * [This is why](http://blog.ploeh.dk/2015/01/15/10-tips-for-better-pull-requests/)
