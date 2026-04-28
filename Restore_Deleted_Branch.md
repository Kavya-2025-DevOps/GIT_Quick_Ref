If a junior developer accidentally deletes a Git branch, recovery is usually straightforward 
**as long as the branch’s commits still exist in the repository history** (which is almost always the case).

Here’s how you restore it.

---

# 🧠 1. Find the last commit of the deleted branch

Git doesn’t immediately erase commits when a branch is deleted. You can recover it using:

```bash
git reflog
```

This shows a history of everything your HEAD pointed to.

Look for something like:

```
abc1234 HEAD@{5}: checkout: moving from feature-login to main
def5678 HEAD@{6}: commit: implement login feature
```

👉 Identify the commit hash where the branch last existed (e.g., `def5678`).

---

# 🌿 2. Recreate the branch from that commit

Once you find the commit hash:

```bash
git checkout -b feature-login def5678
```
########### feature-login - Is a Branch name 

or (modern syntax):

```bash
git switch -c feature-login def5678
```

✔ This restores the branch exactly as it was.

---

# ☁️ 3. If it was deleted on remote (GitHub/GitLab)

If someone ran:

```bash
git push origin --delete feature-login
```

You can restore it the same way:

### Step 1: find commit locally or via reflog

### Step 2: push it back

```bash
git push origin feature-login
```

---

# 🧾 4. If reflog is not available (rare cases)

Try:

```bash
git fsck --lost-found
```

This finds dangling commits:

```
dangling commit def5678
```

Then recreate branch:

```bash
git checkout -b feature-login def5678
```

---

# ⏳ 5. Important limitation

Recovery is NOT possible if:

* Garbage collection already ran (`git gc`)
* Commits were never pushed and local history is gone
* Reflog expired (usually after ~90 days by default)

---

# 🛡️ Best practices to avoid this

* Protect `main` / `develop` branches in GitHub/GitLab
* Enable branch deletion protection for important branches
* Use PR-based workflow (avoid force pushes/deletions)
* Educate team: “delete remote branch only after merge”

---

# 🚀 Quick summary

To recover a deleted branch:

```bash
git reflog
git checkout -b <branch-name> <commit-hash>
git push origin <branch-name>
```

---

If you want, I can also show:

* How Git internally stores deleted branches (very useful for interviews)
* Or a “real incident recovery playbook” used in teams when this happens in production repos
