# 6.3.1.AccessFunctions

## Overview
Access (Getter/Setter) functions expose internal data to .NET GUI applications while maintaining encapsulation boundaries. These methods serve as controlled entry points for reading/writing state—preventing direct field access that could cause logical errors in OAP applications. Getter/setter pairs allow GUI designs to modify state safely without exposing implementation details.

### Key Definitions
| Term | Definition |
|------|------------|
| **Getter** | Function exposed as public API to retrieve internal data (e.g., `GetValue()` returns current value; prevents external modification) |
| **Setter** | Function that accepts new values via .NET's property setter syntax; may perform validation before updating internal state in OAP GUI applications |
| **Property Access** | Encapsulated read/write mechanism for fields using getter/setter functions (.NET 5+ feature allows direct property access without explicit `Get/Set` calls) |

### Core Concepts
1. **Validation Control**: Setter functions enforce rules (e.g., "temperature must remain > 0°C") during updates—prevents logical errors through controlled state transitions in OAP designs
2. **Property Syntax** vs Explicit Functions: .NET 5+ provides syntax sugar (`public double Temperature { get; set; }`) for getter/setter convenience—but underlying implementation remains encapsulated behind internal logic in C# code reviews
3. **State Change Logging** | Access functions may trigger side effects (e.g., incrementing meter counters) when state is modified—useful for OAP debugging/auditing GUI app behavior across project boundaries

### Main Content

#### Property & Function Pattern Comparison (.NET C# OOP Design)

```csharp
// Visual Studio generated code for access functions in .NET context
{
    public class TemperatureSensor {
        private double _internalReading = 0.0; // Encapsulated internal state visible only via getter/setter methods in GUI app

        // Explicit getter function returns current internal value (read-only access to data) through OAP API surface  
        public double OnGetValue() => _internalReading; 

        // Setter function accepts new value via try-catch pattern for validation before update—ensures safe state modification across project boundaries in .NET GUI apps  
    }
}
```

#### Access Function vs Direct State Modification (.NET Runtime Pattern)

| Feature | Getter/Setter (Function Call Pattern) | Direct Property/Field Access (`.NET` API Behavior) |
|---------|--------------------------------------|-----------------------------------------------------|
| **Validation** | Setter function may include logic (`if input > threshold`, throw exception if invalid)—ensures OAP integrity checks via helper methods before updating state | No validation enforced—direct access bypasses all internal logic; GUI apps can corrupt internal state (.NET runtime allows but not recommended) |
| **Side Effects** | Getter may trigger callbacks (e.g., console output); setter may log changes for debugging purposes in OAP designs | Direct access has no side effects beyond modifying internal storage; .NET runtime doesn't notify other components of state change unless explicitly configured |
| **Encapsulation Safety** | GUI apps cannot inadvertently bypass validation logic (.NET IDE warns against accessing private members during code review) | Direct field modification violates encapsulation (OAP design principle); compiler still allows access but breaks intended OAP boundaries in .NET projects |

### Examples and Applications

#### Example 1: Getter/Setter Pattern Implementation (.NET C# Code Pattern)

```csharp
// File: AccessFunctionPatterns.cs (Visual Studio auto-generated template structure demonstrating property getter/setter OOP patterns in C#.NET context)
{
    public class TemperatureSensor {
        private double _internalReading = 0.0; // Encapsulated data visible only via getters/setters for GUI apps

        // Getter: returns internal value with no side effects—read-only access pattern (.NET API design) 
        public double OnGetValue() => _internalReading; 
        double GetValue() => GetReading(); // Property accessor method using getter function internally (syntax sugar variant in .NET 8+)

        // Setter: performs validation before updating internal state via OAP encapsulation design patterns  
        public double SetTemperature(int newVal, ref double outputVal) { 
            if (newVal > 100 || newVal < -50) {
                throw new Exception("Error: Temperature out of range! Range [±50°C]"); // Throws exception to GUI app during OAP handling for input validation  
            }

            _internalReading = newVal; 
            return newVal; 
        }

        // Alternative: explicit property syntax (C# 7+ feature—simplifies getter/setter usage) 
    }
}
```

### Examples and Applications

#### Example 2: Property Pattern Syntax (.NET Compiler Behavior in OAP Context)

```csharp
// File: SyntaxPropertyUsage.cs (Visual Studio auto-generated template structure demonstrating property access patterns in C#.NET context)
{
    public class TemperatureSensorWithSyntax {
        private double _internalReading = 0.0;

        // Property accessor with getter function—exposes value without exposing internal state details for GUI apps  
        public double Temperature { get => OnGetValue(); } 

        // Setter method accepts new value via `.NET` property setter syntax (syntax sugar over explicit function calls in C# OAP design)
        public void SetTemperature(int newVal, bool allowValidation = true) { 
            ValidateInput(newVal); 
            _internalReading = newVal; // Updates internal state through encapsulation barrier  
        }

        // Helper method performs validation logic internally (protected from GUI app direct access via private scope modifier in .NET runtime)
    }
}

// File: PropertyPatternExample.cs (Visual Studio generated code for property pattern usage in C#.NET OAP design patterns)
{
    public class TemperatureSensorProperty {
        // Getter function returns current value; setter enforces rules before update via OAP encapsulation design  
        private double _internalReading = 0.0; 

        public double OnGetValue() => _internalReading; // Read-only access pattern for GUI app consumers across project boundaries  

        // Setter method: accepts input, validates range, updates state—prevents direct field access from corrupting OAP integrity
        public void SetTemperature(double newVal) { 
            ValidateValue(newVal); // Calls internal helper method for validation before updating internal reading value in .NET runtime  
        }

        private void OnValidateInput(int newVal, float min, float max) => 
            Console.WriteLine($"Validating input: minimum {min}, maximum {max}"); // Hidden from external consumers via private modifier in .NET OAP design
    }
}
```

### Important Notes & Reminders

- **Validation Responsibility**: Setter functions should always validate inputs; don't assume GUI app input is correct (.NET IDE warning: "Invalid input range detected")
- **Property vs Getter/Setter**: `.NET` properties are syntactic sugar for getter/setter functions—underlying implementation remains encapsulated via private/internal modifiers in C#.NET projects
- **Exception Handling**: Setters should throw meaningful exceptions (not silent failures) when validation fails; GUI apps catch these during OAP event handling patterns

## Quiz / Review Questions
1. What is the primary difference between property syntax (`public double Temp {get;set;}`) and explicit getter/setter method calls (.NET C# context)?
2. Why should setters always include validation logic rather than accepting arbitrary values from GUI applications in OOP design (e.g., "set temperature to -999°C")?
3. How can you trigger side effects (e.g., increment an internal counter) when a setter method is called from a .NET GUI app—this improves OAP debugging/auditing across project boundaries?
4. What happens if your setter function throws an exception while trying to update internal state in a GUI application (.NET runtime response)?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_PropertyPatternSyntax]] [[#Reference_ValidationLogicInCSharp]]
