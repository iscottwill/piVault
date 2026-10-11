# Parameterized (Custom) Constructors in C# for Embedded Applications

A parameterized constructor accepts one or more arguments during object creation, allowing you to initialize your object with custom or runtime values. This provides flexibility for different scenarios or types of initialization.

## What is a Parameterized Constructor?

A parameterized constructor:
- Takes arguments/parameters when the object is created (`ClassName(arg1, arg2, ...)`), not just `new ClassName()`
- Allows customization during creation instead of relying entirely on default values
- Useful for setting up objects with specific initial states based on input data
- Can coexist alongside parameterless (default) constructor in the same class

## Why Use Parameterized Constructors?

| **Scenario** | **When You Need Parameterization** |
|--------------|-----------------------------------|
| Setting custom initial value | `new Sensor(25.0f)` vs `new Sensor()` |
| Creating multiple types/configurations from one base class | `new Motor(speed=1000)` |
| Handling validation at startup (passing data to validate) | Passing sensor ID, range, thresholds during constructor call |

## Syntax of Parameterized Constructors in C#

```csharp
// Default syntax – one parameter passed to set internal state
public sealed class TemperatureSensor {
    private float _reading = 0f;        // Internal storage
    
    public TemperatureSensor(float initialValue) {          // Takes custom initial value (not default)
        Validate(initialValue);              // Ensure the passed value makes sense
        
        if (initialValue < 0 || initialValue > 100) {                   // Check validity
            Console.WriteLine("Temperature out of range");             // Log error message
        }
        else {
            this._reading = initialValue;     // Store it in internal storage
        }
    }
    
    public TemperatureSensor() {                // Also have a default parameterless constructor
        Validate(0f);                        // Set default value if no argument passed
        
        this._reading = 0.15f;              // Use default initial value
    }
}
```

## Example: Parameterized vs Default Constructor Usage

```csharp
// Create object with custom initial value (via parameterized constructor)
TemperatureSensor s1 = new TemperatureSensor(25.0f);        // Start at 25°C, custom value

// Create object with default parameters (parameterless constructor runs instead)
TemperatureSensor s2 = new TemperatureSensor();           // Starts at default value for this class

// The two objects are distinct instances with potentially different initial states!
s1.Readings.GetReading();                    // Returns the reading from first sensor
s2.Readings.GetReading();                    // Returns a different reading (initialized differently)
System.IO.File.WriteAllText("sensors.txt", $"Temp 1: {s1.Value}, Temp 2: {s2.Value}");    // Write custom values each time
```

## How Parameterized Constructors Work Internally in C# Embedded Development

### Syntax and Usage:

```csharp
// Create multiple objects with different parameterizations
Motor m1 = new Motor(speed: 500, enabled: true);          // Custom constructor with parameters
Sensor s1 = Sensor.Create(0.5f, 100f);           // Using factory method (equivalent to custom constructor logic)

// Parameter values are passed directly into the constructor method at runtime!
```

### Steps When Parameterized Constructor Runs:

When creating `new Sensor(initialValue)` with a parameterized constructor:

1. **Memory Allocation**: Heap memory allocated for new object instance(s) → same as default constructor
2. **Internal Fields/Properties Initialization**: Internal storage is set up (usually zero or minimum valid value)
3. **Parameterized Constructor Code Execution**: User-defined constructor method (`Constructor(arg1, arg2)` runs), passing custom values into internal state initialization
4. **Output Parameters Stored**: Passed values passed into internal variables (via `this.variableName = value`)
5. **Internal Setup Complete**: Object ready to use (internal variables correctly configured)

## Parameter Constructors vs Default Constructor: Benefits and Tradeoffs

| **Feature** | **Parameterized Constructor** | **Default Constructor** |
|-------------|-------------------------------|-------------------------|
| Flexibility | Yes, sets custom initial values | No, uses class defaults |
| Simplicity for users | Higher – requires passing arguments when needed. | Easier – no arguments needed! |
| Validation at startup | Possible (validate passed parameters) | Less direct validation unless helper code is included |
| Use cases | Custom configuration or initialization based on runtime input | Creating objects quickly without specifying values |

## When NOT to Use Parameterized Constructors for C# Embedded Development?

- ❌ Your embedded devices only need the same default value for every sensor object (parameterization adds complexity unnecessarily)
- ❌ You have limited heap memory and creating many objects with expensive parameter initialization could cause OOM scenarios
- ✅ If you prefer factory methods or constructor patterns, use static methods that simplify object creation

Use parameterized constructors when you want users to pass custom input directly into your class initialization logic!
