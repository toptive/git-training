# Example

We'll use [git-bisect-demo](https://github.com/fhinkel/git-bisect-demo) project that includes a bug introduced somewhere in its history. Feel free to clone this repository and try this out yourself.

```bash
git clone https://github.com/fhinkel/git-bisect-demo.git
npm install
```

If you run `npm test` you will realize that test passes, but if you run `npx mocha test1.js` will fail. We forgot to add these tests to the test script. At some point in the past, the tests were all passing. When did the bug get introduced? So, let's use `git bisect` to find out.

![npm test](/img/be1.png)
![npx test](/img/be2.png)

## Bisecting manually

```bash
git bisect start
```

We already konw that HEAD is a `bad` commit, so:

```bash
git bisect bad
```

Now, we need to find the hash for a good commit. So, let's go through the history of git commits.

```bash
$ git log --color --graph --pretty=format:'%h -%d %s <%an>' --abbrev-commit
```

![npx test](/img/be3.png)

We have identified the good commit, so let's test it and apply as `good` one:

```bash
git checkout b58217f #  This is the first good commit.
npx mocha test1.js # Double check that everything was green.
git bisect good
```

![good commit](/img/be4.png)

Follow the interactive prompt. At every step, run the tests with npx mocha test1.js and mark the commit as either `good` or `bad`.

When you've found the wrong commit, inspect the changes (`git show SHA`). Can you see what went wrong? Note the hash of the broken commit. Then call `git bisect reset` to exit bisection mode.

You're all done. Great job!

## Bisecting automatically

Instead of manually running `git bisect`, you can automate the process. Simply pass a command to git bisect run and let git do the rest.

```bash
$ git bisect start
$ git bisect bad
$ git bisect good b58217f
$ git bisect run npx mocha test1.js
```

![good commit](/img/be5.png)
