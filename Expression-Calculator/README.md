# ⿥ Expression Calculator

A simple command-line calculator that can solve math expressions.
It works by converting normal math (infix) into postfix and then evaluating it.

## ✨ Features

- Handles + - * / ^ operators
- Works with parentheses ( )
- Supports unary minus (e.g. -5, 3*-2)
- Accepts decimal numbers (3.14, 0.5)
- Shows clear error messages

## 📦 Build & Run
### Using g++
```bash
g++ -std=c++17 -O2 -o calc src/main.cpp
./calc "3 + 4 * 2"
```
### Using Make
make
```bash
./calc "2 ^ 3 ^ 2"
```

## ▶️ Usage

###  Pass an expression as an argument:
```bash
./calc "3 + 4 * 2 / (1 - 5) ^ 2 ^ 3"
```

### Or type the expression through stdin:
```bash
echo "3*-2 + 10/5" | ./calc
```
## 📖 Examples
Input:  3 + 4 * 2 <br>
Output: 11.0000000000

Input:  -(2+3)*4.5 <br>
Output: -22.5000000000

Input:  2 ^ 3 ^ 2 <br>
Output: 512.0000000000

## ⚠️ Errors

- Division by zero → error: division by zero
- Mismatched parentheses → error: mismatched parentheses
- Wrong symbols → error: unexpected character

## 📂 Project Structure
```bash
.
├─ src/
│  └─ main.cpp
├─ Makefile
├─ CMakeLists.txt
└─ README.md
```
