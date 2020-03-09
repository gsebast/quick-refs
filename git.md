# Git
```bash
# --- Git clone ---
git clone git@HOST:OWNER/REPOSITORY_NAME                # Clone a remote repository using SSH
git clone https://REMOTE_REPOSITORY_URL/                # Clone a remote repository using HTTPS

# --- Git log ---
git log                                                 # Show the entire git history
git log -X                                              # Show only the last X git history entries

# --- Git pull ---
git pull                                                # Get latest changes for current branch

# --- Git add ---
git add CHANGE                                          # Stage a specific CHANGE
git add .                                               # Stage all changes at once

# --- Git commit ---
git commit -m "Your commit message goes here"           # Commit staged change(s) to local branch with a message
git commit -v                                           # Commit staged change(s) by opening the default editor for message editing

# --- Git push ---
git push                                                # Push local commit(s) to local branch
git push REMOTE_NAME REMOTE_BRANCH                      # Push local commit(s) to REMOTE_BRANCH
git push REMOTE_NAME +REMOTE_BRANCH                     # Push local commit(s) to REMOTE_BRANCH and forcing a git history rewrite if applicable
git push --set-upstream-to REMOTE_NAME LOCAL_BRANCH     # Push local commit(s) to LOCAL_BRANCH, creating the LOCAL_BRANCH under REMOTE_NAME in the process
  -or-
git push -u REMOTE_NAME LOCAL_BRANCH
git push REMOTE_NAME :REMOTE_BRANCH                     # Delete remote branch BRANCH_NAME
  -or-
git push REMOTE_NAME -d REMOTE_BRANCH
  -or-
git push REMOTE_NAME --delete REMOTE_BRANCH

# --- Git checkout ---
git checkout BRANCH_NAME                                # Switch to branch BRANCH_NAME
git checkout -b BRANCH_NAME                             # Create and switch to branch BRANCH_NAME

# --- Git branch ---
git branch                                              # List local branches only
  -or-
git branch -l
git branch -r                                           # List remote branches only
git branch -a                                           # List all branches (local and remote)
git branch -d BRANCH_NAME                               # Delete local branch BRANCH_NAME if it is already fully merged upstream
  -or-
git branch --delete BRANCH_NAME
git branch -D BRANCH_NAME                               # Force-delete local branch BRANCH_NAME, irrespective of merge status
  -or-
git branch --delete --force BRANCH_NAME

# --- Git reset ---
git reset --hard HEAD                                   # Hard reset current branch to current HEAD
git reset --soft HEAD~X                                 # Soft-reset the last X commit(s)

# --- Git stash ---
git stash                                               # Stash uncommitted (un-staged and staged) changes
git stash -u                                            # Stash uncommitted (un-staged and staged) changes and untracked files
  -or-
git stash --include-untracked
git stash save "A useful, short stash description"      # Stash uncommitted (un-staged and staged) changes with a short description

git stash list                                          # List all stashes

git stash pop                                           # Reapply last stashed changes and removing those changes from the stash collection
git stash pop stash@{X}                                 # Reapply changes of stash X and removing the respective stash from the stash collection
git stash apply                                         # Reapply last stashed changes and keeping those changes in the stash collection

git stash show                                          # Show stash summary of changes
git stash show -p                                       # Show full diff of stash
  -or-
git stash show --patch

TODO: "partial stashes"

TODO: "branches from stashes"

git stash clear                                         # Delete all stashes
git stash drop stash@{X}                                # Delete stash X only

# --- Git rebase ---
git rebase REBASE_BRANCH                                # Rebase current branch to targeted REBASE_BRANCH

# --- Git mv ---
git mv -k SOURCE_FILE DESTINATION_FILE                  # Rename SOURCE_FILE to DESTINATION_FILE
```

### Procedures
```bash
# Rebasing a BRANCH
1. Switch to branch BRANCH_NAME, i.e. the branch used as base
2. Get latest changes for current branch
3. Switch to branch BRANCH_NAME, i.e. the [local] branch to be rebased
4. Rebase current branch to targeted REBASE_BRANCH

# Squashing last X commits into one
1. Soft-reset the last X commit(s)
2. Commit staged change(s) to local branch with a message
3. Push local commit(s) to REMOTE_BRANCH and forcing a git history rewrite if applicable

# Fast-forward merge (despite detached HEAD)
1. Push local commit(s) to LOCAL_BRANCH, creating the LOCAL_BRANCH under REMOTE_NAME in the process
2. Switch to branch BRANCH_NAME, i.e. the main branch to add the changes to (typically 'master')
3. Do fast-forward merge: `git merge REMOTE_NAME/REMOTE_BRANCH`
4. Push changes onto main branch (typically 'master'): `git push REMOTE_NAME HEAD:REMOTE_BRANCH`

# Reset current repository to 'master'
1. Fetch all infos for REMOTE_NAME: `git fetch REMOTE_NAME`
2. Reset current repository to REMOTE_NAME/REMOTE_BRANCH, discarding all local changes: `git reset --hard REMOTE_NAME/REMOTE_BRANCH`
```

##### Reattach HEAD
**If you want to delete your changes associated with the detached HEAD**
You only need to checkout the branch you were on, e.g.
git checkout master

Next time you have changed a file and want to restore it to the state it is in the index, don't delete the file first, just do

```bash
git checkout -- path/to/foo
```

This will restore the file foo to the state it is in the index.

**If you want to keep your changes associated with the detached HEAD**
Run
```bash
git log -n 1;
```
this will display the most recent commit on the detached HEAD. Copy the commit hash.

Run
```bash
  git checkout master
```

Run
```bash
  git branch tmp <commit-hash>
```
This will save your changes in a new branch called tmp.
If you would like to incorporate the changes you made into master, run git merge tmp from the master branch. You should be on the master branch after running git checkout master.

--------------------------------------------------------------------------------
## Resources
* https://github.com/LeCoupa/awesome-cheatsheets
* https://stackoverflow.com/questions/520650/make-an-existing-git-branch-track-a-remote-branch
* https://stackoverflow.com/questions/10228760/fix-a-git-detached-head
* https://stackoverflow.com/questions/2850369/why-does-git-perform-fast-forward-merges-by-default
* https://stackoverflow.com/questions/16955980/git-merge-master-into-feature-branch
* https://ariya.io/2013/09/fast-forward-git-merge
* https://www.atlassian.com/git/tutorials
  - https://www.atlassian.com/git/tutorials/saving-changes/git-stash
