# Relationships Between Classes in C#"for Embedded Applications

Class relationships describe how different C# classes interact with each other through inheritance, composition, dependency injection, or collaboration patterns. Understanding these is essential for designing modular, maintainable C# embedded applications.

## What are Class Relationships?

Class relationships define organizational structures for your code:
- **Inheritance (Extends)**: One class derives from another ("is-a" relationship)
- **Composition (Has a)**: One class owns or contains another class ("has-a" relationship)
- **Interface/Contract**: Classes must implement defined interfaces (not directly shown here but related)

## Types of Class Relationships in C# Embedded Systems

### 1. Inheritance Relationship ("is-a")

**Definition**: A child class inherits from a parent class ("A is-a B").  
Example: `Motor` extends `Device`, meaning a Motor IS-A type Device (shared functionality).

```csharp
// Parent/Child inheritance – IS-A relationship
abstract public class Device {                        // Base class with common interface
    protected int _id;           // Internal storage
    public virtual void Start() { /* Shared base implementation */ }
}

public class Motor : Device {      // Extends Device (Motor IS-A Device)
    public override void Start() {                // Override parent method for specific device type
        Console.WriteLine("Starting motor: " + this.GetId());        // Call inherited method from parent!
        
        _id = 0;                     // Set to zero (default)
    }
}

// Create object – inherits all members from base class!
Device d = new Motor();                 // d has Device interface, but internally is a Motor instance    
d.Start();                              // Calls Motor's Start() due to polymorphism

// You can access base class data through parent type (polymorphic)
Motor m = d as Motor;        // Cast back down to Motor type if needed
```

**When to Use Inheritance**:
- ✅ Class must behave EXACTLY like a parent type ("is-a" relationship strongly required)
- ✅ Multiple inheritance is supported! You can extend multiple classes (like `Motor : Device, Peripheral`)
- ❌ Not ideal for "has-a" functionality (e.g., Sensor has a Display – use composition)

### 2. Composition Relationship ("has-a")

**Definition**: One class contains another class as part of its structure ("A has-a B").  
Example: A `Sensor` has a `Display`.

```csharp
// Base class defining interface
abstract public class Device {
    public abstract void Actuate() { /* Base implementation */ }
}

// Composition relationship – Sensor HAS-A Display (it contains one)
public sealed class Sensor : Device {
    private IControl _display;            // Has-a display! (Interface variable)
    
    public Sensor(ControlPanel controlDisplay) {     // Constructor receives display instance as input
        this._display = controlDisplay;        // Pass in display via constructor
        
        ValidateDisplay(this._display);              // Ensure interface implemented by passed-in object
    }
    
    override void Actuate() {  // Override inherited implementation
        _display.Actuate();           // Call method on HAS-a class (display)
        this._internalState = true;       // Set internal sensor state
    }
}

// In code using the Sensor with Composition relationship:
Sensor s1 = new Sensor(controlDisplay1);              // Create Sensor #1, displays data from controlPanel #1
Sensor s2 = new Sensor(controlDisplay2);              // Create Sensor #2, displays via different panel
```

**When to Use Composition**:
- ✅ When one object has a strong ownership relationship with another (you manage and dispose it)
- ✅ When the "has-a" object should not be shared across instances
- ✅ When the inner class might have lifecycle tied to the outer class!

### 3. Interface/Contract Relationship ("agrees on")

**Definition**: Two classes agree on a communication contract via interfaces, even if they don't share common parent!  
Example: `Sensor` and `Display` communicate though interfaces!

```csharp
// Define interface – shared contract across unrelated code
public interface ISensorReader {       // Interface (not a class)
    int ReadValue();                    // Method signature required by ALL implementing classes
}

// Implementing class #1 – inherits from Device but doesn't care about inheritance!
public sealed class TemperatureSensor : Device, ISensorReader {
    public override void Actuate() { /* Override if needed */ }
    
    // Implements interface methods alongside regular class definitions
    public override int ReadValue() {                    // Implement ISensorReader.ReadValue (not from base/child)
        return GetReading();              // Internal sensor gets reading, returns value
        
        Console.WriteLine("Reading: " + _rawValue);  // Output to user/external device as needed
    }
}

// Implementing class #2 – different type of device!
public sealed class Motor : Device, ISensorReader {      // Implements same interface as Sensor!
    public override void Actuate() { /* Override as appropriate */ }
    
    // Also implements read value (motor may provide motor readings via this method)
    public override int ReadValue() {              // Implements shared interface for both!
        return GetReading();                // Return current state (e.g., RPM from embedded device)
    }
}

// Use the two different types interchangeably – same interface, different implementations!
ISensorReader reader1 = new TemperatureSensor();       // Create sensor implementing interface
ISensorReader reader2 = new Motor();                    // Create motor also implementing same interface

int reading1 = ((ISensor)temp).ReadValue();            // Read from temperature sensor via shared interface
int reading2 = ((ISensor)motor).ReadValue();           // Read from motor (RPM) using same contract!
```

## Why Class Relationships Matter in C# Embedded Systems

### 1. Maintainability
- Inheritance and interfaces allow you to modify classes without breaking dependent code
- Interface changes affect all implementers – test thoroughly before implementing across multiple types

### 2. Design Flexibility
- Composition allows one object to own/control another's lifecycle (e.g., Sensor creates internal Display)
- Interfaces enable loose coupling (different sensor types share same interface).

### 3. Memory Efficiency
- Base class inheritance: Shared implementation in memory for all child classes!
- Interface implementations: No shared data, but reduces code duplication across multiple specialized sensors/devices.

## Relationships Summary Table

| **Type** | **"is-a"** | **"has-a"** | **Interface (Agrees on)** |
|----------|------------|-------------|---------------------------|
| **Example Class** | Sensor extends Device | Motor has-a Display | TemperatureSensor implements ISensorReader interface |
| **Memory Impact** | Child class uses parent's memory + new storage | Inner object uses separate memory, outer references it | Interface methods stored inline per class (no extra data allocation) |
| **Best for** | Shared functionality across child types | Strong ownership of resources | Decoupling related modules |

Understanding class relationships is key to building large, maintainable C# embedded applications where different components work together seamlessly through well-defined contracts and structures.
