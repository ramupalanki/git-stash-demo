# Git Stash Complete Workflow Demo

## Project Overview

This project demonstrates a complete **Git Stash workflow** using a
simple Python project.

The workflow simulates a real development-team scenario where a
developer is working on an unfinished feature, receives an urgent
request, temporarily saves the unfinished work using Git Stash, handles
the urgent fix on a separate branch, and then returns to the original
feature.

The repository is intentionally simple so the focus remains on Git and
GitHub concepts.

------------------------------------------------------------------------

## Learning Objectives

By completing this project, you will learn how to:

-   Create and initialize a Git repository
-   Create and switch between branches
-   Start feature development without committing unfinished work
-   Temporarily save changes using `git stash`
-   Inspect saved stash entries
-   Restore stashed changes using `git stash apply`
-   Restore and remove stashed changes using `git stash pop`
-   Delete a stash using `git stash drop`
-   Handle an urgent fix using a separate branch
-   Review Git branch and commit history
-   Push all branches to a public GitHub repository
-   Understand when Git Stash is useful in a real development team

------------------------------------------------------------------------

# Project Structure

``` text
git-stash-demo/
│
├── main.py
└── README.md
```

The Python application is intentionally simple.

------------------------------------------------------------------------

# Step 1: Create the Python Project

Create a file named `main.py`.

Initial code:

``` python
print("Welcome to the Git Stash Demo")
print("This is the initial version of the project.")
```

Run the application:

``` bash
python main.py
```

------------------------------------------------------------------------

# Step 2: Initialize the Git Repository

Open a terminal inside the project directory.

``` bash
git init
```

Check the repository status:

``` bash
git status
```

Add the Python file:

``` bash
git add main.py
```

Create the initial commit:

``` bash
git commit -m "Initial project setup"
```

Verify the commit:

``` bash
git log --oneline
```

Expected result:

``` text
<commit-id> Initial project setup
```

------------------------------------------------------------------------

# Step 3: Create the Feature Branch

Create a dedicated feature branch:

``` bash
git switch -c feature/new-message
```

Verify the branches:

``` bash
git branch
```

Expected:

``` text
* feature/new-message
  main
```

------------------------------------------------------------------------

# Step 4: Start Implementing the Feature

Modify `main.py`:

``` python
print("Welcome to the Git Stash Demo")
print("This is the initial version of the project.")

print("New feature is being developed.")
print("This feature is not finished yet.")
```

Check the changes:

``` bash
git status
```

View the differences:

``` bash
git diff
```

## Important

Do **not** commit this feature.

The feature is intentionally unfinished because an urgent task is about
to arrive.

------------------------------------------------------------------------

# Step 5: Stash the Unfinished Feature

Temporarily save the unfinished work:

``` bash
git stash
```

Check the working directory:

``` bash
git status
```

Expected:

``` text
nothing to commit, working tree clean
```

Check the stash:

``` bash
git stash list
```

Expected:

``` text
stash@{0}: WIP on feature/new-message: <commit-id> Initial project setup
```

At this point, the unfinished feature is safely stored in Git Stash.

------------------------------------------------------------------------

# Step 6: Switch to Main

Switch back to the main branch:

``` bash
git switch main
```

Verify:

``` bash
git status
```

The working directory should be clean.

------------------------------------------------------------------------

# Step 7: Create the Urgent Fix Branch

Create a separate branch for the urgent fix:

``` bash
git switch -c urgent-fix
```

Verify:

``` bash
git branch
```

Expected:

``` text
  feature/new-message
  main
* urgent-fix
```

This branch represents urgent work that needs to be completed before
returning to the feature.

------------------------------------------------------------------------

# Step 8: Implement the Urgent Fix

Modify `main.py`:

``` python
print("Welcome to the Git Stash Demo")
print("Urgent bug fix has been applied.")
```

Check the changes:

``` bash
git status
```

View the changes:

``` bash
git diff
```

------------------------------------------------------------------------

# Step 9: Commit the Urgent Fix

Add the change:

``` bash
git add main.py
```

Commit the urgent fix:

``` bash
git commit -m "Fix urgent message issue"
```

Verify the commit:

``` bash
git log --oneline
```

The urgent-fix branch should now contain a meaningful commit:

``` text
<commit-id> Fix urgent message issue
<commit-id> Initial project setup
```

------------------------------------------------------------------------

# Step 10: Return to the Feature Branch

Switch back to the feature branch:

``` bash
git switch feature/new-message
```

Check the status:

``` bash
git status
```

The working directory should be clean.

The unfinished feature is still stored in the stash.

------------------------------------------------------------------------

# Step 11: Demonstrate `git stash list`

Display all saved stashes:

``` bash
git stash list
```

Example:

``` text
stash@{0}: WIP on feature/new-message: <commit-id> Initial project setup
```

`stash@{0}` represents the latest stash.

------------------------------------------------------------------------

# Step 12: Demonstrate `git stash show`

Show a summary of the stash:

``` bash
git stash show
```

Show the complete changes stored in the stash:

``` bash
git stash show -p
```

The output should show the unfinished feature changes.

This provides evidence that the feature was actually saved using Git
Stash.

------------------------------------------------------------------------

# Step 13: Demonstrate `git stash apply`

Restore the unfinished feature:

``` bash
git stash apply
```

Check the status:

``` bash
git status
```

The feature changes should appear again.

View the restored changes:

``` bash
git diff
```

Check the stash:

``` bash
git stash list
```

The stash should still exist.

## What does `git stash apply` do?

`git stash apply`:

-   Restores the stashed changes
-   Keeps the stash entry

In simple terms:

``` text
git stash apply
       |
       +---- Restore changes
       |
       +---- Keep stash
```

------------------------------------------------------------------------

# Step 14: Demonstrate `git stash pop`

First restore the working directory to a clean state so `pop` can be
demonstrated separately:

``` bash
git restore main.py
```

Check:

``` bash
git status
```

Now restore the stash using:

``` bash
git stash pop
```

Check the working directory:

``` bash
git status
```

The unfinished feature should be restored.

Now check the stash:

``` bash
git stash list
```

The stash should no longer be present.

## What does `git stash pop` do?

`git stash pop`:

-   Restores the stashed changes
-   Removes the stash entry after applying it successfully

In simple terms:

``` text
git stash pop
       |
       +---- Restore changes
       |
       +---- Remove stash
```

------------------------------------------------------------------------

# Step 15: Apply vs Pop

  Command             Restores Changes   Keeps Stash
  ------------------- ------------------ -------------
  `git stash apply`   Yes                Yes
  `git stash pop`     Yes                No

### Easy way to remember

**Apply = Restore + Keep**

**Pop = Restore + Remove**

Use `apply` when you want the stash to remain available as a backup.

Use `pop` when you are confident that you no longer need the stash after
restoring it.

------------------------------------------------------------------------

# Step 16: Demonstrate `git stash drop`

The previous `git stash pop` removed the original stash.

Create another temporary change in `main.py`:

``` python
print("Temporary change for stash drop demonstration.")
```

Check the change:

``` bash
git status
```

Create a new stash:

``` bash
git stash
```

Verify:

``` bash
git stash list
```

Example:

``` text
stash@{0}: WIP on feature/new-message: <commit-id>
```

Delete the stash without restoring it:

``` bash
git stash drop stash@{0}
```

Verify:

``` bash
git stash list
```

The stash should no longer exist.

## What does `git stash drop` do?

`git stash drop` permanently removes a stash entry without restoring its
changes.

Be careful when using it because the stashed changes are no longer
available through that stash.

------------------------------------------------------------------------

# Step 17: Complete the Feature

Now finish the feature on `feature/new-message`.

Update `main.py`:

``` python
print("Welcome to the Git Stash Demo")
print("This is the initial version of the project.")

print("New feature has been completed.")
print("The feature was temporarily stored using Git stash.")
```

Run the application:

``` bash
python main.py
```

Expected:

``` text
Welcome to the Git Stash Demo
This is the initial version of the project.
New feature has been completed.
The feature was temporarily stored using Git stash.
```

------------------------------------------------------------------------

# Step 18: Commit the Completed Feature

Check the changes:

``` bash
git status
```

Add the file:

``` bash
git add main.py
```

Commit the completed feature:

``` bash
git commit -m "Complete new message feature"
```

Verify:

``` bash
git log --oneline
```

------------------------------------------------------------------------

# Step 19: Verify All Local Branches

Run:

``` bash
git branch -a
```

Expected:

``` text
* feature/new-message
  main
  urgent-fix
```

The repository should now have three meaningful branches:

-   `main`
-   `feature/new-message`
-   `urgent-fix`

------------------------------------------------------------------------

# Step 20: Review the Complete Git History

This is an important part of the assignment because the Git history
should provide evidence that the workflow was actually performed.

Run:

``` bash
git log --oneline --all --decorate --graph
```

Example:

``` text
* abc5678 (HEAD -> feature/new-message) Complete new message feature
| * def1234 (urgent-fix) Fix urgent message issue
|/
* 111aaaa (main) Initial project setup
```

The commit IDs will be different in your repository.

The history should demonstrate:

1.  Initial project setup
2.  Urgent fix on the `urgent-fix` branch
3.  Final feature completion on `feature/new-message`

------------------------------------------------------------------------

# Step 21: Verify the Final Working Tree

Run:

``` bash
git status
```

Expected:

``` text
nothing to commit, working tree clean
```

Also verify:

``` bash
git stash list
```

The stash list should be empty after completing the `apply`, `pop`, and
`drop` demonstrations.

------------------------------------------------------------------------

# Step 22: Create a Public GitHub Repository

Create a new **public** repository on GitHub.

Recommended repository name:

``` text
git-stash-demo
```

If the local project already contains a README, do not initialize the
GitHub repository with another README.

------------------------------------------------------------------------

# Step 23: Connect the Local Repository to GitHub

Replace `YOUR_USERNAME` with your GitHub username:

``` bash
git remote add origin https://github.com/YOUR_USERNAME/git-stash-demo.git
```

Verify:

``` bash
git remote -v
```

------------------------------------------------------------------------

# Step 24: Push the Main Branch

Switch to main:

``` bash
git switch main
```

If required, rename the local branch:

``` bash
git branch -M main
```

Push:

``` bash
git push -u origin main
```

------------------------------------------------------------------------

# Step 25: Push the Feature Branch

Push the feature branch:

``` bash
git push -u origin feature/new-message
```

------------------------------------------------------------------------

# Step 26: Push the Urgent Fix Branch

Push the urgent-fix branch:

``` bash
git push -u origin urgent-fix
```

Alternatively, all branches can be pushed together:

``` bash
git push --all origin
```

------------------------------------------------------------------------

# Step 27: Verify Remote Branches

Run:

``` bash
git branch -r
```

Expected:

``` text
origin/main
origin/feature/new-message
origin/urgent-fix
```

This is important because the GitHub repository should allow the
reviewer to inspect the feature and urgent-fix branches.

------------------------------------------------------------------------

# Step 28: Final Repository Verification

Run:

``` bash
git status
```

``` bash
git branch -a
```

``` bash
git log --oneline --all --decorate --graph
```

``` bash
git stash list
```

The final repository should have:

-   A clean working tree
-   `main` branch
-   `feature/new-message` branch
-   `urgent-fix` branch
-   Meaningful commits
-   No remaining temporary stash entries
-   All branches pushed to GitHub

------------------------------------------------------------------------

# Complete Git Command Reference

The following commands summarize the entire workflow:

``` bash
# Initialize repository
git init

# Initial commit
git add main.py
git commit -m "Initial project setup"

# Create feature branch
git switch -c feature/new-message

# Check unfinished feature
git status
git diff

# Stash unfinished work
git stash
git status
git stash list

# Switch to main
git switch main

# Create urgent fix branch
git switch -c urgent-fix

# Check urgent fix
git status
git diff

# Commit urgent fix
git add main.py
git commit -m "Fix urgent message issue"

# Return to feature branch
git switch feature/new-message

# Inspect stash
git stash list
git stash show
git stash show -p

# Restore stash and keep it
git stash apply

# Check restored changes
git status
git diff

# Clean changes for pop demonstration
git restore main.py

# Restore stash and remove it
git stash pop

# Verify stash
git stash list

# Create another temporary stash
git stash

# View stash
git stash list

# Delete stash without applying
git stash drop stash@{0}

# Complete feature
git add main.py
git commit -m "Complete new message feature"

# Review branches and history
git branch -a
git log --oneline --all --decorate --graph

# Connect GitHub repository
git remote add origin https://github.com/YOUR_USERNAME/git-stash-demo.git

# Push all branches
git push --all origin

# Verify remote branches
git branch -r

# Final verification
git status
git stash list
```

------------------------------------------------------------------------

# Real-World Use of Git Stash

Git Stash is useful when a developer has unfinished local changes but
needs to temporarily switch context.

For example:

``` text
Developer working on Feature A
            |
            v
      Feature unfinished
            |
            | git stash
            v
       Work temporarily saved
            |
            | Switch branch
            v
       Urgent Fix
            |
            | Commit
            v
       Fix completed
            |
            | Switch back
            v
       Feature A
            |
            | git stash pop
            v
       Continue Feature A
```

Typical situations include:

-   An urgent production issue needs to be fixed.
-   A developer needs to switch to another branch.
-   A developer does not want to commit incomplete work.
-   A clean working directory is required before switching branches.
-   A developer needs to temporarily pause one task and work on another.

Git Stash should generally be treated as temporary storage. Important
work should eventually be committed to an appropriate branch.

------------------------------------------------------------------------

# Git Stash Command Summary

  Command               Purpose
  --------------------- --------------------------------------
  `git stash`           Temporarily save uncommitted changes
  `git stash list`      List all stashes
  `git stash show`      Show a summary of a stash
  `git stash show -p`   Show detailed stash changes
  `git stash apply`     Restore stash and keep it
  `git stash pop`       Restore stash and remove it
  `git stash drop`      Delete a stash without restoring it

------------------------------------------------------------------------

# Assignment Evidence Checklist

Before submitting the repository, verify that the GitHub repository
demonstrates:

-   [x] Initial project commit
-   [x] Feature branch created
-   [x] Unfinished feature changes
-   [x] Unfinished changes saved with `git stash`
-   [x] `git stash list` demonstrated
-   [x] `git stash show` demonstrated
-   [x] Urgent-fix branch created
-   [x] Urgent fix committed
-   [x] Feature branch restored
-   [x] `git stash apply` demonstrated
-   [x] `git stash pop` demonstrated
-   [x] `git stash drop` demonstrated
-   [x] Final feature committed
-   [x] Git history reviewed with
    `git log --oneline --all --decorate --graph`
-   [x] Feature branch pushed to GitHub
-   [x] Urgent-fix branch pushed to GitHub
-   [x] Main branch pushed to GitHub
-   [x] Final working tree is clean

------------------------------------------------------------------------

# GitHub Repository URL

After pushing the project, replace the placeholder below with your
public GitHub repository URL:

``` text
https://github.com/YOUR_USERNAME/git-stash-demo
```

## Submission

Submit the public GitHub repository URL as the final assignment
submission.
