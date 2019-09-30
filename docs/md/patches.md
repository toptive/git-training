# Share Select Changes

Here, we'll focus on how we can use different techniques to share code between branches or even different repositories.

## Cherry-picking

Cherry-picking means that we apply the changes from one or more existing commits. Each commit that we target is going to become a new commit on the current branch. We're essentially telling git, hey, go get that commit that you already know about, grab its changes, and apply them right here. It's conceptually similar to doing a copy and paste. One reason that it's not exactly the same as copy and paste though is that the histories of each one are different, and therefore new commits are going to have different SHAs.

Let's imagine that we have a branch called master that has six different commits on it, and at some point, I started a new feature branch that comes off of one of those commits.

![Start point](https://i.imgur.com/ww995Tw.jpg)

Now, it just so happens that one of the commits that's in master, since I branched, is something that I would like to be able to bring into new feature.

![Start point](https://i.imgur.com/ww995Tw.jpg)

I don't want to merge because I don't want the other commits. I just want to grab one little bit of code that's in that one commit and bring it into my feature branch. This is the problem that cherry-picking solves for us. It allows us to cherry-pick, that is to reach in and grab one commit and apply its change sets to our new feature branch. The result will be that we get a new commit with those same changes. We'll have identical changes between both of them (even though they'll both have different SHAs that reference them).

![Start point](https://i.imgur.com/ww995Tw.jpg)

```bash
$ git cherry-pick d4e8411d09
$ git cherry-pick d4e8411d09..d4e33324.  // we can add a range on commits too
```

### Example

Let's try an example.

https://www.linkedin.com/learning/git-intermediate-techniques/cherry-picking-commits
