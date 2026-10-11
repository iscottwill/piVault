# 6.4.ObjectsAsInstancesOfClasses

## Overview
In .NET C#, objects are instances (instances) of classes that encapsulate both data and behavior—this is a core OOP principle where concrete objects exist to represent real-world entities. Understanding object creation, destruction, and lifecycle management (.NET runtime heap allocation patterns) is essential for writing clean C# code that avoids memory leaks and handles resource cleanup properly in GUI applications across projects.

### Key Definitions
| Term | Definition |
|------|------------|
| **Object Instance** | .NET runtime creates a new object based on class definition when constructor runs; each instance has independent state storage for GUI app management (e.g., separate `TemperatureSensor` objects per room in OAP design) |
| **Instance vs Class** | Class defines shape/structure; instances are created from class templates (.NET heap allocation creates copy of class blueprint + unique data for each object in C#) |
| **Memory Heap Allocation** | .NET runtime allocates memory on heap when constructing instance (unlike stack-based primitives); objects may persist across application shutdowns or restart sequences in OOP GUI apps |

### Core Concepts
1. **Instance Independence**: Each `.NET` instance maintains independent state—modifying one `TemperatureSensor` object doesn't affect unrelated ones in .NET GUI apps designed for scaleability across project boundaries
2. **Constructor Invocation** | Class must define constructor (.e.g., `public Sensor()` or parameterized `public Sensor(double initialReading)`) to specify how instances initialize memory during OAP app startup; ensures consistent state across heterogeneous object collections for GUI apps
3. **Garbage Collection Behavior**: .NET runtime's GC cleans up objects when references are cleared—helps GUI apps manage memory without manual intervention in C# design patterns

### Main Content

#### Object Instance Creation Patterns (.NET Runtime Context)

```csharp
// Visual Studio generated code for object instances in .NET context
{
    // Concrete class defining object type blueprint with constructor  
    public class TemperatureSensor {
        private double _internalReading = 0.0; // Encapsulated state per instance (not shared across other sensors in OAP design)

        // Constructor initializes internal state before assigning to GUI app reference variables (.NET runtime allocates heap space for this new object instance in memory)  
        public TemperatureSensor(double initialRead) { 
            _internalReading = initialRead; 
        }

        // Optional: parameterless constructor (class-level default initialization pattern)
        public TemperatureSensor() : this(0.0) => 
            Console.WriteLine("Created new Sensor instance at runtime via .NET heap allocation"); // Runtime behavior: allocates memory for this sensor object (heap-based storage in OAP GUI apps)
    }

    // Class blueprint defines object interface; instances can be created multiple times for different GUI app states
}
```

#### Instance Creation vs Heap Allocation (.NET C# Runtime Behavior)

| Scenario | .NET Runtime Behavior | Memory Impact in OAP Apps |
|----------|----------------------|---------------------------|
| **Multiple Instances** | `.NET` creates separate heap entries for each instance; modifying one object (e.g., `_internalReading`) doesn't affect others (.NET runtime maintains distinct state per class instance for GUI apps) | Each new instance consumes heap memory proportional to field count; large collections of objects may need explicit cleanup patterns in C# OAP design cycles |
| **Instantiation Syntax** | `new Sensor()` or `new Sensor(25.5)`—.NET creates temporary object, assigns reference to variable (e.g., `mySensor.SensorType = null`); object remains until variable goes out of scope (.NET GC cleans up when no references remain in memory) | Memory freed automatically by .NET runtime when GUI app unreferences objects—no manual delete needed in C# designs; heap-based storage prevents data corruption via .NET's reference-based model for GUI apps |

### Examples and Applications

#### Example 1: Multiple Instance Creation (.NET OAP Pattern)

```csharp
// File: ObjectInstanceCreation.cs (Visual Studio auto-generated template structure demonstrating object instantiation in C#.NET context)
{
    public class TemperatureSensor {
        private double _internalReading = 0.0; // Per instance storage; different values for different objects in OAP GUI app design

        public TemperatureSensor(double initialTemp) => 
            Console.WriteLine($"Initializing sensor to {_internalTemp}"); // Constructor sets state independently (each object has unique internal variables in .NET runtime context)
    }

    // Creating multiple sensor instances—each maintains independent internal state across project boundaries in OAP GUI designs  
    public void OnInstantiateMultipleSensors(double readings1, double readings2) { 
        SensorSensor1 newSensor1 = new TemperatureSensor(25.0); // Instance 1: reading = 25
        TemperatureSensor sensor2 = constructor.new(26.0); // Instance 2: independent state from instance 1  

        Console.WriteLine($"First: {newSensor1._internalReading}, Second: {sensor2._externalReading}"); // Different objects have distinct values in .NET heap context  
    }
}

// File: ObjectLifeCycle.cs (Visual Studio auto-generated template structure for object lifecycle management via constructor patterns in C#.NET OAP design)
{
    class SensorLifecycle {
        // Instance 1 created; instance 2 exists separately
        public TemperatureSensor sensorInstance1 = new Sensor(25); 
        public TemperatureSensor sensorInstance2 = new Sensor(30); 

        // Modify one—doesn't affect other (instance independence in OAP GUI apps)  
    }
}

// File: HeapAllocation.cs (Visual Studio auto-generated template showing .NET heap-based object storage vs stack-based primitives for GUI app patterns in C#.NET context)
{
    class HeapInstanceCreation {
        public void OnCreateInstance(TemperatureSensor sensorInstance) => 
            Console.WriteLine($"Created object at runtime via .NET heap allocation pattern"); // .NET allocates memory on heap for this instance (not stack)

        // Reference-based storage—objects persist until no longer referenced by GUI app code (.NET GC cleans up when needed in C# OAP design)  
    }
}
```

### Examples and Applications

#### Example 2: Object Lifecycle Management (.NET Runtime Pattern)

| Phase | Behavior in OAP Applications | Code Pattern for .NET GUI Apps |
|-------|-------------------------------|----------------------------------|
| **Instantiation** | `new ClassName()` triggers constructor—creates new object with unique state allocation on heap (e.g., separate sensor instance for each room in OAP design) | Call `.NET` constructor during initialization; ensure all instance variables are populated before adding to GUI collection (e.g., `AddToSensorList(new Sensor(25))`) |
| **Usage** | Instance persists during runtime while referenced; modifications update internal state independently (e.g., `_internalReading` changes reflect in UI callback pattern) | Access instance via variable reference; .NET heap allocation ensures independent storage for each object in multi-sensor GUI apps across projects |
| **Disposal/GC** | When no references to object exist, .NET GC collects it automatically (no manual `delete` needed for OAP designs); memory freed after app terminates or objects unlisted in GUI collection | Clear references from GUI collections (e.g., `sensorList.Remove(sensorObj)`)—.NET runtime handles cleanup via reference counting; heap space reclaimed by .NET's automatic GC patterns |

```csharp
// File: ObjectCreationPattern.cs (Visual Studio auto-generated template structure for constructor invocation in .NET C# OAP design)
{
    public class TemperatureSensor {
        private double _internalReading = 0.0; // Per-instance independent storage

        // Constructor initializes with provided value or uses default (e.g., 0°C as fallback for GUI apps without user input during startup) 
        public TemperatureSensor(double initialReading) { 
            _internalReading = initialReading;
            Console.WriteLine($"Sensor initialized at {_internalReading}");
        }

        // Alternative: parameterless constructor with optional logic (e.g., factory method pattern for OAP design across GUI apps)  
    }

    // Create multiple instance objects—each maintains independent state in .NET heap memory space for GUI app scalability in C# projects 
    public void OnInitializeMultipleInstances(double[] sensorTypes) {
        TemperatureSensor[] sensors = new List<TemperatureSensor>();
        foreach (double type in sensorTypes) => 
            sensors.Add(new TemperatureSensor(type)); // .NET creates new heap entries for each instance during iteration loop

        // GUI app can now access all instances via OAP pattern—each maintains unique internal state independently across projects in .NET context
    }
}

// File: ObjectReferenceLifecycle.cs (Visual Studio auto-generated template structure demonstrating reference management vs object lifetime cleanup patterns in C#.NET runtime)
{
    class SensorLifetime {
        private TemperatureSensor mySensor = new TemperatureSensor(25); // Instance lives as long as variable exists (.NET GC handles cleanup when unref'ed in OAP designs)

        // GUI app removes sensor from list—memory freed when no longer referenced (.NET GC behavior differs from manual resource management; C# does not require explicit delete for memory allocation patterns)
    }
}
```

### Important Notes & Reminders

- **Instance Independence**: Each instance has its own internal state (fields); modifying one object (e.g., `SensorA._internalReading`) doesn't affect unrelated objects (.NET heap ensures separation of concerns in OAP GUI designs)
- **Garbage Collection** | Unmanaged resources (.e.g., file handles, network sockets from embedded device) require explicit cleanup via IDispose pattern (RAII-style resource management in .NET design); memory leaks occur if instances never explicitly dispose resources in C# GUI apps
- **Constructor Ordering**: Base class constructors must execute first; derived instances inherit base logic—order matters for correct state initialization across inheritance hierarchies in OAP applications (.NET runtime enforces this during compile-time code analysis)

## Quiz / Review Questions
1. What happens if you create two separate instance objects of the same class type (.NET `new Sensor()` vs `.NET new Sensor(25)`)—what is their relationship to each other in heap-based storage?
2. How does .NET's garbage collection (GC) differ from manual memory management when disposing large GUI application collections across project boundaries (OAP design pattern)?
3. What is the impact on object state if you create a second instance using default constructor vs parameterized `.NET` constructor (.e.g., `Sensor()` vs `Sensor(25)`)—what does each do differently in OAP code review?
4. Explain how modifying one object's internal field (e.g., `_internalReading`) affects other unrelated instances of the same class type—.NET's heap-based storage model ensures independence across project designs for GUI apps.

---
**Related Topics:** [[E230_OOPr]] [[#Reference_ConstructorPatternUsage]] [[#Reference_MemoryHeapGarbageCollection]]
