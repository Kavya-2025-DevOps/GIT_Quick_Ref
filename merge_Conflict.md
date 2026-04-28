A **merge conflict** happens when Git can’t automatically decide which changes to keep because **two branches modified the same part of a file differently**.

Here’s a simple, practical way to solve it.

---

# ⚠️ 1. First, identify the conflict

When you run:

```bash id="c7kq2m"
git merge feature
```

Git will stop and show:

```text id="m4k9sd"
CONFLICT (content): Merge conflict in app.js
Automatic merge failed; fix conflicts and then commit the result.
```

Check status:

```bash id="x2p9ka"
git status
```

You’ll see files marked as **unmerged**.

---

# 🧩 2. Open the conflicted file

Inside the file, Git inserts markers like this:

```text id="v3nq7t"
<<<<<<< HEAD
console.log("Main branch code");
=======
console.log("Feature branch code");
>>>>>>> feature
```

---

# 🧠 What this means:

* `HEAD` → your current branch (e.g., main)
* `=======` → separator
* `feature` → incoming branch changes

---

# 🛠️ 3. Decide what to keep

You have 3 options:

### ✅ Option A: Keep your version

```text id="a1b2c3"
console.log("Main branch code");
```

### ✅ Option B: Keep incoming version

```text id="d4e5f6"
console.log("Feature branch code");
```

### ✅ Option C: Combine both (most common)

```text id="g7h8i9"
console.log("Main branch code");
console.log("Feature branch code");
```

👉 Then remove all conflict markers:

* `<<<<<<<`
* `=======`
* `>>>>>>>`

---

# ✔️ 4. Mark conflict as resolved

After editing:

```bash id="r9k2lm"
git add app.js
```

If multiple files:

```bash id="p3q8zx"
git add .
```

---

# 🎉 5. Complete the merge

```bash id="t8v4nc"
git commit
```

Git will auto-fill a merge commit message.

---

# 🔥 If you're doing rebase instead of merge

After fixing conflicts:

```bash id="rebase1"
git add .
git rebase --continue
```

---

# 🧠 Quick mental model

Think of merge conflicts like:

> “Two people edited the same sentence differently — Git is asking you: *which version should stay?*”

---

# 🛡️ Tips to avoid frequent conflicts

* Pull latest changes often:

  ```bash id="p1a2b3"
  git pull origin main
  ```
* Keep feature branches short-lived
* Avoid multiple people editing the same file area
* Communicate changes in shared modules

---

If you want, I can also show:

* A real-world conflict example from React/Java/Spring projects
* Or how to resolve conflicts using VS Code UI (much easier visually)
* Or tricky interview-level conflict scenarios
