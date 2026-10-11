# Function Templates in C# for Embedded Applications

A template allows a generic class or function definition, which can generate multiple specific implementations based on type parameters. Templates are useful for avoiding code duplication in embedded development.

## What is a Template?

Templates allow you to define a single generic implementation that works with any compatible type:
- You only need one source of code for all parameterized types
- The template generates different specialized implementations for each type used
- Enables flexibility and reusability without sacrificing type safety

### Why C# Does Not Have True Templates (as C++ does)

C# uses generic classes and methods with `<>` syntax rather than C-style templates:
```csharp
// Generic class that compiles into multiple specialized implementations
class DataProcessor<T> {
    void Update(T value) { /* generic implementation */ }
}

// Usage - same code works for many types
DataProcessor<int> intProcessor = new DataProcessor<int>();
DataProcessor<float> floatProcessor = new DataProcessor<float>();
```

## Template Benefits for Embedded Development

| **Advantage** | **Description** |
|---------------|-----------------|
| **Code Reduction** | Write once, use everywhere |
| **Type Safety** | No need to convert types manually |
| **No Duplication** | Different types get their own implementation automatically |
| **Reusable Logic** | Share common operations across data types |

## Example

```csharp
// Reusable algorithm that works with any numeric type
public class ArrayHelper<T> where T : IComparable<T> {
    public void PrintArray(T[] arr) {
        foreach(var val in arr) {
            Console.WriteLine("{0}", val);
        }
    }
}

// Works with int, float, long, etc. without changes
int[] sensorData = GetReading();
float[] temperatureData = GetTempReading();

ArrayHelper<int> helper = new ArrayHelper<int>();
helper.PrintArray(sensorData);
```

C# templates are implemented via generics (with `T`, `U` type parameters) using the `< >` syntax rather than C++ templates.
