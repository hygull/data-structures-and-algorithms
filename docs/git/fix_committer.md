# 🔧 Git Commit Author Fix Guide

## 📋 Overview

This guide helps you fix Git commit author information to use the correct email address (`rishikesh0014051992@gmail.com`) for both past and future commits. This is essential for triggering Jira Smart Commits and maintaining consistent commit history.

> **⚠️ Warning:** These operations rewrite Git history. Make sure you have a backup and coordinate with your team before force-pushing to shared branches.

---

## 🚀 Quick Fix Guide

Follow these steps in order to fix your commit author information:

### 1️⃣ Fix Future Commits (Global Config)

Run this first so you never have the "work email" problem again on this machine:

```bash
git config --global user.email "rishikesh0014051992@gmail.com"
git config --global user.name "Rishikesh Agrawani"
```

> **📝 Note:** This sets your Git identity globally for all repositories on your machine.

---

### 2️⃣ Fix All Past Commits (The "Script" Way)

Since you have multiple commits with the wrong email, use this script. It searches your entire history and replaces the work email with your personal one.

Copy and paste this into your terminal inside your project folder:

```bash
git filter-branch --env-filter '
OLD_EMAIL="rishikesh@aipalette.com"
CORRECT_NAME="Rishikesh Agrawani"
CORRECT_EMAIL="rishikesh0014051992@gmail.com"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```

> **⚠️ Important:** This rewrites the entire commit history. All commit hashes will change.

---

### 3️⃣ Force Push to GitHub

Because you have rewritten the history of your repository, a standard `git push` will fail. You must tell GitHub to accept the new history:

```bash
git push origin --force --all
```

> **⚠️ Caution:** Force pushing overwrites remote history. Ensure no one else is working on the same branch, or coordinate with your team first.

---

## 🎯 Alternative Methods

### Fix a Single Commit

If you only need to fix the most recent commit (not the entire history), use this simpler approach:

```bash
git commit --amend --author="Rishikesh Agrawani <rishikesh0014051992@gmail.com>" --no-edit
git push -f
```

> **📝 Note:** This only fixes the last commit. Use this when you catch the mistake immediately.

---

### Rewrite All Past History (Advanced)

If you absolutely want to remove the work email from your entire Git history on the current branch, use this command:

```bash
git rebase -r --root --exec "git commit --amend --no-edit --author 'Rishikesh Agrawani <rishikesh0014051992@gmail.com>'"
git push -f
```

> **⚠️ Advanced:** This is a more aggressive rewrite. Use only if you understand the implications.

---

## ✅ Verification

After completing the steps, verify your changes:

1. **Check your global config:**
   ```bash
   git config --global user.email
   git config --global user.name
   ```

2. **Check recent commit history:**
   ```bash
   git log --pretty=format:"%h - %an <%ae> : %s" -5
   ```

3. **Verify on GitHub:** Check your repository's commit history on GitHub to ensure the author information is correct.

---

## 📚 Summary

- **Step 1:** Set global Git config to prevent future issues
- **Step 2:** Rewrite commit history to fix past commits
- **Step 3:** Force push the corrected history to GitHub
- **Alternative:** Use simpler methods for single commits or specific branches

Once complete, all your commits will use the correct email address, and Jira Smart Commits will work as expected! 🎉
