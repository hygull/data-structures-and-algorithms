---
inclusion: auto
---

# Project Structure

## Complete Folder Architecture

```
dsa-mastery/
│
├── README.md                          # Main index, roadmap, progress tracker
├── CONTRIBUTING.md                    # Contribution guidelines
├── LICENSE
│
├── foundations/
│   ├── big-o-notation/
│   │   └── README.md                 # Time & Space complexity deep-dive
│   ├── recursion/
│   │   └── README.md
│   └── bit-manipulation/
│       └── README.md
│
├── data-structures/
│   ├── arrays/
│   │   ├── README.md                 # Theory + Mermaid + Complexity Table
│   │   ├── dynamic_array.py
│   │   └── problems.md               # Curated problems list
│   ├── strings/
│   ├── linked-lists/
│   │   ├── README.md
│   │   ├── singly_linked_list.py
│   │   ├── doubly_linked_list.py
│   │   └── problems.md
│   ├── stacks/
│   ├── queues/
│   ├── hash-tables/
│   ├── heaps/
│   ├── trees/
│   │   ├── binary-tree/
│   │   ├── binary-search-tree/
│   │   ├── avl-tree/
│   │   ├── segment-tree/
│   │   ├── fenwick-tree/
│   │   └── trie/
│   ├── graphs/
│   │   ├── README.md
│   │   ├── adjacency_list.py
│   │   ├── adjacency_matrix.py
│   │   └── problems.md
│   ├── union-find/
│   └── advanced/
│       ├── monotonic-stack/
│       ├── monotonic-queue/
│       └── lru-cache/
│
├── algorithms/
│   ├── sorting/
│   │   ├── README.md                 # Comparative analysis + Mermaid
│   │   ├── bubble_sort.py
│   │   ├── merge_sort.py
│   │   ├── quick_sort.py
│   │   └── problems.md
│   ├── searching/
│   │   ├── binary_search.py
│   │   └── README.md
│   ├── two-pointers/
│   ├── sliding-window/
│   ├── divide-and-conquer/
│   ├── greedy/
│   ├── dynamic-programming/
│   │   ├── README.md                 # Pattern taxonomy
│   │   ├── patterns/
│   │   │   ├── knapsack.md
│   │   │   ├── longest-common-subsequence.md
│   │   │   ├── interval-scheduling.md
│   │   │   └── state-machine.md
│   │   └── problems.md
│   ├── backtracking/
│   ├── graph-algorithms/
│   │   ├── bfs.py
│   │   ├── dfs.py
│   │   ├── dijkstra.py
│   │   ├── topological_sort.py
│   │   └── README.md
│   └── advanced/
│       ├── kmp.py
│       └── README.md
│
├── patterns/                          # Interview pattern playbook
│   ├── README.md                      # Master index of all patterns
│   ├── fast-and-slow-pointers.md
│   ├── merge-intervals.md
│   ├── top-k-elements.md
│   ├── binary-search-variations.md
│   ├── tree-bfs-dfs.md
│   ├── subsets-permutations.md
│   └── monotonic-stack-patterns.md
│
├── problems/                          # Solved problems organized by source
│   ├── README.md                      # Progress tracker table
│   ├── leetcode/
│   │   ├── 0001-two-sum/
│   │   │   ├── README.md             # Problem statement, approach, complexity
│   │   │   └── solution.py
│   │   └── 0003-longest-substring/
│   ├── neetcode-150/                  # Curated list tracking
│   │   └── README.md
│   └── company-tagged/
│       ├── google/
│       ├── meta/
│       └── amazon/
│
├── cheat-sheets/
│   ├── complexity-cheat-sheet.md      # Master Big-O reference
│   ├── python-tricks-for-dsa.md       # Language-specific tips
│   ├── common-mistakes.md
│   └── interview-tips.md
│
└── templates/
    ├── topic-readme-template.md       # Reusable template for each topic
    ├── problem-readme-template.md     # Reusable template for each problem
    └── code-template.py               # Boilerplate with docstrings
```

## Naming Conventions

- **Folders**: `kebab-case` (e.g., `linked-lists/`, `dynamic-programming/`)
- **Python files**: `snake_case` (e.g., `singly_linked_list.py`, `merge_sort.py`)
- **Classes**: `PascalCase` (e.g., `Solution`, `LinkedList`)
- **Functions/methods**: `snake_case` (e.g., `def solve()`, `def insert_node()`)
- **Problem folders**: `0001-problem-name/` (zero-padded number + kebab-case name)

## File Organization Rules

- Each topic folder contains: `README.md`, implementation files, and `problems.md`
- Each problem folder contains: `README.md` and `solution.py`
- All Mermaid diagrams are embedded in markdown (no external image files)
- Templates are stored in `/templates/` for consistency
