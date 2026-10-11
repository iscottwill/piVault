# 6.7.ClassTemplates

## Overview
Class templates (generics) in .NET C#.NET allow compile-time type safety for collections and containers—enforcing type safety across GUI app interfaces without runtime overhead. Templates define generic class patterns (e.g., `List<T>`, `Dictionary<K,V>`) used by OAP systems to store heterogeneous data uniformly while maintaining compile-time checks in .NET designs that avoid boxing/unboxing across project boundaries for GUI applications using C#.NET OOP design principles.

### Key Definitions
| Term | Definition |
|------|------------|
| **Class Template** | Generic class definition (e.g., `class SensorList<T>`) parameterizing specific types at instantiation point (.NET runtime infers from usage context in GUI apps across project boundaries) |
| **Type Parameter** | Placeholder token (`T`, `K`, `V`) defining generic type constraints for OAP designs that require flexibility for user-defined classes and data structures via .NET generics pattern across projects  
| **Boxing/Unboxing** | `.NET` runtime converts value types to reference types (e.g., `double` → `object`) when storing in non-generic collections; class templates avoid this overhead in OAP GUI apps designed with generic patterns for performance-critical code across project boundaries  

### Core Concepts
1. **Compile-Time Type Safety**: Class templates enforce type checks during compilation (.NET ensures all elements are compatible—`List<int>` rejects `double` assignment without runtime error, unlike `List<object>` which requires boxing/unboxing across GUI project boundaries in C# code review)
2. **Performance Optimization** | Generic collections don't invoke conversion overhead at runtime—`.NET` JIT compiles optimized type-specific implementations for each instantiation pattern across multiple projects using OOP patterns (e.g., `SensorList<double>` avoids boxing vs `SensorList<object>`)
3. **Interface Compatibility**: Classes implementing `.NET` interface (e.g., `IDisposable`, `IComparable<T>`) ensure consistent behavior across heterogeneous object collections created via generic templates in OAP designs that require uniform handling methods in GUI apps

### Main Content

#### Template Instantiation vs Type Parameter Behavior (.NET C# Pattern)

```csharp
// Visual Studio generated code for class template usage in .NET context
{
    // Generic list stores elements of type T at compile-time (type safety enforced across OAP GUI app design cycles) 
}
```

#### Compile-Time vs Runtime Type Checking (.NET OAP Design)

| Feature | Non-Generic Collection (`List<object>`) | Class Template (`List<T>`, .NET Generic Pattern) | OAP Design Impact |
|---------|----------------------------------------|--------------------------------------------------|-------------------|
| **Type Safety** | `.NET` runtime allows any object assignment—requires explicit casting before access for OAP GUI apps; no compile-time check across project boundaries (e.g., `add null` passes silently) | Compile-time checks enforce type correctness—`.NET` compiler rejects invalid types during coding phase in IDE; catches errors before compilation completes  
| **Runtime Overhead** | `.NET` runtime boxes/unboxes value types (e.g., `double` → `object`) every time store/retrieval occurs across GUI apps designed with non-generic patterns (increases memory usage and GC pressure) | Value types stored directly (e.g., `int`, `double`) without boxing; `.NET` JIT generates optimized code for each type—fewer garbage collections across multiple projects in OAP designs  
| **Memory Efficiency** | Generic elements boxed (.e.g., 64-bit value + object header overhead); larger footprint per element than raw value type storage (`List<double>` consumes less memory per item) | `.NET` stores type-specific data layouts; minimal extra overhead beyond raw field size—critical for GUI apps with many sensor objects (millions of items across project boundaries)  
| **Iteration Speed** | Non-generic requires .NET runtime casting/boxing on each iteration through collection in OAP event handlers; slower performance for large datasets designed via non-template patterns | `.NET` JIT compiles fast type-specific loops; no boxing overhead—faster retrieval operations during GUI callbacks across all project boundaries using generic collections template syntax  

### Examples and Applications

#### Example 1: Generic vs Non-Generic Collection (.NET C# Runtime Pattern)

```csharp
// File: TemplateInstantiation.cs (Visual Studio auto-generated template structure demonstrating class template usage in .NET context)
{
    // Non-generic list: accepts any object type; requires boxing/unboxing conversions for value types across GUI app iterations via OAP design patterns  
    public void OnUseNonGenericList(float[] sensorData) { 
        List<double> genericSensorList = new List<object>(); // Boxing occurs on every assignment (value stored as double → object wrapper in .NET runtime)
        
        foreach (float reading in sensorData) => 
            genericSensorList.Add((double)reading); // Explicit casting required—`.NET` runtime converts at runtime across all iterations  
    }

    // Generic list: compile-time type enforcement; no boxing required for value types in OAP GUI app design cycles across projects  
}
```

### Examples and Applications

#### Example 2: Template Usage Benefits (.NET IDE Pattern)

```csharp
// File: ClassTemplateBenefits.cs (Visual Studio auto-generated template structure demonstrating generic class templates in C#.NET runtime context)
{
    // Generic list type parameter T enforces compile-time type checks—`.NET` compiler prevents invalid types across OAP GUI app code reviews  
    public class SensorList<T> {
        private readonly List<object> _rawData = new List<T>(); // Type enforced at compile time; all elements must be type matching T (`.NET` runtime infers T from context)

        public void OnAddSensor(T sensorType, ref int index) => 
            _rawData.Add(sensorType); // Validates type implicitly; `.NET` rejects assignment if wrong type across project boundaries in OAP designs  
    }

    // Class template instantiation uses concrete types (.e.g., SensorList<double>)—`.NET` JIT compiles optimized loops for value types without boxing/unboxing overhead
}

// File: TemplateConstraints.cs (Visual Studio auto-generated template structure demonstrating generic constraints in C#.NET OAP design pattern)
{
    interface IComparable<T> where T : struct // Where clause restricts instantiation to specific types (value-only classes like structs; ensures compile-time type safety across project boundaries)

    class Sensor : IComparable<double>, IStruct { // Implements generic interface with concrete type constraint for OAP apps requiring consistent comparisons }
}
```

### Examples and Applications

#### Example 3: Interface Compatibility Patterns (.NET Runtime Behavior)

| Pattern | Code Implementation | Usage Across GUI App Collections | Benefit |
|---------|--------------------|----------------------------------|---------|
| **IDisposable + Generic** | `public sealed class SensorList<T> : IDisposable { ... }` implements interface ensuring consistent cleanup across heterogeneous list instances in OAP designs (`.NET` GC manages resources automatically) | `.NET` runtime ensures proper disposal order; GUI apps call `Dispose()` on generic lists without managing individual elements across project boundaries  
| **IComparable + Generic** | `public struct SensorValue : IComparable<SensorValue>` enables direct comparison via operator overloading pattern (.NET compiler enforces type safety) | GUI callbacks can compare values directly (`if (reading1 > reading2)`); no need for explicit conversion logic for OAP designs requiring fast comparisons across project boundaries  
| **IGettable + Generic** | `public interface ITypeConstraint<T> where T : class` ensures only classes compatible with generic constraint can be instantiated; prevents type mismatches in list operations across GUI apps designed with OOP encapsulation patterns  

### Important Notes & Reminders

- **Boxing Overhead** | Non-generic collections force boxing (value → reference); class templates eliminate this—critical for performance in large GUI apps storing millions of sensor values across project boundaries in .NET IDE cycles  
- **Type Constraints**: `where T : struct` enforces value-only types; `.NET` runtime validates against invalid type instantiations during compilation phase (prevents runtime surprises)  
- **Inheritance Pattern** | Generic classes can extend base template or implement interfaces (.NET supports this); GUI apps use templates for scalable OAP designs across multiple projects  

## Quiz / Review Questions
1. What is the primary advantage of using class template (`List<T>`) over non-generic collections (`List<object>`) when storing value types for GUI apps in .NET runtime context?
2. How does the `where T : struct` constraint affect generic class instantiation—what types can or cannot be used as parameters across multiple project OOP designs in C#.NET?
3. In what scenario would boxing/unboxing occur more frequently with non-generic collections versus generic template patterns (OAP design benefit for GUI apps using .NET)?
4. What happens if you try to add incompatible type value (e.g., `int` vs `double`) to a `List<int>` collection in .NET—compile-time error vs runtime exception behavior across project boundary OOP designs?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_TypeSafetyConstraints]] [[#Reference_CompilationTimeVsRuntimeBehavior]]
