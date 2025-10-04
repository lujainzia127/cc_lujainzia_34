# **CC Lab 2 – Git & GitHub Workflow**
**Name:** Lujain Zia  
**Roll No:** 2023-BSE-034  
**Date:** October 3, 2025  

---

## **Task 1 – Create Private GitHub Repository**
- Create a new **private** repository named `Lab2` on GitHub.  
- Take a screenshot of your repo settings showing it’s private.  
  - Save screenshot as: `repo_private.png`.

---

## **Task 2 – Connect Repository via SSH**
1. Generate a new **SSH key** using PowerShell.  
2. Add your SSH **public key** to GitHub → *Settings → SSH and GPG keys*.  
3. Clone your `Lab2` repo using **SSH**.

---

## **Task 3 – Configure Git Username and Email**
Set up your Git identity (links commits to you):
```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```
Verify configuration:
```bash
git config --global --list
```

---

## **Task 4 – File Status & Staging**
- Navigate into your cloned repository folder.  
- Show hidden files and locate the `.git` directory.  
- Explore what’s inside to understand Git internals.

---

## **Task 5 – Local Repository Management**
1. Delete the existing `.git` folder from your cloned repo using Git Bash.  
2. Reinitialize the local git repository:  
   ```bash
   git init
   ```
3. Add a file named `README.md`, commit it, and connect your repo to GitHub.  
4. Push your commit:
   ```bash
   git push -u origin main
   ```

---

## **Task 6 – File Status & Staging**
1. Create a new file `notes.txt` and write a note.  
2. Check its status:
   ```bash
   git status
   ```
3. Stage and commit it:
   ```bash
   git add notes.txt
   git commit -m "Added notes.txt"
   ```

---

## **Task 7 – Branch Creation Using GitHub GUI**
- On GitHub, create a branch: `bugfix/user-auth-error`.  
- Pull this branch locally to sync:
  ```bash
  git fetch origin
  git checkout bugfix/user-auth-error
  ```

---

## **Task 8 – Branch Creation & Push Using Git Bash**
- Create a branch via Git Bash:
  ```bash
  git checkout -b feature/db-connection
  git push -u origin feature/db-connection
  ```

---

## **Task 9 – Branching & Merging**
1. Create and switch to `feature-1`.  
2. Modify `main.py` (add a function) and commit it.  
3. Switch back to main and merge:
   ```bash
   git checkout main
   git merge feature-1
   git push --all origin
   ```

---

## **Task 10 – Pull Request & Branch Review**
1. Create a Pull Request (PR) on GitHub from `feature/db-connection` → `main`.  
2. Review and merge via GitHub UI.  
3. Delete the branch after merge.  
   - Screenshots:
     - `pr_create_details.png`
     - `pr_assigned_reviewer.png`
     - `pr_approved.png`
     - `pr_request_changes.png`
     - `pr_rejected.png`
     - `pr_updated_with_commits.png`
     - `pr_merge_confirm.png`
     - `pr_merged.png`
     - `pr_branch_deleted.png`

---

## **Task 11 – Branch Strategy Simulation**
Create professional workflow branches:
```
develop
staging
feature/*
bugfix/*
```

**Workflow:**
1. Developers work on `feature/*` or `bugfix/*`.
2. Merge into `develop` for integration.
3. Merge `develop` → `staging` for testing.
4. Merge `staging` → `main` for production.

**Screenshots:**
- `branch_strategy.png`
- `branch_merges.png`
- `final_merge.png`

---

## **Bonus – Simulated Team Collaboration**
1. Create a branch `collab`.  
2. Add a collaborator to your GitHub repo.  
3. Both contributors:
   - Pull latest changes.
   - Add their name & fun fact to `notes.txt`.
   - Commit and push.
4. Merge `collab` → `master` and push.  
   - Screenshot: `collab_commit.png`.

---

## **Task 12 – Code Review Workflow**
1. Create a Pull Request from a feature branch → main.  
2. Add a clear title & description.  
3. Assign a reviewer.  
4. Capture review actions (approve, request changes, reject).  
5. Author pushes fixes → PR updates automatically.  
6. Reviewer approves → merge using preferred merge strategy.  
7. Take screenshots of each step and update documentation.

---

## **Task 13 – Branch Cleanup**
- Delete remote branches after merge (GitHub UI or Git Bash):
  ```bash
  git push origin --delete <branch-name>
  ```
- Update local repo:
  ```bash
  git fetch -p
  git branch -a
  ```
- Screenshots:
  - `remote_branch_deleted.png`
  - `remote_branch_delete_cmd.png`

---

# **Exam Evaluation Tasks**

---

## **Q1 – Advanced Branching & Merge Verification**
1. Create a new branch and verify merge history.
   - Screenshots:
     - `Q1_branch_created.png`
     - `Q1_commit_done.png`
     - `Q1_merge_done.png`
     - `Q1_merge_history.png`

---

## **Q2 – Multi-Stage Workflow Simulation**
- Branches: `main`, `develop`, `staging`.  
- Create a feature branch from `develop`, make a change, and merge through all stages.

**Screenshots:**
- `Q2_branches_created.png`
- `Q2_feature_branch_commit.png`
- `Q2_merge_into_develop.png`
- `Q2_merge_into_staging.png`
- `Q2_merge_into_main.png`
- `Q2_stage_verification.png`

---

## **Q3 – Collaboration & Conflict Resolution**
1. Both collaborators modify the same file in separate branches.  
2. Attempt to merge → conflict.  
3. Resolve conflict to preserve both contributions.  
4. Verify the final file includes both changes.

**Screenshots:**
- `Q3_branches_modified.png`
- `Q3_merge_conflict.png`
- `Q3_conflict_resolved.png`
- `Q3_final_file.png`

---

## **Final Submission**
Ensure all screenshots and files are committed and pushed to your repository:
```
CC_LujainZia_34
```
