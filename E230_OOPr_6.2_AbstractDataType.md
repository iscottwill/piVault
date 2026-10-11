# 6.2.AbstractDataType

## Overview
Abstract data types (ADTs) in .NET C# are interfaces defining behavior without implementation details—critical for decoupling GUI applications from concrete class implementations. ADTs enable OOP applications to treat heterogeneous objects uniformly via standardized methods while deferring specific type decisions to runtime or derived classes.

### Key Definitions
| Term | Definition |
|------|------------|
| **Abstract Class/Interface** | Base class defining method signatures but no implementation (`.NET` interface pattern; abstract members prevent direct instantiation) |
| **Implementation Contract** | Interface specifies required behaviors (e.g., `Calculate()` must exist); derived classes must implement all contract methods during compilation in OAP OOP designs |
| **Constrained Polymorphism** | ADTs enforce consistent method signatures across implementations—enables uniform operations on heterogeneous object collections via runtime JIT dispatch in .NET |

### Core Concepts
1. **Interface vs Base Class**: In C#.NET, `interface` defines contracts without implementation; `.NET base classes` may provide default implementation for inherited members (more flexibility than pure abstract interfaces)
2. **Dependency Injection**: OAP applications can inject ADT implementations at runtime—reduces coupling to specific .NET implementation details while maintaining behavioral consistency via abstract contract in C#.NET designs
3. **Dynamic Type Resolution** | GUI apps invoke methods through ADTs without knowing exact child type at compile time; runtime dispatch resolves correct behavior based on actual object class in OAP event handlers

### Main Content

#### Abstract Interface Implementation Patterns (.NET C# Context)

```csharp
// Visual Studio generated code for abstract data type implementations in .NET OOP context
{
    // Base class defines methods but no bodies (abstract interface pattern in .NET) 
    public interface ICalculationBase {
        // Required method definition without implementation—child classes must implement during compilation  
        int Calculate(int inputVal); 

        string OnGetDescription(); // Optional additional method with default implementation (.NET runtime pattern)
    }

    // Concrete class implementing ICalculationBase contract via inheritance (OAP design enables uniform behavior regardless of child type for GUI apps) 
}
```

#### Contract & Implementation Pattern Comparison (.NET OOP Design)

| Feature | Abstract Interface (IInterface, .NET pattern) | Concrete Base Class (BaseClass with Default Impl.) |
|---------|------------------------------------------------|-----------------------------------------------------|
| **Implementation** | No body—child must provide all methods during compilation (strict contract enforcement in OAP apps) | Can provide default implementation for some members; child extends rather than duplicates where applicable in .NET runtime context |

```csharp
// File: AbstractDataTypes.cs (Visual Studio auto-generated template structure for C#.NET interface/abstract pattern implementations)
{
    // Interface contract for GUI applications to treat calculations uniformly via OAP abstract method design  
    public interface ICalculationAdapter {
        // Required calculation method with signature enforced across all derived implementations in OAP context
        int CalculateResult(int inputVal); 

        // Optional default implementation (.NET 8+ feature allows empty interface definitions for flexibility)
        string GetUserDescription() => "User provided input"; 
    }

    // Child class implementing full contract—must provide all required method bodies during compilation  
}
```

### Examples and Applications

#### Example 1: Interface vs Concrete Class Implementation (.NET OOP Design Pattern)

```csharp
// File: AdapterInterface.cs (Visual Studio auto-generated template for OAP adapter pattern using interfaces/abstract classes in C#.NET context)
{
    // Define interface as ADT contract—enforces consistent method signature across implementations during compilation  
    public interface ICalculationAdapter {
        // Base class defines required method without implementation details (interface contract)
        int Calculate(); 
        string OnGetResultDescription() => "Unknown calculation type"; // Default impl in interface for flexibility
    }

    // Concrete child classes implementing ADT contract fully via inheritance pattern
    public struct Addition : ICalculationAdapter {
        private double _a;
        private double _b;

        public int CalculateValue(double value1, double value2) => (int)(value1 + value2);
    }
    
    class Subtraction : ICalculationAdapter {
        // Interface contract enforced—missing implementation would cause compiler error in .NET runtime
        public override int CalculateValue(object sender, EventArgs e) { 
            Console.WriteLine("Subtracting: " + sender); // Default impl provided for flexibility
            return 0;
        }
    }

    // GUI app can treat both Addition and Subtraction uniformly via ICalculationAdapter interface in OOP event handling  
}
```

### Examples and Applications

#### Example 2: Abstract Data Type Benefits (.NET OAP Event-Driven Design)

| Scenario | Benefit Over Concrete Implementation | Code Usage Pattern in .NET GUI Apps |
|----------|-------------------------------------|-------------------------------------|
| **Multiple Algorithms** | Treat different calculation methods (e.g., `Add`, `Multiply`) uniformly via single interface; no need to create separate GUI methods for each type in .NET OAP designs | GUI invokes `calculationAdapter.Calculate()` regardless of actual underlying algorithm at runtime—flexible, extensible design across multiple implementations |
| **Swappable Implementations** | Runtime injection of different ADT implementations (e.g., switch between `Addition` and `Multiplication` classes) without modifying calling code in .NET GUI apps | Inject ICalculationAdapter implementation string ("Add", "Multiply") into variable at runtime; GUI behavior changes dynamically via interface abstraction layer |
| **Error Handling** | Interface defines expected behavior (throws exception for invalid inputs); ensures all implementations handle errors consistently across derived classes via OAP design patterns in .NET code review | If `Calculate()` throws, GUI catches generic exception—interface contract guarantees error handling uniformity across heterogeneous object collections in .NET apps |

```csharp
// File: AbstractDataTypesUsage.cs (Visual Studio auto-generated template for OAP usage of abstract data types via interface contracts in C#.NET context)
{
    // Base class defines method signatures; child implementations provide concrete logic (.NET compilation enforces contract compliance)
    public interface ICalculationAdapter {
        int OnCalculate(int inputVal); 
    }

    // Abstract ADT benefits: GUI apps can inject implementations dynamically at runtime without recompiling base code in OAP applications  
}

// File: ImplementationInjection.cs (Visual Studio generated template structure for runtime injection of ADTs via interfaces)
{
    class CalculatorManager {
        private ICalculationAdapter _calculationAdapter = null; 

        // Method accepts any interface implementation—enables dynamic swapping of concrete implementations in .NET GUI apps  
        public void SetCalculationMethod(object adapterImpl, ref int inputCount) => 
            _calculationAdapter = (ICalculationAdapter)adapterImpl;

        int OnGetResult(int inputVal) => _calculationAdapter.Calculate(inputVal)!; // Runtime dispatch via interface-based ADT pattern  
    }
}
```

### Important Notes & Reminders

- **Interface Compilation** | Interface implementation requires all members to have bodies; missing bodies during compilation cause errors in .NET IDE (not runtime only)
- **Default Implementations**: .NET supports default interface methods (.NET 8+ feature) for optional behavior without breaking abstract interface contracts across OAP GUI apps
- **Dependency Injection**: Injecting ADT implementations at runtime enables OAP applications to switch algorithms/configurations dynamically without recompiling—reduces tight coupling in large-scale .NET apps
- **Polymorphic Behavior**: Interface-based ADTs leverage JIT compilation for correct method dispatch at runtime—ensures consistent behavior across heterogeneous object collections via runtime type analysis

## Quiz / Review Questions
1. Why might you prefer using an interface over a concrete base class when designing contracts for heterogeneous classes in OAP applications?
2. How does a default implementation (.NET 8+ feature) differ from requiring all methods to be implemented directly by child classes during compilation in .NET runtime?
3. In what scenario would abstract data types (interfaces) be more valuable than hardcoded concrete class hierarchies in C#.NET GUI application design?
4. What happens at compile time if a derived class forgets to implement one of the interface members (missing requirement)?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_VirtualMethodOverrides]] [[#Reference_RuntimeTypeDispatchJIT]]
