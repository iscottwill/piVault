# Functions and Operators in C# for Embedded Applications

Understand how functions and operators work together to build powerful, expressive code in C#.

## Functions in C#

Functions encapsulate actions that return values. In .NET:
- **Signature**: Parameter types + name must match declaration exactly
- **Scope**: Define behavior outside of methods/objects
- **Overloading**: Multiple functions with same name but different parameter signatures

```csharp
// Two different functions (overloads)
int Add(int x, int y) { return x + y; }          // int + int = int
Decimal Add(double a, double b) { return a + b; } // double + double = decimal

void DoWork() { /* perform embedded tasks */ }   // no return type
```

## Standard Operators in C#

| Category | Examples |
|----------|----------|
| **Arithmetic** | `+`, `-`, `*`, `/`, `%` |
| **Relational** | `==`, `!=`, `<`, `>`, etc. |
| **Logical** | `&&`, `||`, `!` |
| **Bitwise** | `&`, `\|`, `^`, `<<`, `>>` |
| **Increment/Decrement** | `++`, `--` |

## Using Operators Effectively

```csharp
int result = 5 + 3;                  // Arithmetic: +
bool isPrime = number != 0 && number > 1 && IsDivisor(number, 2);

// Bitwise operator for low-level hardware access (embedded)
uint portRegister = ((portRegister & ~ENABLE_BIT) | ENABLE_MASK);
```

## Operator Precedence

```csharp
int x = 3 + 4 * 5;         // 23, not 35: multiplication before addition
string msg = "Hello" + string.Empty + world;        // Concatenates strings
if (statusCode == 0 || statusCode == -1) { /* OK condition */ }
```

Functions and operators together allow building complex logic from simple operations.
