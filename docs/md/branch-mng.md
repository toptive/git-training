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

https://www.linkedin.com/learning/git-intermediate-techniques/identify-merged-branches


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

https://www.linkedin.com/learning/git-intermediate-techniques/delete-local-and-remote-branches

## Prune stale branches

* Delete all stale remote-tracking branches
* Remote-tracking branches, not remote branches
* Stale branch: a remote-tracking branch that no longer tracks anything because the actual branch in the remote repository has been deleted.

https://www.linkedin.com/learning/git-intermediate-techniques/prune-stale-branches

















































## Getting Started {docsify-ignore}

Using `{docsify-ignore}` to ignore the header above in the sidebar.

## Code Blocks

```javascript
function Greeter(greeting) {
  this.greeting = greeting;
}
Greeter.prototype.greet = function() {
  return "Hello, " + this.greeting;
};
var greeter = new Greeter("world");
```

## Checkboxes

* [ ] checkbox 1
* [x] checkbox 2
* [ ] checkbox 3
  * [ ] checkbox 3.1
  * [x] checkbox 3.2

## Important Note

!> **Time** is money, my friend!

```markdown
!> **Time** is money, my friend!
```

## TODO Note

?> _TODO_ unit test

```markdown
?> _TODO_ unit test
```
