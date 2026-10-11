# Objects as Instances of Classes in C# for Embedded Applications

In C#, you create objects by instantiating (creating) a class. These "instances" are the actual runtime entities that hold data and perform actions. Understanding object instances is crucial for building C# embedded applications.

## What is an Object Instance?

An **object** (instance) of a class represents:
1. A specific entity in your application (e.g., a particular motor instance, temperature sensor instance)
2. The state/data the class holds (private fields or properties)
3. The behavior/methods you can call on that specific object (public methods/properties)

## Creating Objects in C#

### Syntax

```csharp
// Create an object – use `new` to instantiate
TemperatureSensor s1 = new TemperatureSensor();    // Creates first sensor instance  
Motor m1 = new Motor();                              // Creates first motor instance

// Reuse the same class to make many different objects
Sensor s1 = new Sensor();
Sensor s2 = new Sensor();
Sensor s3 = new Sensor();

// Each object has its own independent data (storage)
s1.Value = 25.0f;        // Set value on first sensor
s2.Value = 30.0f;        // Set different value on second sensor
```

### Example: Multiple Instances with Different Data

```csharp
// Create three motor objects – each with its own internal state
Motor m1 = new Motor();           // Motor 1 instance (default initializers)
Motor m2 = new Motor();           // Motor 2 instance
Motor m3 = new Motor();           // Motor 3 instance

// Each object's speed is independent!
m1.SetSpeed(500);                    // Set motor 1 to RPM 500
m2.SetSpeed(1000);                   // Set motor 2 to RPM 1000 (independent!)
m3.SetSpeed(750);                    // Third instance is separate

// Change one doesn't affect the others!
m1.Speed = 500;                      // Only modifies m1's internal speed

Console.WriteLine(m1.ReadRPM());      // Motor 1: "500"
Console.WriteLine(m2.ReadRPM());      // Motor 2: "1000" 
Console.WriteLine(m3.ReadRPM());      // Motor 3: "750"
```

## What Happens When You Create an Object Instance?

When you write `new ClassName()`:

### Step 1: Memory Allocation (Heap)
The garbage collector allocates memory for your object on the heap.

### Step 2: Field Initialization (Instance State)
All fields and properties are initialized:
```csharp
public sealed class Motor {
    public int Speed { get; set; }
    private bool enabled = false;                    // Initialized with default value
}
// When you create a new instance, all fields/properties are created as new objects
Motor m1 = new Motor();
Motor m2 = new Motor();
m1.Speed = 500;                 // Sets data for Instance #1 (m1)
m2.Speed = 1000;                // Uses different internal storage, independent!
```

### Step 3: Constructor Call
Each instance constructor executes to set up specific initialization logic:
```csharp
public sealed class TemperatureSensor {
    public float Value => this._rawValue / 4.0f;   // Read from raw value
    
    private float _rawValue = 0f;                   // Default initial value (set by constructor)
    
    // Constructor initialization code executes for EVERY object instance created!
    public TemperatureSensor() {
        ValidateState();              // Call helper methods to validate input/output
        this._value = 25.0f;         // Set default sensor value
    }
    
    private void ValidateState() {   // Helper method runs during all instances
        if (this.value < 0) {
            throw new Exception("Value cannot be negative");
        }
    }
}

// Create instances – constructors initialize each one!
TemperatureSensor s1 = new TemperatureSensor();  // Instance #1 created: initialized with default value
TemperatureSensor s2 = new TemperatureSensor();  // Instance #2 created: separate internal state
```

## Common Patterns for Creating Multiple Instance Objects in C# Embedded Systems

```csharp
// Initialize multiple instances at startup (create all motors, sensors, etc.)

// Pattern 1: Instantiate and initialize sequentially
for(int i = 0; i < numberOfMotors; i++) {
    Motor m = new Motor();             // Create instance on heap
    m.SetDefaultSettings(i);           // Initialize with default values unique to this motor
}

// Pattern 2: Use constructor arguments to create customized instances
Sensor readout1 = new Sensor(true,   true, false);       // Create instance with custom configuration
Sensor readout2 = Sensor.Create(false, 0.5f);             // Factory method creates different settings
```

## Why Understanding Object Instances Matters in C# Embedded Development

Understanding objects as distinct instances:

### Memory Management
```csharp
// Each object has its own storage – separate memory allocation needed for each!
Motor m1 = new Motor();           // Allocates memory on heap (Object #1)
Motor m2 = new Motor();           // Allocates more memory (Object #2) – completely separate from Object #1!

// Changing one's state doesn't affect the other's internal memory!
m1.Speed = 500;       // Modifies only motor 1's data
m2.Speed = 1000;      // Only modifies motor 2's data (independent!)
```

### Object Lifetime
Objects persist until they are no longer referenced by any code. The garbage collector then frees the memory when they're no longer needed, reducing overall memory usage in embedded devices.

Creating and managing multiple objects correctly is a core competency required for writing efficient C# embedded applications—every new object instance consumes heap memory and has its own lifecycle!
