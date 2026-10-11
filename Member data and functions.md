# Member Data and Functions in C# Classes for Embedded Applications

Members of a class include both **member data** (fields, properties) and **functions** (methods, constructors). Understanding how these work together is essential for building maintainable embedded applications.

## What are Members in C#?

- **Member Data**: Variables that belong to a class instance (or object)
- **Functions/Methods**: Operations/functions you can call on the data/objects

Example: A `Motor` class might have:
- Member data: `int speed`, `bool enabled`, `float currentReading`
- Functions: `SetSpeed()`, `StartMotor()`, `ReadCurrent()`

## Accessing Member Data vs Methods

```csharp
public sealed class Motor {
    // Member DATA – properties/fields that store state
    public int speed { get; set; }          // Getter/Set property for access
    
    // Member FUNCTIONS – functions/methods you can call to interact with the object
    public void SetSpeed(int rpm) {
        // This method modifies internal state
        this.speed = rpm;
    }
    
    public void StartMotor() {         // Another function that acts on current data
        if(speed > 0 && enabled) {
            TurnOn(true);                // Call other methods
        }
    }
    
    // Member variables – private by default (accessible only within class itself)
    private int actualSpeed;           // Stores the real RPM value
}

// Using members of an object instance
Motor m1 = new Motor();             // Create a Motor object
        
m1.SetSpeed(500);                   // Call a function method
m1.speed = 1000;                    // Access member data directly or via property
```

## Key Concepts in Member Data and Functions

### Instance vs Static Members
- **Instance members**: Belong to each individual object (`this.speed`)
- **Static members**: Belong to the class itself, shared by all instances

### Public vs Private Members
```csharp
public class Sensor {
    // Public: Accessible from anywhere in code
    public int value;
    
    // Protected: Only accessible within same class hierarchy (derived classes)
    protected int internalValue;
    
    // Private: Only accessible within the class itself
    private int internalReading = 0;
    
    // Internal: Only accessible within your project/assembly
    internal int cachedValue = 50;      // Default in C#
    
    // Default access – only within same assembly/project (usually default)
    // Use public if you want it globally accessible, or use another access modifier
}
```

## Best Practices for Embedding Member Data and Functions

| **Best Practice** | **Why It Matters for Embedded** |
|-------------------|---------------------------------|
| **Use properties with getters/setters** | Protect internal state, enforce validation on writes |
| **Default access = private** | Avoid accidental public variable modifications outside your class |
| **Avoid exposing everything as functions** | Too many methods increases memory use; use property instead |
| **Minimize member data size** | Smaller classes use less memory and are faster |
| **Make static methods where appropriate** | Share reusable logic without creating extra object instances |

## Why It Matters for C# Embedded Applications

- Understanding member data vs functions helps you design efficient embedded programs that minimize memory usage
- Access modifiers (public/private) determine who can modify your device's state and how much control the system has over hardware
- Constructors, methods, and properties work together to create flexible, reliable systems that interface cleanly with hardware.

Member data and functions are the building blocks of C# OOP—combining data with its behavior through encapsulation.
