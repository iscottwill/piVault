# 6.5.Constructors

## Overview
Constructors in .NET C# are special methods invoked during object creation (.e.g., `new Sensor(type)`)—responsible for initializing internal state before an object becomes available to GUI apps. Constructors ensure consistent starting points for heterogeneous object collections by enforcing pre-condition checks across all instances created via OAP design patterns in .NET runtime.

### Key Definitions
| Term | Definition |
|------|------------|
| **Constructor** | Method with same name as class (e.g., `TemperatureSensor`) that runs during object creation to initialize internal state before first use in OAP GUI app design |
| **Default Constructor** | Parameterless constructor (.NET runtime allocates minimum resources; initializes variables to default values for empty GUI apps without user input during startup) |
| **Parameterized Constructor** | Constructor accepting parameters (e.g., `TemperatureSensor(double)`); allows customization of state at creation time for OAP designs requiring different initial conditions in .NET context |

### Core Concepts
1. **Object Initialization** | Constructors run before object becomes accessible to GUI apps—ensures consistent starting point across multiple instances created via OOP design (e.g., temperature sensors all start at same default value or with user-provided input)
2. **State Pre-conditions**: Parameterized constructors can validate inputs upfront (.e.g., reject negative temperatures); prevents invalid state from being stored in internal fields before GUI apps use object in event handlers
3. **Inheritance Hierarchy** | Derived class constructors may invoke base class constructor (e.g., `SensorDerived(this)` or `: base(defaultTemp)`), ensuring OAP applications properly initialize parent classes during instance creation across project boundaries

### Main Content

#### Default vs Parameterized Constructor Patterns (.NET C# Design)

```csharp
// Visual Studio generated code for constructor patterns in .NET context
{
    public class TemperatureSensor {
        private double _internalReading = 0.0; // Encapsulated internal state—initialized via constructor logic (default or parameterized)

        // Default Parameterless Constructor: creates instance with default values (.NET runtime initializes to zero by default if no field assignment occurs in OAP GUI apps)  
        public TemperatureSensor() => 
            Console.WriteLine("Created sensor instance with default state (zero/empty reading)");

        // Parameterized Constructor: accepts initial value for user customization
        public TemperatureSensor(double initialValue) {
            ValidateInput(initialValue); 
            _internalReading = initialValue;
        }

        // Constructor runs before object becomes usable by GUI app in event handlers across project boundaries in OAP design pattern
    }
}
```

#### Default vs Parameterized Behavior Comparison (.NET Runtime Pattern)

| Feature | Default (Parameterless) Constructor | Parameterized Constructor | GUI App Usage Pattern |
|---------|-----------------------------------|---------------------------|----------------------|
| **Initialization** | `.NET` runtime initializes all fields to default (.e.g., 0.0, null)—enables empty object creation for OAP designs when user hasn't provided input yet at startup | Accepts constructor parameter (e.g., `25°C`) for custom state; validates input before initializing internal data across project boundaries | Use default for empty sensors; use parametric when GUI app needs sensor initialized with specific values from user input in .NET context |
| **Validation** | May have minimal pre-validation (.e.g., check for null reference) or none at all for OAP apps requiring flexibility during startup phase | Validates provided value against allowed range (e.g., "reject if < 0°C"; throws exception if invalid in C# design pattern) | GUI apps can accept user input in parameterized constructor; validate before assigning to `_internalReading` in .NET code review cycles |
| **State Access** | Object becomes usable immediately after instantiation—GUI app can begin reading data (e.g., call `OnGetValue()` right away if initial state is 0°C) | Same as default, but with user-provided starting value; GUI callback patterns reflect initial state from constructor parameter passed in OAP design | Choose constructor type based on when GUI app has received valid input for object initialization (.NET IDE behavior enforces compile-time checks for both scenarios in C# design)

### Examples and Applications

#### Example 1: Constructor Usage Patterns (.NET C# OAP Design)

```csharp
// File: DefaultVsParametricConstructor.cs (Visual Studio auto-generated template structure demonstrating default/parameterized constructors in .NET context)
{
    class TemperatureSensor {
        private double _internalReading = 0.0; // Encapsulated internal state—initialized by constructor parameters

        // Parameterless constructor: creates instance with empty/default state (.NET runtime ensures all fields get initial value (often zero))  
        public TemperatureSensor() => 
            Console.WriteLine("Sensor created without user input (default reading: " + _internalReading);
    }

    // Parameterized constructor: accepts input from GUI app at runtime for custom initialization values in OAP design patterns across project boundaries  
    public TemperatureSensor(double initialValue) {
        ValidateInput(initialValue); 
        _internalReading = initialValue;

        // Constructor ensures object is usable immediately—no need for post-constructor initialization in GUI apps (state ready on first use via callback)
    }
    
    // Validate input range prevents invalid values from corrupting internal state in .NET runtime design pattern  
}
```

### Examples and Applications

#### Example 2: Constructor Validation Logic (.NET Runtime Behavior)

```csharp
// File: ConstructorValidation.cs (Visual Studio auto-generated template structure demonstrating parameter validation patterns in C#.NET context)
{
    public class TemperatureSensor {
        private double _internalReading = 0.0;

        // Parameterized constructor with validation logic (reject out-of-range inputs to protect internal state across GUI app OOP designs)  
        public TemperatureSensor(double initialValue) {
            if (initialValue < -100 || initialValue > 500) {
                throw new ArgumentOutOfRangeException("initialValue must be within [-100°C, +500°C] range"); // Throws exception during initialization for invalid constructor args in GUI app pattern  
            }

            _internalReading = initialValue; // Assign valid value to internal state—prevents null reference errors later during .NET runtime object lifetime
        }

        // Parameterless constructor with no validation (safe default choice when user hasn't provided input yet at startup in OAP designs)  
    }

    // Validation pattern ensures consistent starting point for all instances created via OAP design cycles across project boundaries
}

// File: ConstructorDesignPattern.cs (Visual Studio auto-generated template structure demonstrating factory method + constructor patterns in C#.NET context)
{
    class FactoryMethodCreation {
        public static TemperatureSensor CreateSensor(string inputType, double defaultTemp = 0.0) => 
            inputType == "Custom" ? new TemperatureSensor(defaultTemp * inputType) : new TemperatureSensor(); // Factory method selects constructor type based on OAP design requirements

        // GUI app passes user input to factory—factory delegates to appropriate constructor (default or parametric) in .NET code review cycles
    }
}
```

### Examples and Applications

#### Example 3: Constructor Lifecycle Order (.NET Runtime Pattern)

| Phase | Behavior via Constructors in OAP Design | .NET Runtime Effect |
|-------|-----------------------------------------|--------------------|
| **Construction Start** | Parameterless constructors may use empty initialization; parameterized constructors validate first (C# compile-time checks enforce validation before state assignment in GUI apps) | Constructor execution begins—but may throw exception if pre-condition check fails during .NET runtime analysis |
| **Execution** | Both default and parametric run sequentially—internal field values get initialized before GUI app can use object via callbacks across project boundaries in OAP design patterns | After constructor finishes (even on exception), object remains unusable until error handling resolves via try-catch; GUI app cannot access uninitialized fields safely in C# code review cycles |
| **Cleanup (Optional)** | Constructors may also perform resource acquisition (.e.g., open file handle for embedded device reading); destructor handles cleanup if exceptions occur during lifecycle in OAP applications | Constructor runs before object becomes usable—ensures pre-conditions met before GUI app logic executes across project boundaries in OAP design cycles |

### Examples and Applications

#### Example 4: Multiple Constructors vs Parameterless (.NET OAP Design)

| Scenario | Code Usage | Effect on OOP Design | .NET Runtime Behavior |
|----------|-----------|----------------------|-----------------------|
| **Default (Parameterless)** | `new Sensor()` for empty initialization when user hasn't provided input; GUI app uses fallback logic later in event handlers after constructor completes | Enables instant creation of minimal objects without user input; `.NET` sets all unused fields to default values (e.g., 0) during OAP design cycles | No validation required—safe for initial object creation when user input is unknown; internal state starts at zero/empty until GUI app provides valid values across project boundaries in C# code review |
| **Parameterized** | `new Sensor(userInput)` when GUI app has received and validated input; constructor ensures only valid inputs reach internal state | Enforces pre-condition checks before object becomes usable by event handlers; GUI app handles validation in parameterized range check via try-catch patterns | Throws `ArgumentOutOfRangeException` if invalid value passed to constructor—prevents corrupting internal `_internalReading` field across project boundaries in OAP designs for GUI apps |

## Quiz / Review Questions
1. What is the primary difference between a default (parameterless) constructor and a parameterized constructor when creating objects in .NET C# applications?
2. How can you validate user input before it reaches an internal state field (e.g., `_internalReading`)—what exception does constructor throw if validation fails in a GUI app pattern (.NET runtime)?
3. If your application uses multiple instance types across project boundaries—how do constructors ensure consistent initialization behavior (OAP design principle in C# context)?
4. Why should you prefer parameterized constructors over default for critical state fields when user input is available at GUI startup (OOP encapsulation benefits in .NET code review)?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_DefaultVsParametricConstructor]] [[#Reference_InheritanceConstructorOrdering]]
