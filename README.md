# 🧮 String Calculator TDD Kata

![TDD Cycle](https://upload.wikimedia.org/wikipedia/commons/0/0b/TDD_Global_Lifecycle.png)

## 📝 Description

A step-by-step implementation of the String Calculator TDD Kata, showcasing clean code, test-driven development, and iterative feature building. This project demonstrates how to build a feature-rich calculator that handles various input formats, custom delimiters, and edge cases - all through the Red-Green-Refactor cycle.

## ✨ Features

- **Flexible Input Handling** - Process empty strings, single numbers, or multiple numbers
- **Multiple Delimiter Support** - Use commas, newlines, or custom delimiters
- **Custom Delimiter Definition** - Simple or complex delimiter patterns
- **Input Validation** - Exception handling for negative numbers  
- **Smart Number Processing** - Ignores numbers greater than 1000

## 🚀 Implementation Steps

| Step | Description | Example |
|------|-------------|---------|
| 1️⃣ | Empty string returns zero | `Add("") → 0` |
| 2️⃣ | Single number returns the number | `Add("1") → 1` |
| 3️⃣ | Two numbers return their sum | `Add("1,2") → 3` |
| 4️⃣ | Multiple numbers supported | `Add("1,2,3,4,5") → 15` |
| 5️⃣ | New line as delimiter | `Add("1\n2,3") → 6` |
| 6️⃣ | Custom delimiters | `Add("//;\n1;2") → 3` |
| 7️⃣ | Negative numbers throw exception | `Add("1,-2") → throws "negatives not allowed: -2"` |
| 8️⃣ | Ignore numbers > 1000 | `Add("2,1001") → 2` |
| 9️⃣ | Multi-character delimiters | `Add("//[***]\n1***2***3") → 6` |
| 🔟 | Multiple custom delimiters | `Add("//[*][%]\n1*2%3") → 6` |

## 📊 Test Showcase

### Basic Operations
```javascript
// Empty input
expect(Add('')).toBe(0);

// Single number
expect(Add('1')).toBe(1);
expect(Add('42')).toBe(42);

// Multiple numbers
expect(Add('1,2,3,4,5')).toBe(15);
```

### Delimiter Variations
```javascript
// Newlines as delimiters
expect(Add('1\n2,3')).toBe(6);
expect(Add('4\n5\n6')).toBe(15);

// Custom single-character delimiters
expect(Add('//;\n1;2')).toBe(3);
expect(Add('//|\n4|5|6')).toBe(15);

// Multi-character delimiters
expect(Add('//sep\n7sep8sep9')).toBe(24);
```

### Edge Cases & Special Handling
```javascript
// Negative numbers
expect(() => Add('1,-2,3')).toThrow('negative numbers not allowed -2');
expect(() => Add('-1,-2,-3')).toThrow('negative numbers not allowed -1,-2,-3');

// Ignoring large numbers
expect(Add('2,1000')).toBe(1002);  // 1000 is included
expect(Add('2,1001,3')).toBe(5);   // 1001 is ignored

// Special delimiter characters
expect(Add('//[.*]\n1.*2.*3')).toBe(6);  // Special regex chars
expect(Add('//[123]\n11231123')).toBe(2); // Numbers as delimiters
expect(Add('//[   ]\n1   2   3')).toBe(6); // Spaces as delimiters
```

### Advanced Delimiter Configurations
```javascript
// Multiple delimiters of any length
expect(Add('//[a][b][c]\n1a2b3c4')).toBe(10);
expect(Add('//[***][%][#]\n1***2%3#4')).toBe(10);
expect(Add('//[.][*][+]\n1.2*3+4')).toBe(10);
```

## 🧠 Technical Implementation

### Modular Functions
The solution is designed with clean, single-responsibility functions:

- **`parseDelimiter`**: Extract and process custom delimiters
- **`findNegatives`**: Detect negative numbers for validation
- **`filterValidNumbers`**: Remove numbers > 1000
- **`sumNumbers`**: Calculate the final result

### Code Highlights

```javascript
// Multiple delimiters parsing logic
if (input.startsWith('//[')) {
    const delimiterBrackets = input.match(/\[(.*?)\]/g);
    if (delimiterBrackets) {
        const delimiters = delimiterBrackets.map(d => escapeRegex(removeBrackets(d)));
        const delimiterRegex = new RegExp(delimiters.join('|'));
        const delimiterSectionEnd = input.indexOf('\n') + 1;
        return { delimiter: delimiterRegex, rest: input.slice(delimiterSectionEnd) };
    }
}
```

## 🔍 TDD Approach

Each feature was developed following strict TDD principles:

1. **🔴 RED**: Write a failing test that verifies the expected behavior
2. **🟢 GREEN**: Implement the minimum code needed to make the test pass
3. **🔄 REFACTOR**: Improve the code without changing its behavior

## 📦 Getting Started

```bash
# Clone the repository
git clone [your-repo-url]

# Install dependencies
npm install

# Run tests
npm test
```

## 📈 Commit History

The project's commit history reflects the TDD journey:

- Step-by-step feature implementation
- Test-first development approach
- Regular refactoring for clean code
- Edge case handling and bug fixes

## 📚 Learning Resources

This kata is perfect for practicing:

- Test-Driven Development (TDD)
- Clean Code principles
- Refactoring techniques
- String manipulation in JavaScript
- Regular expressions
- Modular code design
