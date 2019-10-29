# git

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
