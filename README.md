# String Calculator TDD Kata

![TDD Cycle](https://upload.wikimedia.org/wikipedia/commons/0/0b/TDD_Global_Lifecycle.png)

A JavaScript implementation of the String Calculator TDD Kata, featuring custom delimiters, negative number handling, and comprehensive test coverage.

## 🎯 Project Overview

This project demonstrates Test-Driven Development (TDD) principles through an iterative implementation of a string calculator that:

- Handles empty strings, single numbers, and multiple numbers
- Supports various delimiters (commas, newlines, custom delimiters)
- Validates input (throws exceptions for negative numbers)
- Filters numbers (ignores values > 1000)
- Processes complex delimiter configurations

## 📋 Requirements Implementation

The calculator was built iteratively using TDD's Red-Green-Refactor methodology:

| Step | Requirement | Implementation Status |
|------|-------------|----------------------|
| 0 | Handle empty string input | ✅ |
| 1 | Support single number or two numbers | ✅ |
| 2 | Support multiple numbers | ✅ |
| 3 | Allow new lines as delimiters | ✅ |
| 4 | Support custom delimiters | ✅ |
| 5 | Throw exceptions for negative numbers | ✅ |
| 6 | Ignore numbers greater than 1000 | ✅ |
| 7 | Support multi-character delimiters | ✅ |
| 8-9 | Support multiple delimiters of any length | ✅ |

## 🧪 Test Cases

The calculator supports numerous input formats and edge cases:

### Basic Input

```javascript
Add('') // Returns 0
Add('1') // Returns 1
Add('1,2') // Returns 3
Add('1,2,3,4,5') // Returns 15
```

### Delimiters

```javascript
// New lines as delimiters
Add('1\n2,3') // Returns 6

// Single-character custom delimiters
Add('//;\n1;2') // Returns 3
Add('//|\n4|5|6') // Returns 15

// Multi-character custom delimiter
Add('//sep\n7sep8sep9') // Returns 24

// Special custom delimiters
Add('//-\n-1-2-3') // Returns 6
Add('//a\n0a1a2a3') // Returns 6
Add('// \n1 2 3') // Returns 6
```

### Negative Numbers

```javascript
Add('1,-2,3') // Throws "negative numbers not allowed -2"
Add('-1,-2,-3') // Throws "negative numbers not allowed -1,-2,-3"
```

### Ignoring Numbers > 1000

```javascript
Add('2,1000') // Returns 1002 (1000 is included)
Add('2,1001,3') // Returns 5 (1001 is ignored)
```

### Advanced Delimiter Handling

```javascript
// Multi-character delimiters in brackets
Add('//[***]\n1***2***3') // Returns 6
Add('//[abc]\n4abc5abc6') // Returns 15

// Multiple delimiters
Add('//[*][%]\n1*2%3') // Returns 6
Add('//[***][%][#]\n1***2%3#4') // Returns 10

// Special characters as delimiters
Add('//[.][*][+]\n1.2*3+4') // Returns 10
```

## 🏗️ Architecture

The solution follows a modular design with separate functions for:

- **Delimiter parsing** - Handles standard and custom delimiters
- **Negative number validation** - Detects negative inputs
- **Number filtering** - Removes numbers > 1000
- **Number processing** - Converts and sums valid numbers

## 🧠 Key Design Decisions

1. **Regular Expressions**: Used for flexible delimiter parsing and pattern matching
2. **Pure Functions**: Each function has a single responsibility with no side effects
3. **Error Handling**: Clear error messages with all negative numbers listed
4. **Defensive Coding**: Robust handling of edge cases

## 🚀 Running the Tests

```bash
npm test
```

## 📘 Development Steps

The project followed strict TDD principles:

1. **Red(test)** - Write a failing test
2. **Green(feat)** - Make it pass with minimal code
3. **Refactor** - Improve the code without changing functionality

Each step was committed after the full TDD cycle was complete, ensuring a clean and traceable development history.

## 🔍 Edge Case Handling

The calculator handles various edge cases including:
- Empty strings
- Empty delimiter brackets `//[]\n1,2,3`
- Special regex characters as delimiters
- Spaces and tabs as delimiters
- Numbers within delimiters
- Multi-character delimiters with special characters

## 📚 Technologies Used

- JavaScript
- Jest (Testing Framework)
- NPM (Package Manager)
- Visual Studio Code
