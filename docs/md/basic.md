# Git 101

> What does mean Version Control?

Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later. So ideally, we can place any file in the computer on version control. It allows you to revert files back to a previous state, revert the entire project back to a previous state, review changes made over time, see who last modified something that might be causing a problem, who introduced an issue and when, and more.

> So What is Git?

Git is a version-control system for tracking changes in computer files and coordinating work on those files among multiple people. Git is a _Distributed Version Control System_. So Git does not necessarily rely on a central server to store all the versions of a project’s files. Instead, every user “clones” a copy of a repository (a collection of files) and has the full history of the project on their own hard drive. This clone has all of the metadata of the original while the original itself is stored on a self-hosted server or a third party hosting service like GitHub.

> SVN users

Take a look of [Git for Subversion Users](https://www.codemag.com/Article/1105101/Git-for-Subversion-Users)

## Git workflow

Before we start working with Git commands, it is necessary that you understand what it represents.

> What is a Repository ?

A repository (aka repo) is nothing but a collection of source code.

> There are four fundamental elements in the Git Workflow.

![git flow](/img/git-flow.png)

If you consider a file in your Working Directory, it can be in three possible states:

1. _It can be staged_ (aka Index), which means the files with the updated changes are marked to be committed to the local repository but not yet committed.
2. _It can be modified_, which means the files with the updated changes are not yet stored in the local repository.
3. _It can be committed_ (aka HEAD), which means that the changes you made to your file are safely stored in the local repository.

> The Basic Commands

- `git add` is a command used to add a file that is in the working directory to the staging area.
- `git commit` is a command used to add all files that are staged to the local repository.
- `git push` is a command used to add all committed files in the local repository to the remote repository. So in the remote repository, all files and changes will be visible to anyone with access to the remote repository.
- `git fetch` is a command used to get files from the remote repository to the local repository but not into the working directory.
- `git merge` is a command used to get the files from the local repository into the working directory.
- `git pull` is command used to get files from the remote repository directly into the working directory. It is equivalent to a `git fetch` and a `git merge`.

### Playgroud

> Step 0: Make an Account. Duh.

You should have an account on github, bitbucket, or another platform.

> Step 1: Make sure you have Git installed on you machine

Just run the following command `git --version`.

> Step 2: Tell Git who you are.

Introduce yourself. Seriously, mention your Git username and email address, since every Git commit will use this information to identify you as the author.

```bash
$ git config --global user.name "YOUR_USERNAME"
$ git config --global user.email "your@email.com"
```

To check the info you just provided `git config --global --list`.

> Step 3: Generate your SSH keys. (Optional)

Using the SSH protocol, you can connect and authenticate to remote servers and services.

> Step 4: Let’s Git

1. Create a new repository or checkout one
   To create a new repo just make a new directory, open it and perform a `git init` to create a new git repository. To create a working copy of a local repository just run `git clone /path/to/repository`. When using a remote server, your command will be `git clone username@host:/path/to/repository`

2. Add/change && commits

You can propose changes (add it to the Index) using `git add <filename>` or `git add .`. To list all new or modified files to be committed you can run `git status`. To actually commit these changes use `git commit -m "Commit message"`. Now the file is committed to the HEAD, but not in your remote repository _yet_.

3. Pushing changes

Your changes are now in the HEAD of your local working copy. To send those changes to your remote repository, execute `git push origin master`. Change `master` to whatever branch you want to push your changes to.

If you have not cloned an existing repository and want to connect your repository to a remote server, you need to add it with `git remote add origin <remote-URL>`. Now you are able to push your changes to the selected remote server.

### Useful stuff

> Uncommit Changes

Now suppose you just made some error in your code or placed an unwanted file inside the repository, you can unstage the files you just added using `git reset HEAD~1`, this will remove the most recent commit.

> See the Changes you made

Once you start making changes on your files and you save them, the file won’t match the last version that was committed to git. To see the changes you just made `git diff`. Also you can see apply a diff onto specific file runnin `git diff <filename>`.

> Revert back to the last committed version to the Git Repo

Now you can choose to revert back to the last committed version by entering: `git checkout .` Or for a specific file you can run `git checkout <filename>`

> View Commit History

You can use the git log command to see the history of commit you made to your files: `git log`.

> Update local repo with remote repo

Just run `git pull origin <branch-name>`.
