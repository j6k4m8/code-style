# How to Git Nicely

## Pull latest master.

```
git checkout master
git pull origin master
```

## Check out a new feature-branch.
Usually, I like to prefix my branches with a good indicator of what they're going to do. So `fix` or `add` are two good ways of indicating that this is a bug-fix or feature-implementation.

```
git checkout -b fix-secret-loophole
```

## Do your work.
Make your edits. Then,
```
git add [files or directories]
git commit -m "Fix the secret loophole in loophole.c"
```

## Update your copy
If you haven't coded for a bit and want to be sure that you're not going to have any merge conflicts, run:
```
git checkout master
git pull
git checkout fix-secret-loophole
git rebase master
```
There *may* be merge-conflicts, but at least you'll fix them locally, and it won't break when you push to GitHub! (PS: If you're new to dealing with merge confs, GitHub's [Atom editor](https://atom.io) has a great Merge-Conflict extension.)

## Commit and push to GitHub regularly.
The more atomic your commits, the better! We squash them all when we merge a pull-request, so more commits is always better, and will make your life easier if you run into merge conflicts. My rule of thumb is to commit after every "step" of implementation (so generally I don't commit broken things, but I do commit incomplete things) and then push after big, working milestones (so I wouldn't push an incomplete thing, but I would push an unstyled, working thing). But of course, this is all up to you!

## Submit a Pull Request
Go to the repo page on GitHub, click <kbd>Pull Requests</kbd>, and create a new one. Select your new branch to merge into `master`. **If you're still working, add the `do-not-merge` label.** Otherwise, we'll assume it's ready for code-review! 

## Merge!
When tests pass and code review is finished (a good sign is that other developers got to take a look at your code and approved with a 👍 or the like), merge at will!
