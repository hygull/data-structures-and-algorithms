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
├── 01-foundations/
│   ├── big-o-notation/
│   │   ├── README.md                 # Time & Space complexity deep-dive
│   │   └── examples.py
│   ├── recursion/
│   │   ├── README.md
│   │   └── recursion.py
│   └── bit-manipulation/
│       ├── README.md
│       └── bit_tricks.py
│
├── 02-python-built-ins/
│   ├── 01-lists/
│   │   ├── README.md                 # Theory + Mermaid + Complexity Table
│   │   └── lists.py
│   ├── 02-tuples/
│   │   ├── README.md
│   │   └── tuples.py
│   ├── 03-strings/
│   │   ├── README.md
│   │   └── strings.py
│   ├── 04-sets/
│   │   ├── README.md
│   │   └── sets.py
│   ├── 05-frozensets/
│   │   ├── README.md
│   │   └── frozensets.py
│   ├── 06-dictionaries/
│   │   ├── README.md
│   │   └── dicts.py
│   └── 07-booleans-and-none/
│       ├── README.md
│       └── truthy_falsy.py
│
├── 03-python-collections/
│   ├── 01-deque/
│   │   ├── README.md
│   │   └── deque_usage.py
│   ├── 02-counter/
│   │   ├── README.md
│   │   └── counter_usage.py
│   ├── 03-defaultdict/
│   │   ├── README.md
│   │   └── defaultdict_usage.py
│   ├── 04-ordereddict/
│   │   ├── README.md
│   │   └── ordereddict_usage.py
│   └── 05-namedtuple/
│       ├── README.md
│       └── namedtuple_usage.py
│
├── 04-heapq-and-bisect/
│   ├── 01-heapq/
│   │   ├── README.md
│   │   └── heapq_usage.py
│   └── 02-bisect/
│       ├── README.md
│       └── bisect_usage.py
│
├── 05-data-structures/
│   ├── 01-arrays/
│   │   ├── README.md
│   │   └── arrays.py
│   ├── 02-linked-lists/
│   │   ├── README.md
│   │   ├── singly_linked_list.py
│   │   ├── doubly_linked_list.py
│   │   └── circular_linked_list.py
│   ├── 03-stacks/
│   │   ├── README.md
│   │   └── stack.py
│   ├── 04-queues/
│   │   ├── README.md
│   │   ├── queue.py
│   │   ├── circular_queue.py
│   │   └── priority_queue.py
│   ├── 05-hash-tables/
│   │   ├── README.md
│   │   ├── hash_table_chaining.py
│   │   ├── hash_table_open_addressing.py
│   │   └── hash_set.py
│   ├── 06-trees/
│   │   ├── binary-tree/
│   │   │   ├── README.md
│   │   │   └── binary_tree.py
│   │   ├── binary-search-tree/
│   │   │   ├── README.md
│   │   │   └── bst.py
│   │   ├── avl-tree/
│   │   │   ├── README.md
│   │   │   └── avl.py
│   │   ├── red-black-tree/
│   │   │   └── README.md              # Conceptual only
│   │   └── trie/
│   │       ├── README.md
│   │       └── trie.py
│   ├── 07-heaps/
│   │   ├── README.md
│   │   ├── min_heap.py
│   │   └── max_heap.py
│   ├── 08-graphs/
│   │   ├── README.md
│   │   ├── adjacency_list.py
│   │   ├── adjacency_matrix.py
│   │   └── edge_list.py
│   ├── 09-union-find/
│   │   ├── README.md
│   │   └── union_find.py
│   ├── 10-segment-tree/
│   │   ├── README.md
│   │   └── segment_tree.py
│   ├── 11-fenwick-tree/
│   │   ├── README.md
│   │   └── fenwick_tree.py
│   ├── 12-monotonic-stack/
│   │   ├── README.md
│   │   └── monotonic_stack.py
│   ├── 13-monotonic-queue/
│   │   ├── README.md
│   │   └── monotonic_queue.py
│   ├── 14-lru-cache/
│   │   ├── README.md
│   │   └── lru_cache.py
│   ├── 15-lfu-cache/
│   │   ├── README.md
│   │   └── lfu_cache.py
│   ├── 16-skip-list/
│   │   ├── README.md
│   │   └── skip_list.py
│   └── 17-bloom-filter/
│       └── README.md                  # Conceptual only
│
├── 06-algorithms/
│   ├── sorting/
│   │   ├── README.md                 # Comparative analysis + Mermaid
│   │   ├── bubble_sort.py
│   │   ├── selection_sort.py
│   │   ├── insertion_sort.py
│   │   ├── merge_sort.py
│   │   ├── quick_sort.py
│   │   ├── heap_sort.py
│   │   ├── counting_sort.py
│   │   └── radix_sort.py
│   ├── searching/
│   │   ├── README.md
│   │   ├── linear_search.py
│   │   └── binary_search.py
│   ├── two-pointers/
│   │   ├── README.md
│   │   └── two_pointers.py
│   ├── sliding-window/
│   │   ├── README.md
│   │   └── sliding_window.py
│   ├── divide-and-conquer/
│   │   ├── README.md
│   │   └── examples.py
│   ├── greedy/
│   │   ├── README.md
│   │   └── examples.py
│   ├── dynamic-programming/
│   │   ├── README.md
│   │   └── patterns/
│   │       ├── knapsack.md
│   │       ├── longest-common-subsequence.md
│   │       ├── interval-scheduling.md
│   │       └── state-machine.md
│   ├── backtracking/
│   │   ├── README.md
│   │   └── backtracking.py
│   └── graph-algorithms/
│       ├── README.md
│       ├── bfs.py
│       ├── dfs.py
│       ├── dijkstra.py
│       ├── bellman_ford.py
│       ├── topological_sort.py
│       ├── kruskal.py
│       └── prim.py
│
├── 07-patterns/                       # Interview pattern playbook
│   ├── README.md                      # Master index of all patterns
│   ├── fast-and-slow-pointers.md
│   ├── merge-intervals.md
│   ├── top-k-elements.md
│   ├── binary-search-variations.md
│   ├── tree-bfs-dfs.md
│   ├── subsets-permutations.md
│   └── monotonic-stack-patterns.md
│
├── 08-problems/                       # Solved problems organized by source
│   ├── README.md                      # Progress tracker table
│   ├── leetcode/
│   │   ├── 0001-two-sum/
│   │   │   ├── README.md             # Problem statement, approach, complexity
│   │   │   └── solution.py
│   │   └── 0003-longest-substring/
│   │       ├── README.md
│   │       └── solution.py
│   ├── neetcode-150/                  # Curated list tracking
│   │   └── README.md
│   └── company-tagged/
│       ├── google/
│       ├── meta/
│       └── amazon/
│
├── cheat-sheets/
│   ├── complexity-cheat-sheet.md      # Master Big-O reference
│   ├── python-dsa-tricks.md           # Language-specific tips
│   ├── common-mistakes.md
│   └── interview-tips.md
│
├── templates/
│   ├── topic-template.md              # Reusable template for each topic
│   ├── problem-template.md            # Reusable template for each problem
│   └── code-template.py               # Boilerplate with docstrings
│
└── docs/
    ├── git/
    │   ├── commit-hooks-guide.md      # Git hooks for Jira Smart Commits
    │   └── fix_committer.md           # Git configuration guide
    └── project/
        ├── jira_plans.md              # Jira ticket tracking and planning
        └── workflow-guide.md          # Step-by-step workflow for DSA tasks
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
