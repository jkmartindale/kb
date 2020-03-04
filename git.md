# Git

### Delete the last n commits
```shell
git reset --hard HEAD~n
```

### Move commits to another branch
First, actually make the branch you were supposed to use (but don't switch
to it).
```shell
git branch chores/fix-my-sins
```

Now the new branch points to the former `HEAD` of master (or whatever the
wrong branch was). You'll want to move the `HEAD` of the current branch back
however many commits (let's say 4).

Of course, if you do that you might lose uncommitted changes you've made, so
that's why `--keep` is a thing.

```shell
# Change 4 to however many mistakes/commits you managed to make
git reset --keep HEAD~4
```

Now go back to writing your crappy code, but in the right branch this time.
```shell
git checkout chores/fix-my-sins
```

### Reset to remote HEAD
Alright so you gone and messed everything up and want to just go back to the way things were on your remote? Sure you could delete your local repository and re-clone like a *chump* or instead you could do this pro gamer move:
```shell
# Make sure you have an updated copy of whatever remote branch you want to reset to
git fetch origin master
# Reset
git reset --hard origin/master
```

### Nuke a file
oopsie woopsie you just commited a fiwle with API keys or something  
awh!! can't just dewete the fwile in a commit because git has a histowy unu  

This processes the history of every branch and tag, removing the file:
```shell
git filter-branch --force --index-filter \
  "git rm --cached --ignore-unmatch PATH-TO-FILE-TO-DELETE" \
  --prune-empty --tag-name-filter cat -- --all
```

- `--index-filter` will rewrite the Git index without having to check out the entire tree, making it faster than `--tree-filter`  
- `git rm` tells Git to remove the file (plain `rm` works as well, but `git rm` lets you use `--index-filter`)  
- `--cached` tells `git rm` to only modify the Git index and to leave your working tree files untouched  
- `--ignore-unmatch` tells `git rm` not to complain if the file doesn't exist in a commit  
- `--prune-empty` removes gross empty commits that can sometimes be generated  
- `--tag-name-filter cat -- --all` updates the tags you have

Force push your changes on all branches if everything looks right:
```shell
git push origin --force --tags
```

You'll have to update tags separately:
```shell
git push origin --force --tags
```

Remember that your contributors will now have to rebase. Shame on you.

### Find the .git folder
Useful for when your classmates aren't paying attention in class, decide that
they know git better than the professor teaching them git, and then they do an
oopsie woopsie and make nested git repositories (that aren't submodules). This
usually ends up with them having an undesired repository active in their current
working directory, and they want it to stop.

Find the `.git` directory for the undesired repository
```shell
git rev-parse --git-dir
```

Then delete it lol
```shell
rm -rf path/to/.git/
```

Or if you're in a submodule but want its parent `.git` folder for some reason:
```sh
git rev-parse --show-superproject-working-tree
```

### GitHub Atom feeds
GitHub allows you to watch repositories, which sends you notifiations for new issues, pull requests, and releases.
But what if you'd like notifications for each commit, or changes to just a directory or single file?
GitHub publishes Atom feeds for several Git paths:
- Commits to master: https://github.com/:owner/:repo/commits.atom
- Commits to a branch: https://github.com/:owner/:repo/commits/:branch.atom
- Commits to a file or folder: https://github.com/:owner/:repo/commits/path/to/file.atom

Private repositories only offer Atom feeds for commits to a branch, which you can find in the `application/atom+xml` link tag when viewing a branch in your browser.
