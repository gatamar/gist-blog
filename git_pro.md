# basic commands
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

# keys

## GPG

Setting up GPG is tough, here is at least some log of how I done that in few hours.

1. Generate the key
[Generating a new GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)
(it's important to use a new command `gpg --default-new-key-algo rsa4096 --gen-key` !)

2. Add it in Github web ui
[Adding a new GPG key to your GitHub account](https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-new-gpg-key-to-your-github-account)

3. Update Git Config
Do this, but remember, it's not enough!!!
[Telling Git about your signing key](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key)

Now, after signing key added, update GitConfig more:
```
[user]
    signingkey = <GPG-KEY>
[commit]
    gpgsign = true
```
This should be done both for global config `~/.gitconfig` and for any local `path-to-repo/.git/config`. If not `gpgsign = true`, then commit will be neither verified nor unverified 😅.

4. If the above is not enough, play with `gpg` + `pinetry`:
`git config --global gpg.program gpg`
`brew install pinentry`
```
$ cat ~/.gnupg/gpg-agent.conf
pinentry-program /usr/local/bin/pinentry-mac
```
