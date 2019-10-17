# Branching

## Branches Model

In Toptive we use Gitflow Workflow design that was first published and made popular by [Vincent Driessen at nvie](https://nvie.com/posts/a-successful-git-branching-model/) [MUST be read it]. The Gitflow Workflow defines a strict branching model designed around the project release. This provides a robust framework for managing larger projects.

![bm](/img/branch-modeling.png)

We have two main branches with infinite lifetime:

- **master** — this branch contains production code. All development code is merged into master in sometime.
- **develop** — this branch contains pre-production code. When the features are finished then they are merged into develop.

During the development cycle, a variety of supporting branches are used:

- **feature** — feature branches are used to develop new features for the upcoming releases. May branch off from develop and must merge into develop.

- **hotfix** — hotfix branches are necessary to act immediately upon an undesired status of master. May branch off from master and must merge into master anddevelop.

- **release** — release branches support preparation of a new production release. They allow many minor bug to be fixed and preparation of meta-data for a release. May branch off from develop and must merge into master anddevelop.

This ensures a clean state of branches at any given moment in the life cycle of project and the branches naming follows a systematic pattern making it easier to comprehend. Sometimes for a friendly Continuous Delivery and Continuous Integration we change the branch model.
To know more about branch workflow strategies you can read this [post](https://medium.com/@patrickporto/4-branching-workflows-for-git-30d0aaee7bf).

## Useful hints

- **Force push to remote**: some reasons to Force Push are: Local version is better than the remote version, remote version went wrong and needs repair, Versions have diverged and merging is undesirable. `git push -f` or `git push --force`

- **Identify merged branches**

  - List branches that have been merged into a branch: `git branch --merged`
  - Useful for knowing what features have been incorporated: `git branch --no-merged`
  - Useful for cleanup after merging many features: `git branch -r --merged`

- **Delete local and remote branches**

  - Delete branch (Must be on a different branch): `git branch -d new_feature`
  - Delete not yet merged branch: `git branch -D new_feature`
  - Delete remote branch: `git push origin :new_feature`
