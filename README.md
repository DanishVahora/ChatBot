# String Calculator TDD Kata

![Test Results](assets/step-1/Passed_Two_Number_Input.png)

## Overview

This project implements a String Calculator following Test-Driven Development (TDD) principles. The calculator takes a string input containing numbers separated by delimiters and returns their sum, with special handling for various edge cases.

## Features

- Basic string-to-number calculation
- Support for default delimiters (comma, newline)
- Custom delimiter specification
- Multi-character delimiter support
- Multiple delimiter support
- Negative number validation
- Ignoring numbers greater than 1000

## Project Structure

```
string-calculator/
├── src/
│   └── stringCalculator.js
├── tests/
│   └── stringCalculator.test.js
└── assets/
    └── (test result screenshots)
```

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/string-calculator.git

# Navigate to project directory
cd string-calculator

# Install dependencies
npm install
```

## Running Tests

```bash
# Run all tests
npm test

# Run tests with coverage
npm test -- --coverage
```

## Implementation Steps

### Step 1: Basic Implementation

- Return zero for an empty string
- Parse and return the number for a single number input
- Add two numbers separated by a comma

**Test Cases:**
```javascript
expect(Add('')).toBe(0);
expect(Add('1')).toBe(1);
expect(Add('42')).toBe(42);
expect(Add('1,2')).toBe(3);
expect(Add('10,20')).toBe(30);
```

### Step 2: Multiple Numbers

- Support an unknown amount of numbers

**Test Cases:**
```javascript
expect(Add('1,2,3,4,5')).toBe(15);
expect(Add('6,7,8,9,10')).toBe(40);
```

### Step 3: Newline Delimiter

- Support newlines as valid delimiters between numbers

**Test Cases:**
```javascript
expect(Add('1\n2,3')).toBe(6);
expect(Add('4\n5\n6')).toBe(15);
expect(Add('7,8\n9')).toBe(24);
```

### Step 4: Custom Delimiters

- Support custom delimiters defined in the format `//[delimiter]\n[numbers]`

**Test Cases:**
```javascript
expect(Add('//;\n1;2')).toBe(3);
expect(Add('//|\n4|5|6')).toBe(15);
expect(Add('//sep\n7sep8sep9')).toBe(24);
expect(Add('//x\n10')).toBe(10);
expect(Add('//-\n-1-2-3')).toBe(6);
expect(Add('//a\n0a1a2a3')).toBe(6);
expect(Add('// \n1 2 3')).toBe(6);
```

### Step 5: Negative Number Handling

- Throw an exception for negative numbers with the message "negative numbers not allowed" followed by all negative numbers

**Test Cases:**
```javascript
expect(() => Add('1,-2,3')).toThrow('negative numbers not allowed -2');
expect(() => Add('1,-2,-3,4')).toThrow('negative numbers not allowed -2,-3');
expect(() => Add('-1,-2,-3')).toThrow('negative numbers not allowed -1,-2,-3');
expect(() => Add('//;\n1;-2;3')).toThrow('negative numbers not allowed -2');
```

### Step 6: Numbers > 1000

- Ignore numbers greater than 1000

**Test Cases:**
```javascript
expect(Add('1001')).toBe(0);
expect(Add('2,1000')).toBe(1002);
expect(Add('2,1001,3')).toBe(5);
expect(Add('1001,2000,3000')).toBe(0);
```

### Step 7: Multi-Character Delimiters

- Support delimiters of any length in the format `//[delimiter]\n`

**Test Cases:**
```javascript
expect(Add('//[***]\n1***2***3')).toBe(6);
expect(Add('//[abc]\n4abc5abc6')).toBe(15);
expect(Add('//[xyz]\n7xyz8xyz9')).toBe(24);
```

### Step 8 & 9: Multiple Delimiters

- Support multiple delimiters in the format `//[delim1][delim2]...\n`

**Test Cases:**
```javascript
expect(Add('//[*][%]\n1*2%3')).toBe(6);
expect(Add('//[;][,]\n4;5,6')).toBe(15);
expect(Add('//[a][b][c]\n1a2b3c4')).toBe(10);
expect(Add('//[***][%][#]\n1***2%3#4')).toBe(10);
```

## Edge Cases Handled

1. **Empty Input**: Returns 0
2. **Single Number**: Returns the number itself
3. **Negative Numbers**: Throws exception with appropriate message
4. **Numbers > 1000**: Ignored in calculations
5. **Special Regex Characters as Delimiters**: Properly escaped
6. **Delimiters with Numbers**: Correctly parsed
7. **Space Delimiters**: Properly handled

## Implementation Details

The implementation uses several key functions:

- `parseDelimiter`: Extracts custom delimiters and the remaining number string
- `escapeRegex`: Safely escapes special regex characters
- `findNegatives`: Identifies negative numbers for validation
- `filterValidNumbers`: Filters out numbers > 1000
- `sumNumbers`: Performs the actual addition

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
