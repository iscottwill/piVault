# Overloading Functions in C# for Embedded Applications

Function overloading allows you to define multiple functions with the same name but different parameter types or numbers of parameters. This improves code readability and reusability.

## What is Function Overloading?

Multiple functions can have the same name if they differ in:
1. Parameter list types (`int` vs `double`)
2. Number of parameters (accepting 1 vs accepting 2)
3. Default parameter values

```csharp
// Same function name, different overloads
void ProcessSensor(int value) { /* raw sensor processing */ }
void ProcessSensor(float temperature, int humidity) { /* complex data */ }
double Calculate(double[] data) { /* array operations */ }
```

## When to Use Function Overloading

| **Scenario** | **Example** |
|--------------|-------------|
| Multiple input formats needed | `string Convert(string value)` vs `int ToInt(long value)` |
| Reuse same operation on different types | `WriteFile()` for various file sources |
| Simplify complex logic | Different overloads hide underlying complexity |

## Key Points

- C# does **NOT** require all parameters to be of different types (can have same names)
- You can specify default values, but it must be compile-time evaluated
- Function calls may conflict; resolve via parameter list match or type conversion if ambiguous
- Overloaded functions are resolved at compile time (no runtime check needed)

## Example in Embedded Context

```csharp
// Different overloaded methods for same function name but different inputs
void UpdateDisplay(int x, int y, string label) { /* update UI panel */ }
void UpdateDisplay(string label) { /* default parameters: centered position */ }

// Helper method with default value (compile-time resolution by compiler)
float GetSignalQuality(int[] buffer, float threshold = 0.8f) { ... }
```

Function overloading improves code maintainability and reduces duplication of similar functionality across different parameter types.
