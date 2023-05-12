# Git Hub Cheat Sheet

A version control system that manages changes to files.

## Cloning and Initializing
| | |
|-|-|
|git clone {https}|- Pulls github repository and initializes it.|
|git init|- Creates .git file to allow for pushing.|

## Committing
| | |
|-|-|
|git status|- Shows all files that were updated, created, or deleted and if the files are untracked, tracked, or staged. Tracked meaning Git tracks versioning of the file and staged meaning the file is ready to be committed. All staged files are tracked.|
|git add {File}|- Tells git to track and stage the file so it can be committed.|
|git add .|- Tracks and stages all the files listed in status.|
|git commit -m ”{Title}” -m ”{Description}”|- Commits staged files.|

### Reset Commits 
| | |
|-|-|
|git reset -hard {commit hash}|- Resets to commit specified and deletes changes.|
|git reset {commit hash}|- Resets to commit specified and unstages changes.|
|git reset -soft {commit hash}|-Resets to commit specified, but leaves files staged.

### Logs of Commits
| | |
|-|-|
|git log|- Lists commit history. This can tell you the commit hashes.|
|git log {branch}|- Lists commit history for that branch.|

## Pushing
| | |
|-|-|
|git push {location} {branch}|- Pushes commits to the branch at the specified location.|
|git remote -v|- Shows locations you can push to.|
|git remote add {location} {https}|- Adds a location you can push to.|
|git remote remove {location}|- Removes a location you can push to.

## Pulling
| | |
|-|-|
|git pull {location} {branch}|- Pulls changes made from location’s branch.|

## Branches
| | |
|-|-|
|git checkout -b {branch}|- Creates a new branch.|
|git branch|- Shows all branches. * is for current branch.|
|git checkout {branch}|- Switches between branches.|
|git branch -d {branch}|- Deletes branch.|

## Stashing
| | |
|-|-|
|git stash |- Saves changes to a temporary storage area.|
|git stash list |- Lists all the stashes.|
|git stash pop |- Restore changes from the stash to your current directory and removes the last stash.|
|git stash apply |- Restore changes from the stash to your current directory and keeps the last stash.|
|git stash drop |- Removes the last stash.|
|git stash drop {index}|- Removes the stash at the index.|


## Setting Personal Access Tokens

Settings $\rightarrow$ Developer settings $\rightarrow$ Personal access tokens $\rightarrow$ Generate new tokens

- Make sure to check repo box so you have access to public and private repositories
- After a certain time period the token expires and needs to be regenerated and reset

| | |
|-|-|
|git remote set-url {location} https://{username}:{personal access token}@github.com/{owner's username}/{repository}.git| Gives permissions for the location. |

## First push
1. git init
1. git add .
1. git commit -m {Title} -m {Description}
1. git remote add {location} {https}
1. git remote set-url {location} https://{username}:{personal access token}@github.com/{owner's username}/{repository}.git
1. git checkout -b {branch}
1. git push {location} {branch}
- The recommended {location} is origin and the recommended {branch} is master.

## Pulling Requests/Merge
- A pull request is a request to make changes to a branch from another branch.
- A merge is the combining changes from one branch to another.

| | |
|-|-|
|Create a merge commit| Combines the changes from the source branch and the target branch and makes a commit to the target branch with the changes. Preserves the history.|
|Squash and merge| Combines all the changes from the source branch and makes a commit to the target branch with the changes. This removes the source branch. Doesn't preserve the history.|
|Rebase and merge| Commits all the previous commits in the source branch and adds them to the target branch. This removes the source branch. Preserves the history.|

## Github Markdown Notes
- Math mode has to have a newline on the top and bottom and has to be $$ for multi-line 
```
text

$$

$$

test
```

- To use underscores in math mode you have to use \textunderscore
