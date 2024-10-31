#todo 
The premier version control tool. It works by storing previous versions on a hidden folder named `.git`. Essential for modern development workflow, and when integrated with a [[cloud computing|cloud]] repository (like github, gitlab, bitbucket) it makes sharing, collaborating and maintaining code and it's history a really simple task

# Theory
## Head
The git head is the cornerstone of the tool. It is the one that tells where we are currently on the project. So for example, when looking at some code, you can locate your head in an specific commit and your *workspace* will reflect the state of the code at that time, you then can change the head to another commit and it will show you the code in that point of time. via moving the head you define what you work with    
## Commits
commits are safe points in your code, they are parts in time that you decide to save, you can later revisit them as they were, if you mess up you can go back (*reset*) to a previous check point and try again. 
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

## Common errors
### leaving sensitive information
All of the information you commit to git will be stored, if you were to commit any sensitive information (like keys, passwords) anyone with access to that repository will be able to look at them.

This becomes critical when you use a cloud repository. On Github there are bots that scout for any API key, Bank key, or any valuable information they can steal
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