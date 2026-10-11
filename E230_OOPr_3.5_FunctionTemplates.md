# 3.5.FunctionTemplates

## Overview  
Function templates in .NET C# provide compile-time polymorphism by allowing generic methods and types to operate on any data type that satisfies specific constraints. This enables writing reusable code once rather than duplicating for different types—critical when developing GUI applications that handle diverse embedded device communication protocols across OOP frameworks.

### Key Definitions  
| Term | Definition |
|------|------------|
| **Function Template** | Compile-time declaration pattern parameterized by type variables, enabling type-agnostic operation on any compatible data structure |
| **Generics (`<>`)** | Type parameters that resolve to specific types during compilation (e.g., `List<T>` becomes `List<string>` or `List<double>`) |
| **Constrain (`where` clause)** | Restriction on which types can be substituted for type parameters (e.g., `T` must implement interface contracts in OOP GUI designs) |

### Core Concepts  
1.  **Type Parameter Resolution**: C# compiler resolves `T` to concrete types at compile-time—allows optimization; runtime sees fully specialized version
2.  **Zero Runtime Overhead for Type Safety**: Generic constraints checked by compiler, no runtime type checking overhead in OOP GUI applications compared to reflection-based solutions  
3.  **Template vs Instance Methods**: Functions templates operate on type-level information; instance methods modify object state via specific types

### Main Content  

#### Template Syntax Overview (.NET C# Pattern)

```csharp
// File: FunctionTemplates.cs (Visual Studio auto-generated template structure showing generic/ templated function patterns in .NET context)
public static class OOPHelper {
    public static void PrintValue<T>(T value, string message) where T : struct {
        Console.WriteLine($"{message}: {value?.ToString()}"); // Type resolved at compile-time, no runtime overhead for GUI app designs
    }

    // List example—type parameter T resolves to concrete type during application initialization in .NET OAP GUI frameworks
    public static void ProcessItems<ListType>(List<DataType> items)
        where DataType : IObjectLike { /* Operations work on any List subclass without duplication */ }
}
```

#### Template vs Explicit Type Parameters (Performance Implications)

| Feature | Function Template (.NET Generic) | Type-Specific Method | Impact in OAP GUI Apps |
|---------|---------------------------------|----------------------|------------------------|
| **Declares** | Single generic declaration with `T` placeholder | Multiple method overloads for different types | Generic = fewer lines of code; better maintainability across .NET projects |
| **Type Resolution** | Compile-time (`Console.WriteLine()` optimized) | Compile-time (each overload has own signature) | Compilers can optimize specialized methods; no runtime cost difference in practice |
| **Memory Efficiency** | Zero overhead during method calls (single binary at compile time) | One separate compilation unit per type | Generic enables larger GUI project codebases without bloating with duplicated logic |

### Examples and Applications  
#### Example 1: Generic Function Template for Embedded Device Communication (.NET OAP Context)

```csharp
// File: GenericDeviceOps.cs (Visual Studio auto-generated template showing generic operation patterns supported across .NET C# embedded device frameworks)
public static class DeviceCommunication {
    // Accepts any type T implementing ICommunicationProtocol interface in OOP GUI designs for embedded devices
    public static T ExecuteProtocolOperation<T>(T deviceInstance, string command, object? data = null)
        where T : class, ICommunicationProtocol => 
            ((T)deviceInstance)!?.ProcessCommand(command, data); // Type-safe generic function across heterogeneous device interfaces

    // ProcessItems example—accepts different list types (string, int, double, sensor readings) in OAP GUI apps  
    public static string FormatList<T>(List<T> items, string labelText)
        where T : class, IParsable { 
            StringBuilder sb = new StringBuilder();
            foreach (T item in items) => 
                sb.AppendLine(item?.ToString()); // Generic list operations without type-specific code for GUI apps
            return $"[{labelText}]:{sb.ToString()}";
    }
}
```

#### Example 2: Type Parameter Constraints for GUI Event Handling (.NET C# Context)

| Scenario | Templated Solution (Type-Safe in .NET OAP GUI Apps) | Type-Specific Alternative | Constraint Used |
|----------|--------------------------------------------------------|---------------------------|-----------------|
| **Event Handler** | `HandleEvent<T>(T sender)` where T : EventSource | Multiple method overloads | `where T : class, EventSource` |
| **Data Binding** | `BindProperty<DataType>` for UI bindings | Separate binder per property type | `where DataType : IBindableProperty` |

```csharp
// File: GenericEventHandling.cs (Visual Studio auto-generated template showing generic event handling patterns in .NET C# OAP GUI frameworks)
public static class EventHandling {
    public static void SubscribeEvents<T>(T sender, Action<object>? callback)
        where T : class { 
        sender.Subscribe("OnEventReceived", callback); // Works for any object type in OOP GUI design
    }

    // GUI controls—accepts Window, TextBox, ComboBox as types in .NET runtime event handler patterns
}
```

### Important Notes & Reminders  
- **Type Constraints Matter**: `where T : interface` ensures compile-time checks enforce contract (required for OOP frameworks); omitting constraints enables any type but sacrifices safety in C# GUI apps  
- **Runtime Type Safety Still Applies**: Even with templates, .NET runtime enforces type checking; mismatched `T` substitution causes compile error rather than runtime exception  
- **Use Cases Across OAP GUI Development**: Function templates eliminate code duplication for generic operations (list processing, event handling) in C#.NET OOP frameworks  
- **Compatibility Warning**: Very old .NET SDKs (pre-.NET 2.0) lack full template support; ensure target framework version ≥4.8 for C# 4.0+ features  

### Quiz / Review Questions  
1. What compile-time benefit does using function templates provide over explicit type-specific methods in .NET C# OOP GUI applications?  
2. Can you use `void` with a generic parameter declaration `T`? Explain why/why not in the context of .NET OAP frameworks.  
3. Why do we need constraints (`where T : interface`) even at compile time for type inference?  
4. In what scenario would you prefer function overloads (type-specific methods) versus templates in a large GUI application codebase?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_FunctionOverloading]] [[#Reference_TypeConstraints]] [[E230_OOPr_1.2_API.md]]
