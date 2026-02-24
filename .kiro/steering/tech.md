---
inclusion: auto
---

# Technical Stack

## Language Requirements

**Python 3.12+** - chosen for:
- Readability and widespread use in technical interviews
- Modern type hinting features (PEP 695 - Type Parameter Syntax)
- Performance improvements and better error messages
- Industry standard for algorithm education

## Dependency Policy

**Stdlib-only** - No external dependencies unless explicitly noted. This ensures:
- Code runs anywhere Python 3.12+ is installed
- Interview-ready implementations (can't use external libraries in interviews)
- Focus on fundamental algorithms, not library usage
- Minimal setup friction for learners

## Code Quality Standards

### Type Hints (Required)
- All function signatures must use Python type hints
- Use `typing` module for complex types: `List`, `Optional`, `Dict`, `Tuple`, etc.
- Example: `def solve(self, nums: List[int], target: int) -> List[int]:`

### Docstrings (Required)
- Every class and method must have a docstring
- Include: approach name, intuition, algorithm steps, complexity analysis
- Format:
  ```python
  """
  Approach: [Name]
  
  Intuition:
      [1-2 sentences on why this works]
  
  Algorithm:
      1. [Step 1]
      2. [Step 2]
  
  Complexity:
      Time:  O(n) — [reason]
      Space: O(n) — [reason]
  """
  ```

### Naming Conventions
- **Files**: `snake_case` (e.g., `merge_sort.py`, `binary_search_tree.py`)
- **Classes**: `PascalCase` (e.g., `Solution`, `LinkedList`, `BinaryTree`)
- **Functions/Methods**: `snake_case` (e.g., `def solve()`, `def insert_node()`)
- **Constants**: `UPPER_SNAKE_CASE` (e.g., `MAX_SIZE`, `DEFAULT_CAPACITY`)

### Testing Approach
- Every implementation file includes `if __name__ == "__main__":` block
- Use assertions for test cases: `assert solution.solve([2, 7], 9) == [0, 1]`
- Include edge cases: empty input, single element, duplicates, large inputs
- Print success message: `print("✅ All tests passed!")`
- No external testing frameworks required (stdlib `unittest` optional for complex cases)

### Comments
- Explain **why**, not **what**
- Use comments for non-obvious algorithmic insights
- Avoid redundant comments that restate the code
- Good: `# Use two pointers to avoid O(n²) nested loop`
- Bad: `# Increment i by 1`

## Code Style

- Follow **PEP 8** style guidelines
- Use meaningful variable names that reflect algorithmic concepts
- Prefer clarity over brevity (but avoid unnecessary verbosity)
- Maximum line length: 88 characters (Black formatter standard)
- Use 4 spaces for indentation (no tabs)

## Development Tools (Optional)

While not required, these tools can improve code quality:
- **black** - Code formatter
- **mypy** - Static type checker
- **ruff** - Fast Python linter
- **pytest** - Advanced testing framework (for complex test suites)

## Package Management

This project has no external dependencies, so package management is minimal. If you need to manage Python versions:

- **pyenv** - Python version management
- **venv** - Built-in virtual environment (stdlib)

## Build & Test Commands

Since this is a stdlib-only project:

```bash
# Run a specific implementation
python data-structures/arrays/dynamic_array.py

# Run all tests in a directory (if using unittest)
python -m unittest discover -s data-structures/arrays/

# Type check with mypy (optional)
mypy data-structures/arrays/dynamic_array.py
```
