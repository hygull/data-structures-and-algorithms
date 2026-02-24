# 🔄 DSA Mastery Workflow Guide

## Overview

This guide walks you through the complete workflow for working on a DSA task, from picking a ticket in Jira to pushing your completed work with proper commit messages.

**🤖 Powered by Kiro Agent Hooks:** This workflow uses intelligent Kiro Agent Hooks to automate Jira ticket ID management and provide helpful reminders. See the [Agent Hooks Guide](./agent-hooks-guide.md) for details on how these work.

## Step-by-Step Workflow

### Step 1: Pick a Task from Jira Plans

1. Open `docs/project/jira_plans.md`
2. Find a task with status `To Do` or `In Progress`
3. Note the ticket ID (e.g., `DSA-3`)
4. Review the task description and acceptance criteria

**Example:**
```markdown
| DSA-3 | Binary Search | Implement binary search with README | To Do | 2024-01-15 |
```

### Step 2: Update Task Status in Jira

Mark the task as "In Progress" in Jira:
- Via Jira UI: Drag the ticket to "In Progress" column
- Via Git commit: Include `#in-progress` in your first commit (see Step 6)

### Step 3: Identify the Folder Structure

Based on the task category, determine where your files will go:

**Python Built-ins** → `02-python-built-ins/XX-topic/`
```
02-python-built-ins/04-sets/
├── README.md
└── sets.py
```

**Collections Module** → `03-python-collections/XX-topic/`
```
03-python-collections/01-deque/
├── README.md
└── deque_usage.py
```

**Data Structures** → `05-data-structures/XX-topic/`
```
05-data-structures/02-linked-lists/
├── README.md
├── singly_linked_list.py
├── doubly_linked_list.py
└── circular_linked_list.py
```

**Algorithms** → `06-algorithms/category/`
```
06-algorithms/sorting/
├── README.md
├── bubble_sort.py
├── merge_sort.py
└── quick_sort.py
```

**Problems** → `08-problems/source/XXXX-problem-name/`
```
08-problems/leetcode/0001-two-sum/
├── README.md
└── solution.py
```

### Step 4: Create the Folder Structure

Create the necessary folders:

```bash
# Example for binary search (DSA-3)
mkdir -p 06-algorithms/searching
cd 06-algorithms/searching
```

### Step 5: Generate Content Following the SPEC

Follow the templates from `project_execution_plans.md`:

#### For Topic README.md

1. **Start with a Mermaid diagram** (not text)
2. **What Is It?** — 1 sentence, max 20 words
3. **Structure** — Mermaid diagram showing the data structure
4. **Real-World Analogy** — 1 sentence
5. **Python Built-in Way** — Show native Python approach first
6. **Operations at a Glance** — Complete complexity table
7. **Step-by-Step** — Before/after Mermaid diagrams for each operation
8. **When to Use It** — 2-column table
9. **Edge Cases** — At least 3-5 cases
10. **Implementation** — Link to code file
11. **Practice Problems** — 5-10 problems with difficulty and key insight

#### For Code Files (.py)

1. **Docstring header** with topic, category, complexity
2. **Python built-in demo** function (if applicable)
3. **Custom implementation** class with type hints
4. **Tests** in `if __name__ == "__main__":` block

**Template:**
```python
"""
Topic:      Binary Search
Category:   Algorithm
Python:     3.12+

Complexity:
    search(): Time O(log n) | Space O(1)
"""

from typing import List

def builtin_example() -> None:
    """Show how Python handles this natively."""
    import bisect
    nums = [1, 3, 5, 7, 9]
    idx = bisect.bisect_left(nums, 5)
    print(f"Found at index: {idx}")

class BinarySearch:
    """
    Binary search implementation.
    
    Operations:
        search(arr, target): O(log n) time, O(1) space
    """
    
    def search(self, arr: List[int], target: int) -> int:
        """Find target in sorted array. Returns index or -1."""
        left, right = 0, len(arr) - 1
        
        while left <= right:
            mid = left + (right - left) // 2
            
            if arr[mid] == target:
                return mid
            elif arr[mid] < target:
                left = mid + 1
            else:
                right = mid - 1
        
        return -1

if __name__ == "__main__":
    print("=== Python Built-in ===")
    builtin_example()
    
    print("\n=== Custom Implementation ===")
    bs = BinarySearch()
    
    # Test 1: Normal case
    assert bs.search([1, 3, 5, 7, 9], 5) == 2, "Test 1 failed"
    
    # Test 2: Not found
    assert bs.search([1, 3, 5, 7, 9], 6) == -1, "Test 2 failed"
    
    # Test 3: Edge case — empty array
    assert bs.search([], 5) == -1, "Test 3 failed"
    
    # Test 4: Edge case — single element
    assert bs.search([5], 5) == 0, "Test 4 failed"
    
    print("✅ All tests passed!")
```

### Step 6: Commit Your Work with Jira Ticket ID

The Kiro Agent Hook will automatically prompt for the ticket ID when you submit a commit:

```bash
git add .
git commit -m "Implement binary search with README and tests"

# Kiro Agent Hook prompts:
🤖 Jira Smart Commit - Add Ticket ID
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
What is the Jira ticket ID for this commit? (e.g., DSA-3, or press Enter to skip): 3

✅ Commit message updated to: DSA-3 Implement binary search with README and tests
```

**Result:** Commit message becomes `DSA-3 Implement binary search with README and tests`

#### Using Jira Smart Commit Commands

Enhance your commits with Jira commands:

**Mark as done:**
```bash
git commit -m "Complete binary search implementation #done"
# Agent Hook adds: DSA-3 Complete binary search implementation #done
```

**Log time:**
```bash
git commit -m "Add comprehensive test cases #time 1h"
# Agent Hook adds: DSA-3 Add comprehensive test cases #time 1h
```

**Add comment:**
```bash
git commit -m "Fix edge case #comment Handled empty array scenario"
# Agent Hook adds: DSA-3 Fix edge case #comment Handled empty array scenario
```

**Combined:**
```bash
git commit -m "Complete implementation with all tests #time 3h #done"
# Agent Hook adds: DSA-3 Complete implementation with all tests #time 3h #done
```

### Step 7: Verify Your Work

Before pushing, verify:

1. **README.md checklist:**
   - [ ] Opens with Mermaid diagram (not text)
   - [ ] No text block exceeds 3 sentences
   - [ ] Python built-in way shown first
   - [ ] Every operation has before/after Mermaid diagrams
   - [ ] Complexity table is fully filled
   - [ ] 3+ edge cases listed
   - [ ] 5+ practice problems with key insights

2. **Code file checklist:**
   - [ ] Type hints on all functions
   - [ ] Docstrings on all classes and methods
   - [ ] Built-in demo function (if applicable)
   - [ ] Custom implementation class
   - [ ] Tests in `if __name__ == "__main__":` block
   - [ ] All tests pass: `python filename.py`

3. **Commit message checklist:**
   - [ ] Starts with `DSA-X` format (space, not colon)
   - [ ] Descriptive message (not just "update" or "fix")
   - [ ] Includes Jira commands if applicable (`#done`, `#time`, etc.)

**Run tests:**
```bash
python 06-algorithms/searching/binary_search.py
```

**Check commit log:**
```bash
git log --oneline -5
```

Expected output:
```
a1b2c3d DSA-3 Complete binary search implementation #time 3h #done
e4f5g6h DSA-3 Add comprehensive test cases
i7j8k9l DSA-3 Create README with Mermaid diagrams
```

### Step 8: Push to Remote

Push your changes:

```bash
git push origin main
```

Or if working on a feature branch:

```bash
git checkout -b DSA-3-binary-search
git push origin DSA-3-binary-search
```

### Step 9: Verify Jira Integration

1. Open the Jira ticket (DSA-3)
2. Check the "Development" section — your commits should appear
3. If you used `#done`, verify the ticket moved to "Done" status
4. If you used `#time`, verify the time was logged

**Troubleshooting:**
- Commits not showing? Wait 2-3 minutes for Jira sync
- Still not showing? Verify your Git email matches your Jira account
- Status not updated? Check Jira workflow allows the transition

### Step 10: Update Jira Plans Document

Update `docs/project/jira_plans.md`:

```markdown
| DSA-3 | Binary Search | Implement binary search with README | Done | 2024-01-15 | 2024-01-16 |
```

Commit the update:
```bash
git add docs/project/jira_plans.md
git commit -m "DSA-3 Update Jira plans with completion status"
git push
```

## Quick Reference

### Folder Structure by Category

| Category | Path | Example |
|----------|------|---------|
| Foundations | `01-foundations/topic/` | `01-foundations/big-o-notation/` |
| Python Built-ins | `02-python-built-ins/XX-topic/` | `02-python-built-ins/04-sets/` |
| Collections | `03-python-collections/XX-topic/` | `03-python-collections/01-deque/` |
| Heapq/Bisect | `04-heapq-and-bisect/XX-topic/` | `04-heapq-and-bisect/01-heapq/` |
| Data Structures | `05-data-structures/XX-topic/` | `05-data-structures/02-linked-lists/` |
| Algorithms | `06-algorithms/category/` | `06-algorithms/sorting/` |
| Patterns | `07-patterns/` | `07-patterns/fast-and-slow-pointers.md` |
| Problems | `08-problems/source/XXXX-name/` | `08-problems/leetcode/0001-two-sum/` |

### Commit Message Format

```
DSA-X <descriptive message> [#command]
```

**Commands:**
- `#done` — Mark ticket as done
- `#time Xh` — Log X hours of work
- `#comment <text>` — Add comment to ticket
- `#in-progress` — Move to in progress

### Common Git Commands

```bash
# Check status
git status

# Stage all changes
git add .

# Commit (hook will prompt for ticket ID)
git commit -m "Your message"

# Commit without hook (for trivial changes)
git commit --no-verify -m "Fix typo"

# View recent commits
git log --oneline -5

# Amend last commit message
git commit --amend

# Push to remote
git push origin main
```

## Example: Complete Workflow for DSA-3 (Binary Search)

```bash
# Step 1: Check jira_plans.md and pick DSA-3

# Step 2: Create folder structure
mkdir -p 06-algorithms/searching
cd 06-algorithms/searching

# Step 3: Create README.md
# (Use your editor to create content following SPEC)

# Step 4: Create binary_search.py
# (Use your editor to create code following template)

# Step 5: Test your code
python binary_search.py
# Output: ✅ All tests passed!

# Step 6: Commit with Jira ticket
git add .
git commit -m "Create README with Mermaid diagrams"
# Kiro Agent Hook prompts: Enter ticket ID: 3
# Result: DSA-3 Create README with Mermaid diagrams

git add .
git commit -m "Implement binary search with test cases"
# Kiro Agent Hook prompts: Enter ticket ID: 3
# Result: DSA-3 Implement binary search with test cases

git add .
git commit -m "Add edge case handling and documentation #time 3h #done"
# Kiro Agent Hook prompts: Enter ticket ID: 3
# Result: DSA-3 Add edge case handling and documentation #time 3h #done

# Step 7: Push to remote
git push origin main

# Step 8: Verify in Jira
# - Open DSA-3 ticket
# - Check commits appear in Development section
# - Verify ticket moved to Done
# - Verify 3 hours logged

# Step 9: Update jira_plans.md
# (Edit the file to mark DSA-3 as Done)
git add docs/project/jira_plans.md
git commit -m "DSA-3 Update Jira plans with completion status"
git push
```

## Tips for Success

1. **Always start with the Mermaid diagram** — Visual first, text second
2. **Keep explanations under 3 sentences** — No walls of text
3. **Show Python's built-in way first** — Then custom implementation
4. **Test before committing** — Run `python filename.py` to verify
5. **Use descriptive commit messages** — Not just "update" or "fix"
6. **Leverage Jira Smart Commits** — Use `#done`, `#time`, `#comment`
7. **Review before pushing** — Check `git log --oneline` for proper format
8. **Update jira_plans.md** — Keep the tracking document current

## Troubleshooting

### Agent Hook Not Prompting

**Problem:** Kiro Agent Hook doesn't ask for ticket ID.

**Solution:**
1. Verify the hook is enabled in Kiro settings
2. Check Kiro is running and connected
3. Review the [Agent Hooks Guide](./agent-hooks-guide.md) for troubleshooting
4. Test the hook manually by asking Kiro to check your commit message

### Tests Failing

**Problem:** `python filename.py` shows assertion errors.

**Solution:**
1. Read the error message carefully
2. Check your implementation logic
3. Verify edge cases are handled
4. Add debug print statements
5. Test with simple inputs first

### Commits Not Showing in Jira

**Problem:** Commits with `DSA-X` don't appear in Jira.

**Solution:**
1. Wait 2-3 minutes for sync
2. Verify Git email matches Jira account: `git config user.email`
3. Check repository is connected to Jira (requires admin)
4. Verify ticket ID exists in Jira

### Mermaid Diagrams Not Rendering

**Problem:** Diagrams show as code blocks on GitHub.

**Solution:**
1. Ensure you're using triple backticks with `mermaid` language tag:
   ````markdown
   ```mermaid
   graph LR
       A --> B
   ```
   ````
2. Test on GitHub's Mermaid Live Editor first
3. Avoid unsupported Mermaid features

## References

- [Project Execution Plans](../../project_execution_plans.md) — Complete SPEC v3
- [Specs Steering Document](../../.kiro/steering/specs.md) — Content standards
- [Structure Steering Document](../../.kiro/steering/structure.md) — Folder architecture
- [Agent Hooks Guide](./agent-hooks-guide.md) — Kiro Agent Hooks setup and troubleshooting
- [Git Hooks Guide](../git/commit-hooks-guide.md) — Traditional Git hooks (legacy)
- [Jira Plans](./jira_plans.md) — Task tracking
- [Jira Smart Commits Documentation](https://support.atlassian.com/jira-software-cloud/docs/process-issues-with-smart-commits/)
