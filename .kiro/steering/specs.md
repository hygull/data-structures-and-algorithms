---
inclusion: auto
---

# Spec and Task Guidelines

This document defines the standards for creating content in the DSA Mastery repository.

## Folder Architecture

```
dsa-mastery/
├── README.md                          # Main index, roadmap, progress tracker
├── CONTRIBUTING.md
├── LICENSE
├── foundations/                       # Big-O, recursion, bit manipulation
├── data-structures/                   # Arrays, linked lists, trees, graphs, etc.
├── algorithms/                        # Sorting, searching, DP, graph algorithms
├── patterns/                          # Interview pattern playbook
├── problems/                          # Solved problems (LeetCode, Neetcode-150)
├── cheat-sheets/                      # Quick reference guides
└── templates/                         # Reusable templates
```

## README Template Requirements

### Topic README (for data structures/algorithms)

Every topic folder must contain a README.md with:

1. **What Is It?** - 2-3 sentence definition explaining the problem it solves and why it exists
2. **Visual Representation** - At least 1 Mermaid diagram (2+ for complex topics)
3. **Core Operations & Complexity** - Complete table with Best/Average/Worst time and Space complexity
4. **How It Works** - Step-by-step breakdown with Mermaid diagrams
5. **When to Use It** - Interview intuition with signal words and pairing suggestions
6. **Key Patterns & Variations** - Common sub-types seen in interviews
7. **Common Pitfalls & Edge Cases** - At least 3-5 specific edge cases
8. **Implementation** - Link to code file
9. **Must-Solve Problems** - 5-10 curated problems with difficulty and pattern tags
10. **References & Further Reading** - Links to authoritative sources

### Problem README (for individual problems)

Every problem folder must contain a README.md with:

1. **Metadata Table** - Source, difficulty, topics, companies, pattern, link
2. **Problem Statement** - Concise restatement with input/output format and examples
3. **Approach 1** - Brute force with intuition, Mermaid diagram, and complexity analysis
4. **Approach 2** - Optimal solution with intuition, Mermaid diagram, and complexity analysis
5. **Key Takeaways** - Pattern learned, similar problems, tricky edge cases

### Code Template

All Python files must follow this structure:

```python
"""
Topic/Problem: [Name]
Category:      [Data Structure / Algorithm / Problem]
Complexity:    Time O(?)  |  Space O(?)
Author:        [Your Name]
Date:          [Date]

Description:
    [Brief description]

References:
    - [Link to problem or theory]
"""

from typing import List, Optional

class Solution:
    """
    Approach: [Name]
    
    Intuition:
        [1-2 sentences]
    
    Algorithm:
        1. [Step 1]
        2. [Step 2]
    
    Complexity:
        Time:  O(n) — [reason]
        Space: O(n) — [reason]
    """
    
    def solve(self, nums: List[int], target: int) -> List[int]:
        pass

# Tests
if __name__ == "__main__":
    s = Solution()
    assert s.solve([2, 7, 11, 15], 9) == [0, 1], "Test 1 Failed"
    print("✅ All tests passed!")
```

## Mermaid Diagram Standards

Use these diagram types consistently:

| Use Case                     | Mermaid Type       | Example Context                |
| ---------------------------- | ------------------ | ------------------------------ |
| Data structure layout        | `graph LR` or `TD` | Linked list, tree, graph       |
| Algorithm step-by-step flow  | `flowchart TD`     | Sorting, searching logic       |
| State transitions            | `stateDiagram-v2`  | DFA, DP state machines         |
| Process interaction          | `sequenceDiagram`  | How operations modify structure|
| Comparison / taxonomy        | `mindmap`          | Algorithm family tree          |
| Timeline of operations       | `gantt`            | Algorithm execution timeline   |

All diagrams must render correctly on GitHub (use GitHub-native Mermaid, no external images).

## Content Depth Requirements

Each topic must be both a learning resource and a quick-reference cheat sheet:

| Section                   | Depth                                                      |
| ------------------------- | ---------------------------------------------------------- |
| **Definition**            | 2-3 sentences. No fluff.                                   |
| **Visual**                | At least 1 Mermaid diagram. 2+ for complex topics.        |
| **Complexity Table**      | Every operation. Best / Average / Worst / Space.           |
| **Step-by-Step**          | Numbered. With diagram. Trace through a small example.     |
| **Interview Intuition**   | When to recognize it. Signal words. What it pairs with.    |
| **Patterns & Variations** | Sub-types (e.g., Binary Search: classic, on-answer, rotated)|
| **Edge Cases**            | At least 3-5 edge cases with brief explanations.           |
| **Must-Solve Problems**   | 5-10 curated problems with difficulty + pattern tags.      |
| **Code Implementation**   | Clean Python. Type hints. Docstrings. Test cases.         |

## Coding Standards

| Rule                         | Detail                                                     |
| ---------------------------- | ---------------------------------------------------------- |
| **Type Hints**               | All function signatures use Python type hints              |
| **Docstrings**               | Every class and method has a docstring                     |
| **Naming**                   | `snake_case` for files/functions, `PascalCase` for classes|
| **Tests**                    | Every file has `if __name__ == "__main__":` with assertions|
| **No External Dependencies** | stdlib only (unless explicitly noted)                      |
| **Comments**                 | Explain *why*, not *what*                                  |

## Commit Message Format

All commits to this repository must follow the Jira Smart Commit format to enable automatic tracking and integration with Jira.

### Required Format

```
DSA-X <descriptive commit message>
```

Where `X` is the Jira ticket number from `docs/project/jira_plans.md`.

### Examples

**Good commit messages:**
```
DSA-3 Add binary search implementation with test cases
DSA-7 Fix edge case in merge sort for single element arrays
DSA-12 Update complexity analysis in AVL tree README
DSA-5 Implement heap operations #time 2h #done
```

**Bad commit messages:**
```
Add binary search          ❌ Missing ticket ID
DSA-3: Add implementation  ❌ Using colon instead of space
Fixed bug                  ❌ Missing ticket ID and unclear message
```

### Git Hook Integration

A Git hook is installed at `.git/hooks/prepare-commit-msg` that automatically prompts for the Jira ticket ID if your commit message doesn't already include it.

**Usage:**
```bash
$ git commit -m "Add binary search implementation"

🎫 Jira Smart Commit Helper
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Enter Jira ticket ID (e.g., DSA-3) or press Enter to skip: 3

✅ Commit message updated: DSA-3: ...
```

**Bypass the hook** (for trivial commits):
```bash
git commit --no-verify -m "Fix typo in README"
```

### Jira Smart Commit Commands

Enhance your commits with Jira commands:

| Command | Effect | Example |
|---------|--------|---------|
| `#done` | Transition ticket to Done | `DSA-3 Complete implementation #done` |
| `#time Xh` | Log work time | `DSA-5 Add tests #time 2h` |
| `#comment <text>` | Add comment to ticket | `DSA-7 Fix bug #comment Resolved edge case` |

**Combined commands:**
```bash
git commit -m "DSA-10 Complete heap implementation #time 3h #done"
```

### References

For detailed information on the Git hook setup and troubleshooting, see:
- [Git Hooks Guide](../../docs/git/commit-hooks-guide.md)
- [Workflow Guide](../../docs/project/workflow-guide.md)

---

## Quality Checklist (Per Topic)

Before marking a topic complete, verify:

- [ ] README.md follows the template exactly
- [ ] At least 2 Mermaid diagrams render correctly on GitHub
- [ ] Complexity table is fully filled (no blanks)
- [ ] Step-by-step walkthrough traces through a concrete example
- [ ] Interview intuition section has signal words and pairing suggestions
- [ ] 3+ edge cases listed
- [ ] 5+ curated problems with difficulty and pattern tags
- [ ] Code file has type hints, docstrings, and passing test cases
- [ ] No broken links
- [ ] Consistent formatting with the rest of the repo
- [ ] All commits use proper Jira ticket format: `DSA-X <message>`
