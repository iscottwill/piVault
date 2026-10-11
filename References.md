# References in C# for Embedded Applications

Understanding references is crucial for memory management and understanding how objects communicate in .NET/C#.

## What is a Reference?

In C#, all variables are **value-type or type-agnostic**. A reference (or handle) is simply a pointer to a location in memory where the actual data resides.

### Two Types of References

| Type | Description | Example |
|------|-------------|---------|
| **Reference Type** | Reference points to object on heap | `class MyClass {}` |
| **Value Type** | Stores value directly, reference is address | `int count` |

## Example Demonstrating References

```csharp
string name = "Alice";          // String (reference type)
int age = 25;                   // int (value type)

Console.WriteLine($"{name} is {age}"); // Reference + value combined
```

### Key Differences

| **Reference Type** | **Value Type** |
|--------------------|----------------|
| `string msg = "Hello".ToString();` | `int x = 10; int y = x + 5;` |
| String is stored as reference to heap data | Value is copied directly |
| Modifying original affects both places | Each place has independent copy |

## References vs Pointers

- **Reference**: .NET's abstraction over pointer-like memory address
- **Pointer**: Direct low-level memory manipulation (C/C++)
- C# uses "references" as an abstraction layer for better safety

## Using References Effectively in Embedded Development

- Use references to share large data structures between components
- Understand that string concatenation creates new objects (not copy)
- Be aware of memory usage: large string concatenations can spike memory usage
