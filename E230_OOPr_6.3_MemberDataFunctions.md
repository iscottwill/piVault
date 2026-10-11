# 6.3.MemberDataFunctions

## Overview
Member data and functions in .NET OOP encapsulate internal state (fields/properties) and behavior (methods) into cohesive units. Understanding the distinction between "public API" (accessible by GUI apps without exposing internal implementation details) and "private/internal" members (hidden implementation logic protected from direct access) is essential for designing maintainable C# applications that prevent unintended side effects through proper encapsulation patterns.

### Key Definitions
| Term | Definition |
|------|------------|
| **Public API** | Exposed methods/properties (getters/setters, public functions) via which external GUI apps interact with internal class state in OOP designs |
| **Private/Internal Members** | Internal implementation details hidden from external access; protected only via .NET's `private`, `internal` modifiers during compilation |
| **Getter/Setter Pattern** | Property access controlling whether internal data (fields) can be modified directly vs through controlled logic in C#/.NET context |

### Core Concepts
1. **Encapsulation vs Exposure**: GUI apps should interact with classes via public API surface—never directly manipulate private/internal members unless using reflection (dangerous and non-OOP design pattern)
2. **Public Function Contracts**: OAP applications depend on consistent method signatures for input/output (e.g., `OnSetTemperature(int newVal)` returns void, no errors thrown for valid input)
3. **Helper Methods vs Public API**: Internal utility functions (helper methods) may perform auxiliary computation but are not exposed directly to GUI app consumers in .NET designs

### Main Content

#### Member Access & Function Pattern Comparison (.NET C# OOP Design)

```csharp
// Visual Studio generated code for member data/function patterns in .NET context
{
    public class TemperatureSensor {
        private double _reading = 0.0; // Internal state (private, not directly accessible via external GUI app methods) 
        
        // Public getter exposes reading value to OAP client via controlled method access pattern  
        public double OnGetReading() => _reading; 

        // Public setter ensures only validated values can update internal state via .NET API constraints in OOP design  
        public void OnSetTemperature(double newVal, bool allowValidation = true) { 
            ValidateValue(newVal); 
            _reading = newVal; 
        }

        // Internal helper function (private/internal scope only)—not part of public API surface for GUI apps  
    }
}
```

#### Public vs Private Function Access Patterns (.NET OOP Design)

| Feature | Public API Method | Private Helper Function | Code Pattern in .NET Context |
|---------|-------------------|------------------------|------------------------------|
| **Access Scope** | `public` modifier (accessible from GUI app across OAP project boundaries via .NET's cross-class method calls) | `private/internal` only accessible within class scope—hidden from external consumers during compilation |
| **Purpose** | Controlled behavior interface for GUI apps to call methods without knowledge of internal logic (.NET encapsulation protects implementation details from direct manipulation) | Utility logic (e.g., validation, conversion); called by public API but not exposed as part of .NET's public API surface in C# OAP applications |
| **Error Handling** | May throw exception if input invalid (enforce contracts externally); GUI apps can catch and handle errors via try-catch blocks in OOP design patterns | Never throws to external consumers; may log internal errors silently via internal logger class patterns |

### Examples and Applications

#### Example 1: Public API vs Helper Method Usage (.NET C# Pattern)

```csharp
// File: TemperatureSensor.cs (Visual Studio auto-generated template structure demonstrating public API + private helpers in C#.NET OOP design)
public class TemperatureSensor {
    /** 
     * Internal state field (_reading) holds actual temperature value
     * GUI app interacts via public API: OnGetReading(), OnSetTemperature()—not direct access to _field variable
     */
    private double _reading = 0.0;

    // Public API getter/validator ensures only valid values can be written (e.g., > 0, <= 100) via .NET property constraints  
    public double OnGetReading() => _reading; // Returns current value via controlled access in OAP design

    // Public setter with validation method—prevents arbitrary modifications to internal state from GUI applications  
    public void OnSetTemperature(double newVal, bool allowValidation = true) { 
        if (allowValidation) {
            ValidateRange(newVal); // Calls internal helper for range check (private/internal scope only)
            _reading = newVal; 
        }

        if (!ValidateRange(newVal)) { /* Validation fail—exception logic in OAP app */ return; }
    }

    // Private helper method (internal scope only)—not part of public API surface; GUI apps can't call this directly in .NET context  
    private void ValidateRange(double input) => 
        (input > -50 && input < 150) ? Console.WriteLine("Value valid. Setting to: " + input) : Console.WriteLine("Error: Out of range"); // Hidden from external OAP app access
}

// File: TemperatureSensorHelpers.cs (Visual Studio template structure for helper function patterns in C#.NET OOP design)
{
    class SensorHelper {
        public void OnCheckSensorReadings(TemperatureSensor sensorData, EventArgs e) => 
            Console.WriteLine($"Reading: {sensorData.OnGetReading()}"); // GUI app uses only public API surface (not internal helpers directly)
    }
}

// File: InternalHelpers.cs (Visual Studio auto-generated template for internal/protected helper methods within OAP classes in .NET context)
{
    class SensorHelperImplementation {
        private void OnValidateInput(double value, int minVal, int maxVal) => 
            Console.WriteLine($"Validating input: minimum {minVal}, maximum {maxVal}"); // Internal method not exposed to GUI app consumers via public API

        // Helper functions perform validation/conversion internally; public API wraps these for safer GUI interaction
    }
}
```

### Examples and Applications

#### Example 2: Helper Method vs Public Function Usage in .NET OAP Apps (.NET Design Patterns)

| Pattern | Implementation | Use Case in OOP Applications |
|---------|---------------|------------------------------|
| **Getter** | `.Get` method (e.g., `Sensor.GetValue()`) returns current state value via controlled access | GUI displays reading; exposes value without exposing storage mechanism details in C#.NET design pattern |
| **Setter** | `.Set` method (e.g., `Sensor.UpdateTemperature()`) ensures validation before modification | GUI modifies temperature only after user input passes validation logic internally in .NET OAP app |

```csharp
// File: GetterSetters.cs (Visual Studio auto-generated template structure demonstrating getter/setter OOP patterns in C#.NET context)
{
    class TemperatureSensor {
        private double _reading = 0.0;

        public int OnGetValue() => (int)_reading; // Returns value via controlled access method (public API surface)
        public void OnSetTemperature(double newVal) => _reading = newVal; // Internal setter—no external validation if GUI app trusts caller in OAP design

        // Internal getter/setter provides tighter control over state access for advanced OOP applications using reflection patterns in .NET code reviews  
    }

    // Helper method performs conversion/validation internally; GUI app doesn't need to know about internal logic during API usage
}
```

### Important Notes & Reminders

- **Avoid Reflection Access**: GUI apps should avoid reflecting/reading private fields directly (OAP design principle); use public API methods in .NET OOP context for maintainability across teams and IDEs
- **Validation is Essential**: Public setters must enforce constraints even when user input seems correct; helper functions handle validation logic internally so GUI apps don't expose implementation details (e.g., "Value range too high")
- **Protected Members**: `protected` members accessible to derived classes in inheritance—use for child class-specific access patterns (OAP OOP design) without exposing to external consumers
- **Internal Scope Difference** | Internal scope is project-level; private = assembly-only. In .NET cross-project apps, `.internal` allows helper methods across same project (not necessarily other projects)

## Quiz / Review Questions
1. What is the primary difference between a public getter method (.e.g., `GetValue()`) and accessing a private field directly in OOP C# design?
2. Why should GUI applications avoid using reflection to access internal/private class members during runtime (.NET IDE context)?
3. How can you implement validation logic for a public setter while keeping the validation details hidden from external consumers across project boundaries in .NET?
4. What is the role of helper/auxiliary methods (.e.g., `ValidateInput()`) versus public API methods in OAP design patterns for encapsulated classes?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_VirtualMethodOverrides]] [[#Reference_PrivateMemberAccess]]
