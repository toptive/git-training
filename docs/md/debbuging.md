# Debbuging

![Result](/img/bugs.png)

In Toptive team, there are many pull requests that are merged every day and mistakes are inevitable. To fix them, we can start by looking through our commit history by hand, but this would end up being a very tedious process. Thankfully, Git has multiple tools that can help us hunt for a bug or the culprit when things go wrong.

## Git Blame

The `git blame` command helps us to find the commit that created the specific line of code that causes a bug in a specific file of a project. It also determines the author of the commit, making is easier to ask for more information about the code. For example:

![Result](/img/blame-file.png)

```bash
$ git blame -L 8,12 docs/md/patches-example.md
```

![Result](/img/git-blame.png)

The option `-L` limits the line output range. By following the _partial SHA-1_ of a commit you can easily see who, when and how was a specific line of code modified.

This command is helpful when you can assume the cause of the problem. What if you had no idea how to get back to a working state? This is where git bisect comes into play.

## Git Bisect

This is a debugging tools used to find out which specific commit introduced a bug or a problem in the project by performing an automatic binary search.

If you don't know what is breaking, and there have been a bunch of commits since the last state where you know the code worked, you’ll likely turn to git bisect for help. Bisect divides the git commit tree into 'good' bug-free commits and 'bad' commits by testing them with the binary search. Based on the result of the test, git navigates through recent commits identifying them, until it finds the culprint. If you have multiple bugs, you need to perform a binary search for each of the bugs.

![bs](/img/bisect1.png)

### How does this work?

The workflow of `git bisect` consists of two major steps. At first, you have to specify a range of revisions, limited by a good and a bad revision. These revisions can be referenced as revision hash, tag or any other git revision selector. At second, the bisect process starts and git automatically performs a checkout of the first revision to test. After passing the result of the test to back to git, by executing `git bisect good` in case of a success or `git bisect bad` in case of a failure, the next revision will be chosen. The second step will be repeated until the first broken revision has been found.

1. First, let's start with the binary search mode to find a bug:

```bash
$ git bisect start
```

2. Next, you need to look for a commit where everything was still working. To do so, let's examine the commit history to find what you need:

```bash
$ git log --oneline   # --oneline shows only the names of commits
```

![log](/img/bisect2.png)

3. Tag the oldest `good` commit SHA-1:

```bash
$ git bisect good 95d69a1
```

4. After you have assigned the `good` tag, you need to find a `bad` commit to divide the commit tree where git can apply the binary search algorithm. Since you know that the latest commit has the error, you will assign it as the `bad` commit using:

```bash
$ git bisect bad f11c599
```

5. Once you have assigned initial and final pointers for your search, Git walks you through the commit history and tags `good` and `bad` commits. This process continues until you successfully find out the _first_ `bad` commit, the cause of your problem.

Now you can exit the git binary search mode by executing:

```bash
$ git bisect reset
```

The advantage of git bisect is that reduces the number of commits that you would have to go through with binary search.

### Practical example

[Git biset tutorials](/md/debbuging-example)

### Tips

- Automatically bisect a broken build between to between v1.2 and HEAD:

```bash
$ git bisect start HEAD v1.2 --      # HEAD is bad, v1.2 is good
$ git bisect run make                # "make" builds the app
$ git bisect reset                   # quit the bisect session
```

- Automatically bisect a test failure between origin and HEAD:

```bash
$ git bisect start HEAD origin --    # HEAD is bad, origin is good
$ git bisect run make test           # "make test" builds and tests
$ git bisect reset                   # quit the bisect session
```

## Git Grep

This cmd allows us to efficiently and quickly search through the project for a string or regular expression in any of the files in your source code. It also avoids searching on _.gitignore_ file.

Additional options:

- `-n` or `--line-number`: prints out the line numbers where Git has found matches.
- `-i` or `--ignore-case`: ignores case differences between the searched keyword and the file.
- `-c` or `--count`: Shows the number of matches found in the file for the inputted keyword.
- `-p` or `--show-function`: displays the context of the searched keyword.
- `--and`: ensures multiple matches in the same line of text.

## Debugging Git network connection issues

!> Problem: sometimes we are able to push to github but we aren't able to fetch/clone/pull from the repo. For example: `git fetch origin` it hangs there forever and doesn't respond at all.

- Check your connectivity :P

```bash
$ ping google.com

PING google.com (216.58.205.238): 56 data bytes
64 bytes from 216.58.205.238: icmp_seq=0 ttl=46 time=124.577 ms
```

- Check if you have access to the repo
  Since we are able to push to repo, we are pretty sure that we have access to the repo, but still :check:

- Check if ssh/https was disabled.

```bash
$ ssh git@github.com

PTY allocation request failed on channel 0
Hi manusajith! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
```

- Try changing your DNS to 8.8.8.8

?> Welcome to `GIT_TRACE`

This configuration option gives us a more verbose trace to the git network connections and all the internal commands it goes through. This environment variable can accept the following values:

- `1,2 or true`: git will print trace: messages on stderr telling about alias expansion, built-in command execution and external command execution.

- `greater than 1 and less than 10`: git will interpret this value as an open file descriptor and will try to write the trace messages into this file descriptor.

- `absolute path`: git will interpret this as a file path and will try to write the trace messages into it.

```bash
$ GIT_TRACE=1 git fetch origin

13:44:47.299097 git.c:350               trace: built-in: git 'fetch' 'origin'
13:44:47.403611 run-command.c:336       trace: run_command: 'ssh' 'git@github.com' 'git-upload-pack '\''woumedia/naturalblender-api.git'\'''
```
