# Git Stash Complete Workflow Demo

This project demonstrates the complete Git Stash workflow using a simple Python project.

The workflow simulates a real development team scenario:

1. Start developing a new feature.
2. Do not commit the unfinished feature.
3. Temporarily save the work using `git stash`.
4. Switch to an urgent-fix branch.
5. Implement and commit the urgent fix.
6. Return to the feature branch.
7. Inspect the saved stash.
8. Restore the feature using `git stash apply`.
9. Demonstrate `git stash pop`.
10. Demonstrate `git stash drop`.
11. Complete the feature.
12. Review the Git history.
13. Push all branches to GitHub.

---

# 1. Project Structure

The project contains a simple Python file:

```text
git-stash-demo/
│
├── main.py
└── README.md