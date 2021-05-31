1. Clone and update submodules
```
git clone --recurse-submodules --remote-submodules git@project
```

2. Merge with resolving conflicts
```
git merge --squash --strategy-option theirs other_branch
```

3. Find a commit with deleted file (wasn't able to use)
```
https://stackoverflow.com/questions/7203515/how-to-find-a-deleted-file-in-the-project-commit-history
```

4. Discard not-pushed-yet commits
```
git reset --hard origin/master
```
