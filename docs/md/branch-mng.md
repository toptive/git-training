# Branch Management

## Force push to remote

### Reasons to Force Push

* Local version is better than the remote version
* Remote version went wrong and needs repair
* Versions have diverged and merging is undesirable

```bash
$ git push -f
$ git push --force
```

https://www.linkedin.com/learning/git-intermediate-techniques/force-push-to-a-remote

## Identify merged branches

* List branches that have been merged into a branch
* Useful for knowing what features have been incorporated
* Useful for cleanup after merging many features

```bash
$ git branch --merged
```


```bash
$ git branch --no-merged
```


```bash
$ git branch -r --merged
```

## Delete local and remote branches

```bash
# Delete branch
# (Must be on a different branch)
$ git branch -d new_feature
```

```bash
# Delete not yet merged branch
$ git branch -D new_feature
```

```bash
# Delete remote branch
$ git push origin :new_feature
```

## Prune stale branches

* Delete all stale remote-tracking branches
* Remote-tracking branches, not remote branches
* Stale branch: a remote-tracking branch that no longer tracks anything because the actual branch in the remote repository has been deleted.

