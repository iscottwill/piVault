# 3.3.FunctionsandOperators

## Overview
Functions (also called methods in OOP) are the building blocks of code that encapsulate logic for performing operations and returning values. Operators perform atomic calculations using operands; functions often handle complex computations across multiple lines or return data structures. Understanding both is essential for designing maintainable C# applications.

### Key Definitions
| Term | Definition |
|------|------------|
| **Function/Method** | Named block of code that performs operations and optionally returns values in OOP contexts |
| **Operator** | Built-in language construct (e.g., `+`, `-`) or custom function for atomic computations like arithmetic or comparison logic |
| **Parametrized Functions** | Functions that accept input arguments via parameters to customize behavior at runtime |
| **Return Type** | Data type expected by the compiler; determines what the function produces and can return to callers |

### Core Concepts
1. **Operator vs Function Distinction**: Operators (like `+`) are primitive constructs in language definition; functions are defined by developers through method declarations
2. **Parameter Passing Modes**: Reference values passed by reference, while most primitive types pass by value (copy) and references can trigger changes to object state
3. **Overloading Capability**: C# lets developers define multiple functions or operators with same name but different signatures

### Main Content

#### Function Declaration Patterns (.NET OOP Syntax)

```csharp
// Visual Studio generated code template showing both operator and function declarations
public class CalculationExample {
    // Primitive function declaration with return type, parameter list, function body
    public int Add(int valueA, int valueB) {
        return valueA + valueB; // Call built-in operator inside function body
    }

    // Operator overloading pattern (custom + for struct objects in .NET)
    public static CalcResult Add(CalcResult a, CalcResult b) { 
        // Returns result as object type from operator application
        CalcResult calculatedValue = new CalcResult(a.Value + b.Value);
        return calculatedValue; 
    }
}

class OperatorSyntaxExample {
    public void OnMethodExecution(EventArgs e) => AddValues()!; // Method call with null safety operator
}
```

#### Function vs Operator Application Behavior

| Feature | Function (`Calculate()`) | Operator (`+`, `*`, etc.) |
|---------|-------------------------|---------------------------|
| **Declaration** | Hand-written in code (e.g., `public int Calculate(double a)`) | Built into language spec (compiler-generated implementation) |
| **Customization** | Can implement arbitrary logic, multiple lines of code | Simplifies to binary operation or single-statement expression unless overloaded |
| **Naming Convention** | Uses explicit function/method names (`Calculate`, `Convert`, etc.) | Uses operator symbols (`+`, `-`, `*`, `/`) |
| **Visibility Control** | Can be public, private, protected, internal | Built-in operators have fixed syntax (though overloading possible) |
| **Memory Impact** | Typically negligible overhead for primitive types | Minimal runtime call overhead; may compile directly to machine code |

### Examples and Applications

#### Example 1: Multi-Line Function Implementation with Operator Usage (.NET C#)

```csharp
// File: OOPFunctions.cs (Visual Studio generated template structure)
public class CustomFunctionExample {
    // Private helper function uses + operator internally for value calculation logic
    private int PerformAddition(int first, int second) {
        // Internal implementation of operation using simple operator syntax
        return first + second; 
    }
    
    // Public method with complex business logic calling the helper function above
    public int ComputeTotalPrice() => PerformAddition(20, 15);
    
    // Overloaded operator implementation example (C# feature)
    public static CalcResult Add(CalcResult operandA, CalcResult operandB) {
        return new CalcResult(operandA.Value + operandB.Value);
    }
}

class CustomOperatorExample {
    public void OnFunctionInvocation(object sender, EventArgs e) => 
        // Function method called via explicit function invocation pattern  
        ComputeCustomOperation();
}
```

#### Example 2: Operator Overloading Patterns (.NET OOP Development Style)

Operators can be overloaded when working with custom types or structs in C# .NET development contexts:

| Scenario | Pattern | Implementation |
|----------|---------|----------------|
| **Addition for struct objects** | `operator +` syntax overwrites standard addition | `(a, b) => a + b` returns new instance of struct type |
| **Custom comparison function** | Custom methods (e.g., `GreaterThan()`) override operator use | Returns boolean or custom value based on parameters passed through function call |

```csharp
// File: Operators.cs (Visual Studio OOP development template structure)
public class CustomOperatorExample {
    // Method overloading pattern with multiple parameter signatures
    public string ProcessAddition(string inputA, string inputB) => 
        $"Result: {inputA + " " + inputB}"; // Using standard concatenation operator
    
    // Function method for complex operation using built-in operators internally
    private void ComputeComplexFunction() {
        var result = CalculateValue(); // Call function definition that uses operators internally
    }

    // Overloaded operator with static return type (common pattern in C# .NET dev)
    public static Calculator Add(CalcResult operandA, CalcResult operandB) { 
        return new CalcResult(operandA.Value + operandB.Value);
    }
}
```

#### Operator vs Function Application Flow Diagram

```
┌─────────────┐     ┌──────────────────┐
│  +operator  │     │   Calculate()    │
│  (Built-in) ├───> │   (Developer-Def) │
└─────────────┘     └──────────────────┘
       │                     │
       ▼                     ▼
┌─────────────────────┐┌──────────────────────┐
│  Returns immediate  ││  Can perform multi-line│
│   value via compile-time │    execution logic │
└─────────────────────┘└──────────────────────┘
```

### Important Notes & Reminders

- **Primitive Types (int, double)**: Always pass by value—modifying function parameters affects only local copy, not external object state in OOP C# patterns
- **Reference Type Parameters**: When parameters are classes/objects, changes to those values affect the original reference; but this does NOT modify internal object state of the parameter itself
- **Overloaded Function Definitions**: Multiple functions with same name but different signatures (parameter types, count) can coexist—compiler selects appropriate one based on call context
- **Visibility Controls**: Ensure public functions are documented clearly for external API consumption; private helper functions remain hidden within class scope

## Quiz / Review Questions
1. What is the difference between defining a function versus using an operator like `+` in C# OOP development?
2. How do overloaded operators work when custom type objects need special behavior defined in code?
3. Which parameter passing mode should you expect for primitive types (`int`, `string`) in .NET functions?
4. What is a typical signature pattern for a public method that returns and processes multiple inputs?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_FunctionOverloading]] [[#Reference_ParamPassingSyntax]]