# 6.9.RelationshipsBetweenClasses

## Overview  
Class relationships in .NET C# define structural interactions between classes in object-oriented designs—inheritance, composition, aggregation patterns are foundational to building scalable GUI applications and embedded device frameworks that require complex state management across projects.

### Key Definitions  
| Term | Definition |
|------|------------|
| **Inheritance (Is-a)** | Class derived from base class; shares code, adds specialization (e.g., `Window` extends `Control` in .NET GUI frameworks) |
| **Composition (Has-a)** | A class contains references to other independent classes; object lifecycle managed by container |
| **Aggregation (Uses-a)** | Similar to composition but more flexible—container may outlive contained objects |

### Core Concepts  
1.  **Inheritance Hierarchy**: Base class defines shared interface/behavior; derived class adds functionality without code duplication in OOP GUI apps  
2.  **Object Identity Across Classes**: Subclasses maintain independent state even inheriting base behavior—critical for GUI applications with dynamic component creation  
3.  **Abstraction & Interface Compliance**: Base classes may be abstract; derived instances must implement contract in .NET C# compile-time validation  

### Main Content  

#### Relationship Types (.NET OAP Pattern)

```csharp
// File: ClassRelationships.cs (Visual Studio template showing inheritance and composition patterns in .NET GUI frameworks)
abstract public class SensorComponent { 
    // Abstract base—enforces contract in derived classes for OOP GUI design
    public virtual void ReadData() => Console.WriteLine("Sensor reading acquired"); 
    
    protected string _type = "Generic";
}

// Inheritance example: TemperatureSensor extends SensorComponent (.NET OAP framework)
public class TemperatureSensor : SensorComponent { 
    private double _internalTemp = 0.0; // Independent state from base class
    
    public override void ReadData() => Console.WriteLine($"Temperature reading: {_internalTemp}°C");
}

// Composition example: MonitorWindow contains SensorComponent instances (.NET GUI pattern)
public class MonitorWindow : Form { 
    private readonly List<SensorComponent> _sensors = new(); // Composition—window has sensors as property
    
    public void SetupMonitors() { 
        AddSensor(new TemperatureSensor(25.0)); // Window manages sensor lifecycle via composition
    }

    public void OnSensorAdded(SensorComponent sensor) { 
        _sensors.Add(sensor); // MonitorWindow owns reference to SensorComponent—disposes when needed in OAP GUI apps  
    }
}
```

#### Relationship Comparison Table  

| Pattern | Syntax | Key Property | .NET OAP GUI Usage |
|---------|--------|--------------|---------------------|
| **Inheritance** | `class Derived : Base` | Single inheritance (mostly) | Reuse sensor data access patterns across device types in OOP frameworks |
| **Composition** | Class contains reference to other class | Strong coupling—object lives with container | `MonitorWindow` manages its `SensorComponent` instances throughout GUI app lifecycle |
| **Aggregation** | Reference via property; weak ownership | Container may live independently of contained objects | External sensor data can be injected into OAP design without full object relationship |

### Examples and Applications  

#### Example 1: Embedded Device Interface Pattern (.NET C#)  

```csharp
public interface ISensorProtocol { // Abstract contract in .NET runtime for GUI integration
    int GetValue();
    void SetTarget(int newValue);
}

// Inheritance hierarchy—different sensor types implement same protocol
public class AnalogSensor : SensorComponent, ISensorProtocol { 
    private double _lastReading = 0.0;
    
    public int GetValue() => (int)_lastReading * 100; // Protocol method call on derived object
    
    public void SetTarget(int target) { 
        // Override base behavior—custom implementation in OAP GUI frameworks  
        _lastReading = target / 100.0;
    }
}

// Composition pattern—MonitorWindow delegates protocol handling to sensor instances
public class ControlPanel : Form {
    private ISensorProtocol _sensor = null; // Interface-based dependency in .NET OAP design
    
    public void UpdateReadings() => 
        _sensor?.GetValue(); // Polymorphic call via interface in GUI event handler
}
```

### Quiz / Review Questions  

1. When using inheritance vs composition in embedded device applications—what are the tradeoffs for memory management in .NET runtime?  
2. How does abstract base class usage enforce interface compliance across all derived sensor types in OAP GUI frameworks?  
3. Can one class inherit from multiple classes (.NET multiple inheritance)? If not, what pattern achieves similar benefit?  
4. Why is composition preferred for managing independent embedded device instances in .NET C# GUI applications versus using inheritance?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_FriendClasses]] [[E230_OOPr_6.7_ClassTemplates.md]] [[E230_OOPr_6.4_ObjectsAsInstancesOfClasses.md]]


