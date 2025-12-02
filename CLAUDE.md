# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an Advent of Code 2025 project written in APL (A Programming Language). The repository is structured to solve daily coding challenges using APL's array-oriented programming paradigm.

## Project Structure

```
aoc25_apl/
├── utils.aplf              # Reusable utility functions for common AoC patterns
├── dayXX.aplf              # Daily solution files (root level)
├── aoc25.dws               # Dyalog workspace file
└── 2025/
    ├── template.aplf       # Template for new daily solutions
    └── data/
        ├── inputs/         # Actual puzzle inputs (dayXX.txt)
        ├── examples/       # Example inputs from puzzle descriptions
        └── puzzles/        # Puzzle description markdown files
```

## Working with APL Files

### Running APL Code

APL files (`.aplf`) are executed using the Dyalog APL interpreter. To run a solution file:

```bash
dyalog dayXX.aplf
```

Or load interactively in the Dyalog session:
```apl
)LOAD dayXX.aplf
```

### Working with the Workspace

The repository includes `aoc25.dws`, a Dyalog workspace file that can be used to persist loaded utilities and solutions across sessions:

```apl
)LOAD aoc25.dws        ⍝ Load the workspace
)SAVE aoc25.dws        ⍝ Save current state to workspace
```

### Using Utility Functions

The `utils.aplf` file contains reusable functions for common AoC patterns:

- **String & Parsing**: `Split`, `Lines`, `ParseNums`, `Digits`, `Trim`
- **Grid & 2D**: `ToGrid`, `Neighbors4`, `Neighbors8`, `InBounds`, `Manhattan`
- **Collections**: `Count`, `Unique`, `Freq`, `GroupBy`
- **Math**: `GCD`, `LCM`, `Sum`, `Product`, `Range`
- **Functional**: `Iterate`, `UntilStable`, `WhileTrue`
- **Input Reading**: `ReadLines`, `ReadString`, `ReadNums`, `ReadGrid`

To use utilities in a solution, load the file at the start or copy needed functions:
```apl
)LOAD utils.aplf
```

### Creating New Day Solutions

1. Copy `2025/template.aplf` to `dayXX.aplf` at root level (where XX is the day number, e.g., `day01.aplf`)
2. Place input files in the appropriate locations:
   - `2025/data/inputs/XX.txt` - actual puzzle input
   - `2025/data/examples/XX.txt` - example from puzzle description (optional)
   - `2025/data/puzzles/XX.md` - puzzle description (optional)
3. Update the input file path in your solution file to point to `2025/data/inputs/XX.txt`
4. Implement `Part1` and `Part2` functions
5. Run the file: `dyalog dayXX.aplf`

The template structure:
- Input reading section with multiple methods (lines, numbers, string, grid)
- Helper functions section (`ParseLine`, `Split`) for day-specific parsing
- `Part1` function with placeholder
- `Part2` function with placeholder
- Sample and actual input execution with output statements

## APL-Specific Conventions

### Function Definitions

Functions are defined using the `←` assignment operator:
```apl
FunctionName ← {⍵}           ⍝ Monadic (single argument)
FunctionName ← {⍺ + ⍵}       ⍝ Dyadic (two arguments)
```

### File Input Patterns

The codebase uses direct `⎕NGET` calls in solution files rather than calling utility functions:

```apl
⊃⎕NGET 'file.txt' 1    ⍝ Read as vector of lines
⊃⎕NGET 'file.txt' 0    ⍝ Read as single string
↑⊃⎕NGET 'file.txt' 1   ⍝ Read as character grid
⍎¨⊃⎕NGET 'file.txt' 1  ⍝ Read as numeric lines
```

Alternatively, use the utility functions from [utils.aplf](utils.aplf):
```apl
ReadLines 'file.txt'   ⍝ Vector of lines
ReadString 'file.txt'  ⍝ Single string
ReadGrid 'file.txt'    ⍝ Character grid
ReadNums 'file.txt'    ⍝ Numeric lines
```

### Common APL Patterns in This Codebase

- **Partitioned enclose for splitting**: `(delimiter=input)⊂input`
- **Filter using compress**: `condition/data`
- **Where (indices of 1s)**: `⍳≢data` combined with filtering
- **Recursion with guards**: `{condition:base_case ⋄ recursive_call}`
- **Fixed-point iteration**: `function⍣≡⊢data`

## Naming Conventions

- Functions use PascalCase: `ParseNums`, `ReadGrid`, `ToGrid`
- Variables use camelCase: `input`, `data`, `result`
- Keep function names descriptive and verb-based for transformations
