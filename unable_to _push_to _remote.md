If you can’t push code to a remote Git repo, it usually comes down to a few common issues. The fix depends on the exact error, but here’s a clear troubleshooting flow that covers almost all cases.

🚨 1. First, check the error message

Run:

git push origin main

Whatever Git prints is the key. Common ones are:

Authentication failed
Rejected (non-fast-forward)
Permission denied
Remote not found
🔐 2. Authentication issues (MOST COMMON)
❌ Error:
Authentication failed
✅ Fix:

GitHub/GitLab no longer accepts passwords. You must use:

👉 Option A: Personal Access Token (PAT)
Go to GitHub → Settings → Developer settings → Tokens
Generate token
Use it instead of password when pushing
👉 Option B: SSH (recommended)

Check remote:

git remote -v

If using HTTPS, switch to SSH:

git remote set-url origin git@github.com:username/repo.git

Test SSH:

ssh -T git@github.com
🔄 3. Non-fast-forward error (very common)
❌ Error:
rejected (non-fast-forward)
Meaning:

Remote has new commits you don’t have locally.

✅ Fix:
git pull --rebase origin main
git push origin main

OR:

git pull origin main
git push origin main
🚫 4. Permission denied
❌ Error:
Permission denied (publickey)
Fix:
Check SSH key is added to GitHub/GitLab
Verify correct account access
Regenerate SSH key if needed:
ssh-keygen -t ed25519 -C "your_email@example.com"

Then add it to GitHub.

🌐 5. Remote repository not found
❌ Error:
Repository not found
Fix:

Check remote URL:

git remote -v

Fix it:

git remote set-url origin <correct-url>
🧩 6. You are on wrong branch

Check:

git branch

Push correct branch:

git push origin feature-login

Or set upstream:

git push -u origin feature-login
⚠️ 7. Detached HEAD state

Check:

git status

If you see “detached HEAD”:

Fix:

git checkout main
git push origin main
🧠 Quick diagnosis cheat sheet
Problem	Fix
Auth failed	Use PAT or SSH
Non-fast-forward	git pull --rebase
Permission denied	Fix SSH key
Repo not found	Fix remote URL
Wrong branch	git push origin <branch>
