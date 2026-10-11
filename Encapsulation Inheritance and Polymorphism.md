# Encapsulation, Inheritance, and Polymorphism in C# for Embedded Applications

These are the three fundamental pillars of Object-Oriented Programming (OOP). Understanding them is crucial for designing robust C# embedded applications.

## 1. Encapsulation

**Encapsulation** bundles data (fields/properties) and methods together within a class, making them accessible only through defined interfaces. This protects internal state from accidental interference.

```csharp
// Example: Encapsulated sensor class
public sealed class TemperatureSensor {
    // Fields - NOT directly accessible outside the class
    private int reading;
    
    // Public accessor properties - controlled access to data
    public int Value { 
        get => reading;              // Get the internal value
        set {                        // Set a new value with constraints
            if(value < 0 || value > 100) {
                Console.WriteLine("Value out of range");
            }
            else {
                reading = value;     // Update only through property
            }
        }
    }
    
    // Method to read from external device
    public void LoadReading() {
        this.reading = GetFromExternalDevice();  // Read via method
    }
}
```

**Why it matters for embedded:** It restricts what external hardware can modify and protects internal state by exposing only what's necessary.

---

## 2. Inheritance

**Inheritance** allows a child class to acquire the fields, methods, and behavior of a parent class, promoting code reuse while allowing customization.

```csharp
// Base class - common functionality shared by all
public abstract class Device {
    public void Initialize() { /* Default initialization */ }
}

// Child class - inherits from base but adds specific behavior
public sealed class Motor : Device {
    public override void Initialize() {
        base.Initialize();        // Calls parent's method
        this.enabled = false;     // Sets up motor-specific state
    }
    
    public void StartMotor() { /* Motor-specific logic */ }
}

// Another child class
public sealed class Sensor : Device {
    public override int GetReading() { /* Returns sensor reading */ }
}
```

**Why it matters for embedded:** Creates a hierarchy where base classes define common interfaces, while specialized subclasses handle different hardware types.

---

## 3. Polymorphism

**Polymorphism** means "many forms". Objects of different types may behave consistently under the same method calls but with different implementations based on the object's type.

```csharp
// Base class interface - common behavior defined abstractly
abstract public class Device {
    // Method signature: return type and parameter signature are defined
    public virtual void Actuate()
}

// Two types of devices implementing polymorphism
public class Motor : Device { 
    public override void Actuate() { /* Start/stop motor */ }
}

public class Display : Device {
    public override void Actuate() { /* Show current screen */ }
}

// Code that works with any device type - no code changes needed!
void DoWork(Device d) { 
    // This function call will execute different logic for each type of device:
    
    Motor motor = new Motor();
    Display display = new Display();
    
    // Call this method on either motor or display
    motor.Actuate();           // Executes as Motor's Actuate()
    display.Actuate();         // Executes as Display's Actuate() 
}
```

**Why it matters for embedded:** Enables you to write code that works with any hardware type without hardcoding specifics. The device handles its own behavior through inherited or overridden methods.
