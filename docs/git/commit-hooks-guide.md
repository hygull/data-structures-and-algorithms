# 🪝 Git Hooks for Jira Smart Commits

## What Is It?

A Git hook that automatically prompts you to add a Jira ticket ID to your commit messages, enabling seamless integration between your commits and Jira tasks.

## How It Works

When you run `git commit`, the `prepare-commit-msg` hook:

1. Checks if your commit message already starts with `DSA-` pattern
2. If not, prompts you: "Enter Jira ticket ID (e.g., DSA-3) or press Enter to skip:"
3. If you provide a ticket ID, it prepends it to your commit message in the format: `DSA-X <your message>`
4. If you press Enter, it skips and uses your original message

## Installation

The hook is already installed at `.git/hooks/prepare-commit-msg` and is executable.

To verify:
```bash
ls -la .git/hooks/prepare-commit-msg
```

You should see `-rwxr-xr-x` permissions (the `x` means executable).

## Usage Examples

### Example 1: Adding a Ticket ID

```bash
$ git commit -m "Add binary search implementation"

🎫 Jira Smart Commit Helper
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Enter Jira ticket ID (e.g., DSA-3) or press Enter to skip: 3

✅ Commit message updated: DSA-3: ...
```

**Result:** Commit message becomes `DSA-3 Add binary search implementation`

### Example 2: Ticket ID with Prefix

```bash
$ git commit -m "Fix edge case in merge sort"

🎫 Jira Smart Commit Helper
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Enter Jira ticket ID (e.g., DSA-3) or press Enter to skip: DSA-7

✅ Commit message updated: DSA-7: ...
```

**Result:** Commit message becomes `DSA-7 Fix edge case in merge sort`

The hook automatically strips the `DSA-` prefix if you include it.

### Example 3: Skipping the Prompt

```bash
$ git commit -m "Update README"

🎫 Jira Smart Commit Helper
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Enter Jira ticket ID (e.g., DSA-3) or press Enter to skip: [press Enter]

⏭️  Skipping Jira ticket ID
```

**Result:** Commit message remains `Update README`

### Example 4: Message Already Has Ticket ID

```bash
$ git commit -m "DSA-5 Implement AVL tree rotations"
```

**Result:** Hook detects the `DSA-` prefix and skips the prompt entirely.

## Jira Smart Commits Integration

Once your commits include the `DSA-X` prefix, Jira automatically links them to the corresponding ticket. You can also use Jira Smart Commit commands:

### Transition Workflow
```bash
git commit -m "DSA-3 Implement binary search #done"
```
Moves ticket DSA-3 to "Done" status.

### Log Time
```bash
git commit -m "DSA-5 Add unit tests #time 2h"
```
Logs 2 hours of work on ticket DSA-5.

### Add Comment
```bash
git commit -m "DSA-7 Fix bug #comment Resolved edge case with empty arrays"
```
Adds a comment to ticket DSA-7.

### Combined Commands
```bash
git commit -m "DSA-10 Complete heap implementation #time 3h #done"
```
Logs time AND transitions the ticket.

## Bypassing the Hook

If you need to commit without the hook (e.g., for automated commits or quick fixes):

```bash
git commit --no-verify -m "Quick typo fix"
```

The `--no-verify` flag skips all Git hooks.

## Troubleshooting

### Hook Not Running

**Problem:** The hook doesn't prompt when you commit.

**Solution:**
1. Check if the hook file exists:
   ```bash
   ls -la .git/hooks/prepare-commit-msg
   ```

2. Ensure it's executable:
   ```bash
   chmod +x .git/hooks/prepare-commit-msg
   ```

3. Verify you're not using `--no-verify`:
   ```bash
   git commit -m "message"  # ✅ Hook runs
   git commit --no-verify -m "message"  # ❌ Hook skipped
   ```

### Hook Not Prompting in Non-Interactive Mode

**Problem:** Hook doesn't prompt when using Git GUI tools or CI/CD.

**Solution:** This is expected behavior. The hook only prompts in interactive terminal sessions. In non-interactive mode (GUI tools, scripts, CI/CD), it silently skips the prompt.

### Ticket ID Not Appearing in Jira

**Problem:** Commits with `DSA-X` prefix don't show up in Jira.

**Solution:**
1. Verify the ticket ID exists in Jira
2. Ensure your Git email matches your Jira account email
3. Check that your repository is connected to Jira (requires admin setup)
4. Wait a few minutes — Jira sync can be delayed

### Wrong Ticket ID Added

**Problem:** You added the wrong ticket ID to a commit.

**Solution:**
1. Amend the last commit:
   ```bash
   git commit --amend
   ```
   Edit the message in your editor, save, and close.

2. For older commits, use interactive rebase:
   ```bash
   git rebase -i HEAD~3  # Edit last 3 commits
   ```
   Change `pick` to `reword` for the commit you want to edit.

### Hook Interfering with Merge Commits

**Problem:** Hook prompts during merge commits.

**Solution:** The hook automatically skips merge, squash, and amend commits. If it's still prompting, check the `COMMIT_SOURCE` variable in the hook script.

## Customization

To modify the hook behavior, edit `.git/hooks/prepare-commit-msg`:

### Change the Ticket Prefix
Replace `DSA-` with your project prefix:
```bash
# Line 17: Change the pattern
if echo "$COMMIT_MSG" | grep -qE "^YOUR-PREFIX-[0-9]+ "; then

# Line 33: Change the prepend format
echo "YOUR-PREFIX-$TICKET_ID $COMMIT_MSG" > "$COMMIT_MSG_FILE"
```

### Make Ticket ID Mandatory
Remove the "press Enter to skip" option:
```bash
# Replace the prompt section with:
while [ -z "$TICKET_ID" ]; do
    echo -n "Enter Jira ticket ID (required): "
    read -r TICKET_ID
done
```

### Auto-Detect Ticket from Branch Name
If your branches are named like `DSA-3-binary-search`:
```bash
# Add after line 15:
BRANCH_NAME=$(git symbolic-ref --short HEAD 2>/dev/null)
if echo "$BRANCH_NAME" | grep -qE "^DSA-[0-9]+"; then
    TICKET_ID=$(echo "$BRANCH_NAME" | grep -oE "DSA-[0-9]+")
    echo "$TICKET_ID $COMMIT_MSG" > "$COMMIT_MSG_FILE"
    exit 0
fi
```

## Best Practices

1. **Always include ticket IDs** for feature work and bug fixes
2. **Skip ticket IDs** for trivial commits like typo fixes or README updates
3. **Use Smart Commit commands** to update Jira status directly from commits
4. **Keep commit messages clear** — the ticket ID is a prefix, not a replacement for a good message
5. **Review before pushing** — use `git log --oneline` to verify ticket IDs are correct

## References

- [Jira Smart Commits Documentation](https://support.atlassian.com/jira-software-cloud/docs/process-issues-with-smart-commits/)
- [Git Hooks Documentation](https://git-scm.com/docs/githooks)
- [Project Workflow Guide](../project/workflow-guide.md)
