## The perfect commit

- goal is to make a commit that make sense
- each commit should be centralized for one topic
- selectively select specific files for commits

> Golden rule - only combine changes of a commit that belongs to a single commit

showing how to specifically select what changes to add in the commit not needing  certain changes in the commit 

2nd part of a perfect commit is to **crafting the perfect commit messsage**
- dependants on teams
- subject - concise summary
- body
	- what is different
	- why change
	- any notes

## Branching strategies

- follow your teams convention
- doccument
	- branching conventions
	- workflow conventions


how your team interrate changes and structure trelease.
Here are some examples:

### mainline development
- Always be integrating with the main branch
- few branches
- small commits
- needs strong / high quality QA standards

### state, releases and feature branches
- different type of branches for different purpoeses
	- i.e main branch, develop branch, feature branch
- two main types of branches and its usage
	- Long running branches
		- exist through out the whole lifetime of the project
		- often mirror stages in a sdlc
		- often no direct commits (tested / reviewd code to merge)
	- Short lived branches
		- fix / features / bug fixes / refactoring
		- one off branch, delete after integrating to long running branches

### example workflow
Github workflow
- one main long running branch
- many short lived branches
Gitflow
- 2 long running: `main` and `dev` (sdlc stages)
- many short lived branches: `features` / `releases` / `hotfix`

> not sure how to simplify his explanation but similar to how I am doing it at work

## merge v rebase
getting code from feature branch to main branch

- Fast forward merge - get all commit history from the feature branch
- Merge commit - when there are some difference in history, git try to connects two branch (may be easier to look visually)

Rebase
very cool diagram
- essentially rewrites history to make the history a straight line

## snippets


### view changes of a file
```
git diff <file>
```

### select specific changes to commit
`-p` flag or `patch` to start the interactive ui to select what to commit
```
git commit -p <file>
```

### undo merge conflicts
```
git merge --abort
git rebase --abort
```