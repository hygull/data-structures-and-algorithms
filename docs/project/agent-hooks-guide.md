# 🪝 Kiro Agent Hooks Guide

## What Are Kiro Agent Hooks?

Kiro Agent Hooks are intelligent automation triggers that connect IDE events to AI agent actions. Unlike traditional Git hooks that run shell scripts, Agent Hooks leverage Kiro's AI capabilities to provide context-aware assistance during your development workflow.

**Key Differences from Git Hooks:**

| Feature | Git Hooks | Kiro Agent Hooks |
|---------|-----------|------------------|
| **Execution** | Shell scripts | AI agent actions |
| **Intelligence** | Rule-based | Context-aware |
| **Interaction** | Limited | Conversational |
| **Scope** | Git operations only | Any IDE event |
| **Customization** | Bash scripting | Natural language prompts |

## How Agent Hooks Work

Agent Hooks follow a simple pattern:

```
WHEN [event happens] → THEN [take action]
```

**Event Types:**
- `fileEdited` — File is saved/modified
- `fileCreated` — New file is created
- `fileDeleted` — File is deleted
- `promptSubmit` — User submits a prompt to Kiro
- `agentStop` — Agent finishes execution
- `preToolUse` — Before a tool is used
- `postToolUse` — After a tool is used
- `preTaskExecution` — Before a task starts
- `postTaskExecution` — After a task completes
- `userTriggered` — Manual trigger by user

**Action Types:**
- `askAgent` — Prompt Kiro to perform an action
- `runCommand` — Execute a shell command

## Installed Hooks in This Project

### 1. Jira Smart Commit - Add Ticket ID
**ID:** `jira-ticket-prepend`  
**Event:** `promptSubmit`  
**Action:** `askAgent`

Automatically checks if your commit message includes a Jira ticket ID (DSA-X format). If not, prompts you to provide one and prepends it to your message.

**Example:**
```
You: "Implement binary search"
Hook: "What is the Jira ticket ID? (e.g., DSA-3)"
You: "3"
Result: "DSA-3 Implement binary search"
```

### 2. Jira Smart Commit - Log Completion
**ID:** `jira-commit-reminder`  
**Event:** `agentStop`  
**Action:** `askAgent`

After Kiro finishes a task, reminds you about Jira Smart Commit commands you can use in your next commit.

**Reminder includes:**
- `#done` — Mark ticket as done
- `#time Xh` — Log time spent
- `#comment <text>` — Add comment to ticket

### 3. DSA Progress Tracker
**ID:** `dsa-progress-tracker`  
**Event:** `fileEdited`  
**Action:** `runCommand`  
**Patterns:** `**/*.py`, `**/README.md`

Logs every time you save a Python file or README to `.kiro/progress.log`, creating a timestamped record of your work.

**Log format:**
```
File saved: algorithms/sorting/merge_sort.py at Mon Jan 15 14:30:22 PST 2024
File saved: algorithms/sorting/README.md at Mon Jan 15 14:35:18 PST 2024
```

## Managing Hooks

### View All Hooks

Hooks are stored in Kiro's configuration. To see all active hooks, check the Kiro settings or use the Kiro CLI:

```bash
# View hook status (if CLI available)
kiro hooks list
```

### Enable/Disable Hooks

Hooks are enabled by default when created. To disable a hook temporarily:

**Option 1: Through Kiro Settings**
1. Open Kiro settings
2. Navigate to "Hooks" section
3. Toggle the hook on/off

**Option 2: Through Configuration**
Edit the hook configuration file (location varies by Kiro installation):
```json
{
  "id": "jira-ticket-prepend",
  "enabled": false
}
```

### Delete a Hook

To permanently remove a hook:

**Option 1: Through Kiro Settings**
1. Open Kiro settings
2. Navigate to "Hooks" section
3. Delete the hook

**Option 2: Through CLI**
```bash
kiro hooks delete jira-ticket-prepend
```

## Customizing Hooks

### Modify Existing Hooks

To change a hook's behavior, you'll need to recreate it with updated parameters. For example, to change the Jira ticket pattern from "DSA-" to "PROJ-":

1. Delete the existing hook
2. Create a new hook with updated prompt:

```bash
# Using Kiro CLI or API
kiro hooks create \
  --id jira-ticket-prepend \
  --name "Jira Smart Commit - Add Ticket ID" \
  --event promptSubmit \
  --action askAgent \
  --prompt "Check if message starts with 'PROJ-' pattern..."
```

### Create Custom Hooks

You can create your own hooks for project-specific workflows. Examples:

**Auto-format Python files on save:**
```json
{
  "id": "auto-format-python",
  "name": "Auto Format Python",
  "event": "fileEdited",
  "patterns": "**/*.py",
  "action": "runCommand",
  "command": "black $FILE_PATH && isort $FILE_PATH"
}
```

**Remind about tests before committing:**
```json
{
  "id": "test-reminder",
  "name": "Test Reminder",
  "event": "promptSubmit",
  "action": "askAgent",
  "prompt": "If the user is about to commit, remind them to run tests first: python -m pytest"
}
```

**Log time spent on tasks:**
```json
{
  "id": "time-tracker",
  "name": "Time Tracker",
  "event": "preTaskExecution",
  "action": "runCommand",
  "command": "echo \"Task started: $(date)\" >> .kiro/time.log"
}
```

## Best Practices

1. **Keep prompts specific** — Clear instructions lead to better AI responses
2. **Use file patterns wisely** — Avoid triggering on every file change
3. **Test hooks incrementally** — Create one hook at a time and verify behavior
4. **Document custom hooks** — Add comments explaining why each hook exists
5. **Avoid infinite loops** — Don't create hooks that trigger themselves
6. **Consider performance** — Heavy commands on `fileEdited` can slow down your workflow

## Troubleshooting

### Hook Not Triggering

**Problem:** Hook doesn't activate when expected.

**Solutions:**
1. Verify the hook is enabled in settings
2. Check the event type matches your action
3. For file-based hooks, verify file patterns are correct
4. Check Kiro logs for error messages

**Debug file patterns:**
```bash
# Test if your file matches the pattern
# Pattern: **/*.py
# File: algorithms/sorting/merge_sort.py
# Should match: YES

# Pattern: **/README.md
# File: docs/project/README.md
# Should match: YES
```

### Hook Executing Too Often

**Problem:** Hook triggers on every minor change.

**Solutions:**
1. Narrow file patterns to specific directories
2. Use more specific event types
3. Add conditions in the prompt (for `askAgent` actions)
4. Consider using `userTriggered` instead of automatic events

**Example fix:**
```json
// Before: Triggers on ALL Python files
"patterns": "**/*.py"

// After: Only triggers on algorithm files
"patterns": "algorithms/**/*.py,data-structures/**/*.py"
```

### Agent Prompt Not Working as Expected

**Problem:** `askAgent` action doesn't produce desired results.

**Solutions:**
1. Make prompts more explicit and detailed
2. Include examples in the prompt
3. Break complex tasks into multiple hooks
4. Test the prompt directly with Kiro first

**Example improvement:**
```json
// Before: Vague prompt
"prompt": "Help with commit message"

// After: Specific instructions
"prompt": "Check if the commit message starts with 'DSA-' pattern. If not, ask the user for the Jira ticket ID (e.g., DSA-3). Prepend 'DSA-X ' to their message where X is the number they provide."
```

### Command Failing in runCommand

**Problem:** Shell command in `runCommand` action fails.

**Solutions:**
1. Test the command manually in terminal first
2. Check file paths are correct (use `$FILE_PATH` variable)
3. Ensure required tools are installed (e.g., `black`, `pytest`)
4. Check command syntax (no multi-line commands)
5. Verify permissions for file operations

**Debug commands:**
```bash
# Test command manually
echo "File saved: algorithms/sorting/merge_sort.py at $(date)" >> .kiro/progress.log

# Check if file is writable
touch .kiro/progress.log
ls -la .kiro/progress.log
```

### Progress Log Growing Too Large

**Problem:** `.kiro/progress.log` becomes huge over time.

**Solutions:**
1. Rotate logs periodically:
   ```bash
   mv .kiro/progress.log .kiro/progress.log.old
   ```

2. Modify hook to limit log size:
   ```bash
   # Keep only last 100 lines
   tail -n 100 .kiro/progress.log > .kiro/progress.log.tmp && mv .kiro/progress.log.tmp .kiro/progress.log
   ```

3. Add log rotation to a weekly cron job

## Hook Variables

When using `runCommand` actions, these variables are available:

| Variable | Description | Example |
|----------|-------------|---------|
| `$FILE_PATH` | Full path to the file | `algorithms/sorting/merge_sort.py` |
| `$FILE_NAME` | File name only | `merge_sort.py` |
| `$FILE_DIR` | Directory path | `algorithms/sorting` |
| `$WORKSPACE` | Workspace root | `/home/user/dsa-mastery` |

**Usage example:**
```bash
echo "Modified: $FILE_NAME in $FILE_DIR" >> .kiro/changes.log
```

## Integration with Jira Smart Commits

Agent Hooks complement Jira Smart Commits by:

1. **Ensuring ticket IDs are present** — The `jira-ticket-prepend` hook guarantees every commit has a ticket ID
2. **Reminding about commands** — The `jira-commit-reminder` hook keeps Smart Commit syntax fresh
3. **Tracking progress** — The `dsa-progress-tracker` hook creates an audit trail

**Complete workflow:**
```
1. Edit file → DSA Progress Tracker logs the change
2. Submit commit → Jira Ticket Prepend adds DSA-X prefix
3. Agent finishes → Jira Commit Reminder shows available commands
4. Push to remote → Jira processes Smart Commit commands
```

## Advanced Examples

### Multi-Step Workflow Hook

Create a hook that guides you through a complete task:

```json
{
  "id": "task-workflow-guide",
  "name": "Task Workflow Guide",
  "event": "preTaskExecution",
  "action": "askAgent",
  "prompt": "Guide the user through the DSA task workflow: 1) Check jira_plans.md for ticket details, 2) Create folder structure, 3) Generate README with Mermaid diagrams, 4) Implement code with tests, 5) Commit with Jira ticket ID. Ask which step they need help with."
}
```

### Code Quality Gate

Prevent commits without tests:

```json
{
  "id": "require-tests",
  "name": "Require Tests",
  "event": "promptSubmit",
  "action": "askAgent",
  "prompt": "If the user is committing Python code, check if corresponding test files exist. If not, remind them to add tests before committing. Look for test_*.py or *_test.py files."
}
```

### Automatic Documentation

Generate docstrings when creating new functions:

```json
{
  "id": "auto-docstring",
  "name": "Auto Docstring",
  "event": "fileCreated",
  "patterns": "**/*.py",
  "action": "askAgent",
  "prompt": "Scan the newly created Python file for functions without docstrings. Suggest adding docstrings with parameter descriptions, return types, and complexity analysis."
}
```

## Migration from Git Hooks

If you're migrating from traditional Git hooks to Kiro Agent Hooks:

**Old Git Hook (prepare-commit-msg):**
```bash
#!/bin/bash
# Prepend ticket ID to commit message
COMMIT_MSG_FILE=$1
COMMIT_MSG=$(cat "$COMMIT_MSG_FILE")

if [[ ! $COMMIT_MSG =~ ^DSA- ]]; then
    read -p "Enter Jira ticket ID: " TICKET_ID
    echo "DSA-$TICKET_ID $COMMIT_MSG" > "$COMMIT_MSG_FILE"
fi
```

**New Agent Hook:**
```json
{
  "id": "jira-ticket-prepend",
  "event": "promptSubmit",
  "action": "askAgent",
  "prompt": "Check if message starts with 'DSA-'. If not, ask for ticket ID and prepend 'DSA-X ' to the message."
}
```

**Benefits of migration:**
- No shell scripting required
- Works across all platforms (Windows, Mac, Linux)
- More intelligent and context-aware
- Easier to modify and maintain
- Better error handling and user feedback

## Resources

- [Workflow Guide](./workflow-guide.md) — Complete DSA task workflow
- [Jira Plans](./jira_plans.md) — Task tracking
- [Project Execution Plans](../../project_execution_plans.md) — Content standards
- [Kiro Documentation](https://kiro.dev/docs) — Official Kiro docs
- [Jira Smart Commits](https://support.atlassian.com/jira-software-cloud/docs/process-issues-with-smart-commits/) — Jira integration

## Support

If you encounter issues with Agent Hooks:

1. Check this troubleshooting guide first
2. Review Kiro logs for error messages
3. Test hooks individually to isolate problems
4. Consult Kiro documentation
5. Ask Kiro directly: "Help me debug my agent hook"

---

**Last Updated:** 2024-01-15  
**Version:** 1.0.0
