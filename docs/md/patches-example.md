# Example

## Step 1: initialize a repository

Create an empty repository into a new folder and add a `README.md` file:

```bash
$ mkdir cherry-pick-example && cd cherry-pick-example
$ git init
$ echo "# cherry-pick-example" > README.md
$ git add README.md
$ git commit -m "C1: initialize the repo"
```

In your Terminal, add the URL for the remote repository where your local repository will be pushed:

```bash
$ git remote add origin https://github.com/USERNAME/PROJECT-NAME.git
$ git push -u origin master
```

## Step 2: create a python program

Create a simple python program that *prints* the content of a file. Let's create a `main.py` file with the following code:

```python
#!/usr/bin/env python

import sys

def main():
    with open(sys.argv[1], 'r') as my_file:
        print(my_file.read())


if __name__== "__main__":
    main()
```

Then, just run `python main.py file.txt` and you should see the content of `file.txt`. Let's add the file into master branch and push it:

```bash
$ git add main.py
$ git commit -m  "C2: add main.py file"
$ git push origin master
```

## Step 3: create a new_feature branch

Suppose that a new requirements came and now you should also print the number of words that exist on the file. So, to do it, just create a `new_feature` branch and add the changes:

```bash
$ git checkout -b new_feature
```

```python
#!/usr/bin/env python

import sys

def main():
    with open(sys.argv[1], 'r') as my_file:
        lines = my_file.read()
        print(lines)
        print(len(lines))

if __name__== "__main__":
    main()
```

```bash
$ git add main.py
$ git commit -m  "C3: update main.py file"
$ git push origin new_feature
```

## Step 4: a bug fix happens into master

A client report a bug on the app, it's crashing when there isn't a file parameter. So, let's fix it on master:

```bash
$ git checkout master
$ git pull origin master
```

```python
def main():
    if len(sys.argv) != 2:
        raise Exception('Please run: python main.py <filename>')

    with open(sys.argv[1], 'r') as my_file:
        print(my_file.read())
        print(len(my_file.read()))
```

```bash
$ git add main.py
$ git commit -m  "C4: fix the supported amount of parameters"
$ git push origin master
```

## Step 4: add try/except on main function

On the main function, add a general try/except to handle the error and the push it on master:

```python
if __name__== "__main__":
    try:
        main()
    except Exception as e:
        print(str(e))
        exit(0)
```

```bash
$ git add main.py
$ git commit -m  "C5: add try/except on main file"
$ git push origin master
```

## Cherry-picking a commit

The goal will be apply only the commit `C4` from *master* to *new_feature*.

1. On *master* branch, run `git pull` to ensure you have the latest changed
2. On *master*, run `git log` in Terminal. Verify that changes that you want to apply.
3. Check which commit hash/hashes are relevant and you want to have on the other branch as well.
4. Move to the *new_feature* branch
5. Make sure you have the last commit on this branch. Run `git pull` again.

![Result](/img/cp-ex2.png)

To apply the commit SHA `39787bdd4e9eaf75267a73aba36d5e4f0140db1f` on `new_feature` branch, just run the following command in Terminal:

```bash
$ git cherry-pick 39787bdd4e9eaf75267a73aba36d5e4f0140db1f
```

![Result](/img/cp-ex3.png)

At this point, just push the new change and you will apply only `C4` on `new_feature` branch. You will see a new commit on the branch.

![Result](/img/cp-ex4.png)






