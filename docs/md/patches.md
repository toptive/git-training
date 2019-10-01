# Share Select Changes

Here, we'll focus on how we can use different techniques to share code between branches or even different repositories.


## Cherry-pick

![logo](/img/cherry-pick-logo.png ':size=35%') [Cherry picking]((https://git-scm.com/docs/git-cherry-pick)) in git means to choose one or more existing commits from one branch and apply it onto another. This is in contrast with other ways such as *merge* and *rebase* which normally apply many commits onto another branch.


### Cherry-picking commits

Cherry-picking means that we apply the changes from one or more existing commits. Each commit that we target is going to become a new commit on the current branch. We're essentially telling git, hey, go get that commit that you already know about, grab its changes, and apply them right here. It's conceptually similar to doing a copy and paste. One reason that it's not exactly the same as copy and paste though is that the histories of each one are different, and therefore new commits are going to have different SHAs.

Let's imagine that we have a branch called master that has six different commits on it, and at some point, I started a new feature branch that comes off of one of those commits.

![Start point](/img/cp1.png)

Now, it just so happens that one of the commits that's in master, since I branched, is something that I would like to be able to bring into new feature.

![Commit to Cherry-picking](/img/cp2.png)

I don't want to merge because I don't want the other commits. I just want to grab one little bit of code that's in that one commit and bring it into my feature branch. This is the problem that cherry-picking solves for us. It allows us to cherry-pick, that is to reach in and grab one commit and apply its change sets to our new feature branch. The result will be that we get a new commit with those same changes. We'll have identical changes between both of them (even though they'll both have different SHAs that reference them).

![Result](/img/cp3.png)

```bash
$ git cherry-pick d4e8411d09
$ git cherry-pick d4e8411d09..d4e33324.  // we can add a range on commits too
```

Strictly speaking, using git cherry-pick doesn’t alter the existing history within a repository; instead, it adds to the history. As with other Git operations that introduce changes via the process of applying a diff, you may need to resolve conflicts to fully apply the changes from the given commit.

#### Execution options

* *-edit*: will cause git to prompt for a commit message before applying the cherry-pick operation. Nice to attache a representation commit message.

* *--no-commit*: will execute the cherry pick but instead of making a new commit it will move the contents of the target commit into the working directory of the current branch.

* *--signoff*: will add a 'signoff' signature line to the end of the cherry-pick commit message.


#### Tips

* If you want to merge without commit ids you can use this command

```bash
git cherry-pick master~2 master~0
```

The above command will merge last three commits of master from 1 to 3. If you want to do this for single commit just remove last option

```bash
git cherry-pick master~2
```

* In case you needed to cherry pick a merge instead of a commit, you can use:

```bash
git cherry-pick -m 1 <hash>
```

* If you cherry-pick from a public branch, you should consider using:

```bash
git cherry-pick -x <commit-hash>
```

This will generate a standardized commit message. This way, you (and your co-workers) can still keep track of the origin of the commit and may avoid merge conflicts in the future.


* If you have notes attached to the commit they do not follow the cherry-pick. To bring them over as well, You have to use:

```bash
git notes copy <from> <to>
```

* Very usefull for releases and bug hotfixes. Consider following scenario.
You have two branches:
	* a) *release1* - This branch is going to your customer, but there are still some bugs to be fixed.
	* b) *master* - Classic master branch, where you can for example add functionality for release2.
You fix something in *release1*. Of course you need this fix also in *master*. And that is a typical use-case for cherry picking. So cherry pick in this scenario means that you take a commit from *release1* branch and include it into the *master* branch.


#### Caution!

Cherry picking is commonly discouraged in developer community. The main reason is because it creates a *duplicate* commit with the same changes and you lose the ability to track the history of the original commit. If you can merge, then you should use that instead of cherry picking. Use it with caution!

#### Practical Example

[Cherry pick example tutorial](/md/patches-example)

### Resolve cherry-picking conflicts

When we cherry-pick a commit, we're applying a predefined set of changes to our current branch. We can't be guaranteed that those changes are not going to conflict with the current state of the branch. Like `git rebase`, you need to add the file after resolve the conflict and then continue the cherry pick.

```bash
git cherry-pick 914122312

error: could not apply 914122312.. commit message
hint: after resolving the conflicts, mark the corrected paths
hint: with 'git add <path>' or 'git rm <paths>'
hint: add commit the result with 'git commit'
...
...
You are currently cherry-picking commit 914122312.
   (fix conflicts and run 'git cherry-pick --continue')
   (use 'git cherry-pick --abort' to cancel the cherry-pick operation)
```

## Patches

### Create a diff patches

Diff patches are a way for us to be able to share changes using files, instead of transferring them via a "get remote repository." This is useful whenever changes are not ready for a public branch, so we don't want to push it up toward the remote repository, or when we want to work with collaborators who don't share a remote with us. This is often used during a discussion, a review, or an approval process.

The idea is just to package up changes into files and then those files can either be emailed or put into a thumb drive or something to be shared with someone else.

To create a diff file we can use the following command:

```bash
$ git diff from-commit to-commit > output.diff
```

where:
* *from-commit*: the point at which we want the patch to start.
* *to-commit*: the patch will span the changes up to and including this point.
* *output.diff* the patch will be written here, if that file doesn't already exist, it will create it, and if it does already exist it will replace the contents with the output.

To create a diff between branches, you can run the following command:

```bash
$ git diff $(git merge-base <master> <experimental-branch>) > patch.diff
```

Then you can apply the patch using the git apply command: git apply

```bash
git apply output.diff
```

or, just can follow the old-school using [patch](https://linux.die.net/man/1/patch), for example:

```bash
$ patch -p1 < output.diff
```

