# 6.5.2.ParameterizedConstructor

## Overview
Parameterized constructors accept specific values to initialize internal state before an object becomes usable by GUI apps in .NET C#. Unlike default constructors (zero/empty), parameterized constructors enforce pre-conditions—validating inputs against acceptable ranges to prevent corrupting internal data across object collections created via OOP design patterns in .NET runtime context.

### Key Definitions
| Term | Definition |
|------|------------|
| **Parameterized Constructor** | Constructor accepting explicit parameters (e.g., `public Sensor(string initialValue)`)—validates input before initializing internal state for GUI apps across project boundaries in OAP design cycles |
| **Input Validation** | Constructor checks provided values against constraints (.e.g., temperature must be >= -100°C); throws exception if validation fails to reject invalid parameters for unsafe object states in .NET code review |
| **Pre-Condition Enforcement** | Constructor guarantees required state before object becomes accessible via callbacks—prevents runtime errors from uninitialized or incorrectly initialized fields in OAP GUI applications designed across multiple projects using C#.NET design principles |

### Core Concepts
1. **State Validation Upfront**: Parameterized constructors can reject invalid inputs immediately (before object even enters heap)—saves GUI app time on error handling later during OOP event handler execution in C# runtime patterns
2. **Custom Initialization Logic**: Accepting user-provided parameters allows creating objects with tailored starting states (e.g., `Sensor(25°C)` vs `Sensor(-10°C)`—OAP design enables heterogeneous object collections for different GUI scenarios across project boundaries)
3. **Derivation Support**: Derived classes can specify base constructor parameters (.e.g., `SensorDerived(double inheritedTemp)`)—ensures proper inheritance chain initialization via this pattern in .NET JIT-compiled OOP applications running across multiple projects

### Main Content

#### Parameterized Constructor vs Default (.NET C# Runtime Comparison)

| Feature | Default Constructor (Parameterless) | Parameterized Constructor | OAP Design Impact |
|---------|-------------------------------------|---------------------------|-------------------|
| **State Initialization** | All fields start at zero/null (`.NET` runtime guarantees for numeric/string types in .NET IDE context) | Custom values passed via constructor parameters—validated before assignment to internal state across project boundaries | Parameterized enables GUI apps that require user-provided initial conditions during startup phase in C# design cycles |
| **Validation Timing** | Minimal/pre-computed validation (safe fallback when input unavailable; zero/empty always usable by GUI event handlers for OAP designs) | Full validation performed before field assignment—rejects invalid inputs to constructor call prevents unsafe initialization across multiple objects created via .NET runtime in OAP GUI apps | Rejecting invalid params at constructor stage saves time on post-construction error handling (try-catch blocks fewer occurrences in C# code review) |
| **Exception Handling** | `.NET` may throw `NullReferenceException` only if object accessed before fields initialized; default prevents this via guaranteed zero-init pattern | May throw `ArgumentOutOfRangeException` during constructor—prevents unsafe state creation entirely for GUI apps designed with defensive programming practices across project boundaries | Throws happen early (.e.g., during object creation)—makes debugging easier in .NET IDE cycles (exception traceback points to line where invalid param passed) vs runtime errors later in event handlers |

```csharp
// File: ConstructorPatternComparison.cs (Visual Studio auto-generated template structure demonstrating default vs parameterized constructor comparison across OAP design scenarios in C#.NET runtime context)
{
    class TemperatureSensor {
        private double _internalReading; 

        // Parameterless: creates empty object with zero state—usable immediately by GUI app regardless of user input availability in OAP design cycle  
        public TemperatureSensor() { 
            Console.WriteLine("Default constructor created (zero reading, minimal resources)"); 
        }

        // Parameterized: accepts custom value—if invalid, throws constructor-time exception preventing unsafe state creation across project boundaries in .NET IDE context
        public TemperatureSensor(double initialReading) {
            ValidateInput(initialReading); 
        }

        private void ValidateInput(double val, float min, float max) => 
            Console.WriteLine($"Validating input: {max}, minimum {min}... (Validation fails if value out of range for GUI app OOP design patterns)"; 
    }
}

// File: ParameterizedConstructorUsage.cs (Visual Studio auto-generated template demonstrating parameterized constructor invocation via .NET runtime analysis in C# context)
{
    class ParametricUsagePattern {
        // Valid input: constructor executes normally, internal state receives user value across multiple OAP GUI app instances designed for different temperatures in project boundaries  
        public void OnInstantiateValid() { 
            TemperatureSensor s1 = new TemperatureSensor(25); // Valid param: 25°C—constructor completes successfully
            Console.WriteLine($"Created with valid input (state = 25.0)"); // Internal field assigned after validation passes

            // Invalid input: constructor throws exception immediately; object not created (.NET runtime prevents creation of corrupted state across project boundaries in OAP designs)  
        }
    }
}
```

### Examples and Applications

#### Example 2: Parameterized Constructor Benefits in .NET GUI Apps

| Benefit | Behavior in OAP Design | Code Pattern | GUI App Impact |
|---------|------------------------|--------------|----------------|
| **Early Validation** | `.NET` checks params before field assignment—catches user errors immediately at startup phase in C# IDE cycles across project boundaries | `new Sensor(userInput)`. Throw exception if invalid; object not created with corrupted state for OAP designs requiring consistent starting point | Users notified of bad input quickly (error message visible during app launch, not after runtime failures) — saves debugging time in .NET development cycle patterns  
| **Consistent Initialization** | All instances receive validated starting state—prevents uninitialized field access errors across GUI app collections created via `.NET` constructor calls in OAP pattern | Parameterized constructor ensures same validation rule applied to every `new Sensor()` call; consistent behavior across all objects in project boundaries | Reliable object pool usage (.e.g., 10 sensors initialized with valid values) prevents sporadic crashes from invalid field access during event handler execution in .NET runtime cycles  
| **Custom State Control** | GUI designer can specify initial temperature/scale—no need for later manual initialization via setter methods across multiple projects designed with OOP encapsulation patterns | `new TemperatureSensor(30.0)` directly; constructor guarantees correct starting state before object becomes available to GUI app for use in callbacks | Flexible OAP designs—different sensors initialized differently based on user design; no extra work needed to set initial values after instantiation via callback pattern  
| **Inheritance Chain** | Derived class constructors call base constructor with params (implicit or explicit `.NET` runtime enforces proper initialization order for OAP patterns across classes) | `class SensorDerived : TemperatureSensor { public SensorDerived(double customVal) : base(customVal); }` — parameter passed through chain; all levels initialized properly across project boundaries | Ensures derived class objects have properly configured base state; critical for GUI apps requiring multiple class types initialized consistently for callbacks  
| **Defensive Design** | Invalid params rejected—prevents silent null/zero state corruption in GUI events (OAP design principle: reject bad data before it enters system) | Throw immediately on invalid input; GUI app handles error gracefully via try-catch without creating corrupted objects during .NET IDE cycles | Clean separation of valid/invalid states across object lifecycle—simplifies debugging and testing for GUI application patterns in C# code review cycles  

### Important Notes & Reminders

- **Error Handling**: Constructor throw (`throw` keyword) prevents object creation entirely when validation fails (.NET runtime behavior); GUI app may need to retry or ask user for valid input (OAP design pattern for error handling)
- **Try-Catch Block**: Wrapping constructor call in try-catch handles invalid params gracefully; OAP apps may log errors and continue with fallback objects if valid data unavailable (.NET runtime supports this pattern across all project boundaries)
- **Validation Method Placement** | Validation should occur before any state assignment; `.NET` compiler enforces proper order. If validation fails, `_internalReading` never gets assigned—object remains unusable for GUI app callbacks until fixed input provided  
- **Multiple Constructors Pattern**: .NET supports both default and parameterized constructors (same class can have multiple)—GUI apps choose based on data availability; constructor selection determines initial state across project boundaries in OAP design patterns  

## Quiz / Review Questions
1. Why should you prefer throwing an exception within a parameterized constructor when input validation fails—rather than setting field to null or zero? 
2. How does .NET differentiate between default (zero-initialized fields) and parameterized (custom values) constructors during object creation across multiple GUI projects in .NET runtime context?
3. In what scenario would a GUI app benefit from using a parameterized constructor with strict input validation versus letting the default (zero) state apply temporarily until valid input becomes available (.OAP design principle)?
4. What happens to internal fields when a constructor's validation method throws—does the object get created at all? (Answer: `.NET` runtime prevents creation; no corrupted object exists in memory for OAP patterns across projects using C#.NET)

---
**Related Topics:** [[E230_OOPr]] [[#Reference_DefaultConstructorUsage]] [[#Reference_ConstructorValidationBehavior]]
