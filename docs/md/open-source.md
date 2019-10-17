# How to contribute to Open Source projects

As a Software Developer many times when we use external libraries we arrive to detailed cases that are not included by
the Library, or we find a small bug or even we would like a new feature, all of these scenarios could be useful for
somebody else. At this point, we need to involve the issue and try to contribute to the community.

The aim of this section is to give you the detailed steps to follow and commands to use when you contribute to an
open-source project.

## Workflow

This is the basic workflow to create a pull request

**1. Fork**

Fork the Git repository, this is to create a copy of the original repository in your account.

**2. Clone**

Once it is done, you will be able to see that repository in your account. Now click Clone/Download and copy the URL.
Make sure you are cloning the repository that is in your account by checking the URL. It should have your GitHub
username.

Then just open your terminal and navigate to the parent folder for your project and execute the git clone command with
the copied URL:

```bash
$ git clone <project-url>
```

**3. Create branch**

Navigate into the project folder `<project-url>` and create a feature branch for the changes you are going to make.

```bash
$ cd <project-url>
$ git checkout -b branch-name
```

**4. Make your changes**

After making the changes just add them to the branch and commit it with an appropriate message.

```bash
$ git add file-name-1
$ git add file-name-2
$ ...
$ git commit -m "your proper comment explaining the changes made"
```

**5. Push your changes**

Just push the changes that you have made on to the branch.

```bash
$ git push origin branch-name
```

**6. Create Pull Request**

Once you pushed, go to your GitHub repository page. You should be able to see a yellow bar with Compare and Pull request
button. Click that and add comments.

## Update a Local Fork

With a locally cloned repository, you can do the same with git in your CLI as follows. First change to your repository folder, then confirm:

```bash
$ git remote -v
```

Specify a remote upstream repo to sync with your fork:

```bash
$ git remote add upstream https://***.com/OriginalOwner/OriginalProject.git
```

Verify:

```bash
$ git remote -v
```

Fetch branches and commits from the upstream repo. You’ll be storing the commits to master in a local branch upstream/master:

```bash
$ git fetch upstream
```

Checkout your fork’s local master, then merge changes from upstream/master into it.

```bash
$ git checkout master
$ git merge upstream/master
```
