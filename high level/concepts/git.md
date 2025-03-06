 The premier version control tool. It works by storing previous versions on a hidden folder named `.git`. Essential for modern development workflow, and when integrated with a [[cloud computing|cloud]] repository (like github, gitlab, bitbucket) it makes sharing, collaborating and maintaining code and it's history a really simple task

# Theory
## 4 objects

Internally git only knows four things:
### Commits
commits are safe points in your code, they are parts in time that you decide to save, you can later revisit them as they were, if you mess up you can go back (*reset*) to a previous check point and try again.
### tree 
Is like a directory, it points to blobs or other trees. 
### blobs
A bunch of bytes. This is the information that you are actually storing
### tags
Just another reference to a commit object and just makes for easier referencing
## Head
The git head is the cornerstone of the tool. It is the one that tells where we are currently on the project. So for example, when looking at some code, you can locate your head in an specific commit and your *workspace* will reflect the state of the code at that time, you then can change the head to another commit and it will show you the code in that point of time. via moving the head you define what you work with    
## Branches
As your projects start to grow, you might want to do some stuff without altering the current state; That is were branches come into play. When you create a branch, it will sprout from the current commit, and they will keep on growing separately with each commit to the branch. When you are sure that the new branch is completed you can *merge* them.

This is commonly use for features or different people. The plan is for the **main** branch to always be fully functional and error free. when a new feature is started, you should branch out, complete it and then merge into **main**.

With branching, [[CI]] and [[CD]] you can make any code that touches the **main** branch pass some test, or deploy to your servers. 

## .gitignore
you don't want to push everything to git, somethings as keys, environment variables, packages or compilated code should stay out, as these may hold important value, or just take extra space 
## stages
Files tracked by Git have 3 stages, these being 
- **Untracked**: new files and modifications
- **Staged**:  files that where added using a `git add`
- **Committed**: files fully stored on a commit
## Merge
There are multiple types of merging.
### Fast-Forward Merge
This happens when the target branch is ahead, and there are no divergent changes. The branch pointer simply moves forward.
```sh
git checkout main 
git merge feature-branch
```

If a fast-forward merge is possible, it will be performed automatically.
### Recursive (3-way) Merge

This occurs when branches have diverged, and Git needs to create a new commit to combine them.

```sh
git checkout main 
git merge feature-branch
```

If conflicts arise, Git will prompt you to resolve them before completing the merge.

### Squash Merge

This merges changes into a single commit instead of keeping all individual commits from the feature branch.

```sh
git checkout main 
git merge --squash feature-branch 
git commit -m "Squashed commit message"
```


### No-FF (No Fast-Forward) Merge

Forces Git to always create a new merge commit, even if a fast-forward merge is possible.

```sh
git checkout main
git merge --no-ff feature-branch
```

### Ours Merge Strategy

This keeps changes from the current branch and ignores incoming changes.
```sh
git checkout main 
git merge -s ours feature-branch
```

### Theirs Merge Strategy

The inverse of "ours"—it keeps incoming changes and discards changes from the current branch.
```sh
git checkout main 
git merge -X theirs feature-branch
```

### Octopus Merge (Multiple Branch Merge)

Used when merging more than two branches simultaneously (usually for integration branches).
```sh
git checkout main
git merge feature-branch1 feature-branch2
```

###  Rebase Merge (Alternative to Merge)

Instead of merging, rebase applies commits one by one on top of the target branch.
```sh
git checkout feature-branch
git rebase main
```

Then, fast-forward merge:
```sh
git checkout main
git merge feature-branch
```

## rebase

rebase has two use cases
### linear merging
When you merge, your new branch commits will go after the last commit (the ones after the branches parted ways). In other words the stories will be diverted and it will be shown.

When you use rebase for merging it actually puts the commits before any current changes on the branch. And then will change the hashes of the current commits. This will create a more linear commit history.  This could be cleaner depending on what workflow you are following

![[git_rebase.png]]
### changing previous commits
When you want to change something in a previous commit you can use rebase.

You have to define an starting point and an ending point. like this:
```sh
git rebase -i HEAD~2
```

In this case this will open a [[vim]] window with the two commits on that range
![[rebaseConsole.png]]
You have to edit the beginning and decide what you are going to do (see the list on the image. e for editing, s for squashing...)

after exiting [[vim]] you will go to those commits you decided to edit you can make any changes as you'd like.  After that do a:
```sh
git commit --amend
git rebase --continue
```
or
```sh
git commit --amend --no-edit
git rebase --continue
```
If that fails a merge error has occurred. you could try creating a new commit and that would resolve the rebase. 

#### Deleting previous commits
if you want to delete some previous commits. You would start a rebase, and set it to *d* on vim, this will delete these commits completely.
After deleting them on your local changes, you must do a 
```sh
git push origin BRANCH --force
```

That will delete them from the remote repository

This is a powerful tool but without care you could delete important stuff. 

## remotes
Remotes are the repositories you normally see.

you can add one with 
```sh
git remote add NAME URL
```

Whenever you do a pull, or push. You specify the name of the remote. `origin` is just a common name, it does not mean anything special.
## Common errors
### leaving sensitive information
All of the information you commit to git will be stored, if you were to commit any sensitive information (like keys, passwords) anyone with access to that repository will be able to look at them.

This becomes critical when you use a cloud repository. On GitHub there are bots that scout for any API key, Bank key, or any valuable information they can steal
### dangling files
dangling files are created when you add a new file to your `.gitignore` but that file is already committed. These files won't be tracked nor deleted by `.gitignore` so even though you don't want them they will stay.
for example, if you pushed your logs to git, but then added `*.log` to the `.gitignore` they will still be tracked

to solve this you do a:
```sh
git rm -r --cached .
```
### not stashing
if you need to move your git head, but your working directory has files in it, it won't allow you, Instead of creating a commit you can stash, this will save those changes temporarily
# practice
### create repo
```sh
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/USER/REPONAME.git
git push -u origin main
```
## adding origin
you can have as many remotes as you might want
```sh
git remote add NAME https://github.com/USER/REPONAME.git
```
## git checkout

checkout has two different uses. Changing branches:
```sh
git checkout branch
```
and restoring older commits:
```sh
git checkout COMMIT_ID
```
In response to these two uses there are two new commands that work the same as git checkout
- git switch
- git restore

## change accounts
Whenever you are working on multiple git accounts, to change you must:
`git config credential.username user` where user would be the simple name, for example `dcanasp`.