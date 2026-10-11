# Class Templates in C# for Embedded Applications

A **class template** (also known as a generic class) is a blueprint for creating multiple different concrete classes (instances) that share the same structure and behavior but use different types.

## What are Class Templates?

Class templates allow you to:
- Define once, create many different instances/versions using any compatible data type (T, U, etc.)
- Use the same API/interface across all template instances
- Provide flexible, reusable code for embedded systems with variable hardware types
- Eliminate code duplication when implementing similar logic for multiple data types

## Why Use Class Templates?

| **Advantage** | **Explanation** |
|--------------|-----------------|
| **Code Reuse**: Implement once, use everywhere (e.g., Sensor and Motor share same read class template) |
| **Type Safety**: Built-in type checking at compile time |
| **Memory Efficiency**: Compile-time specialization generates code tailored to each instantiatation |
| **Reduced Boilerplate**: Write generic logic once instead of duplicating for different types |

## Example: Simple Class Template in C# for Embedded Systems

```csharp
// Create a class template that works with any data type T
template <typename T>        // Generic type T - used everywhere, no specific type required yet
class DataProcessor {
    private T _data;      // Stores data of type T (internal storage)
    
    public void Set(T value) {           // Helper function to set internal data (generic across all types)
        this._data = value;              // Assigns T-typed value internally
    }
    
    public T GetData() {                  // Returns stored value as T type
        return _data;                    // Internal data can be read and cast back if needed
        
        // Use in C# embedded contexts with generic types
        DataProcessor<int> intProc = new DataProcessor<int>();           // Create instance using int
        DataProcessor<float> floatProc = new DataProcessor<float>();      // Create instance using float
    }
    
    public void Process() {              // Common processing logic across all implementations
        DoWork();                 // Applies same algorithm regardless of data type (int, float, string, etc.)
    }
}

// How to Use Class Template in C# Embedded System:

// Create two instances with different types! No extra code needed!
DataProcessor<int> countProc = new DataProcessor<int>();          // Instance #1 using int type
DataProcessor<float> readingProc = new DataProcessor<float>();    // Instance #2 using float type
DataProcessor<string> stringProc = new DataProcessor<string>();   // Instance #3 using string type

// Use both instances with same interface! No code changes needed for each different type!
countProc.Set(10);                     // Set internal data to 10 (int)
readingProc.Set(50.7f);                // Set internal data to 50.7 (float)

stringProc.Set("Hello World");         // Set internal data to this string

int count = countProc.GetData();       // Read back the value! 
float reading = readingProc.GetData(); // Works with float too!
```

## Template vs Concrete Class: Example and Benefits

| **Scenario** | **Template Approach (One class, many instances) |
|--------------|--------------------------------------------------|
| Sensor reading across different data types | Single `DataProcessor<T>` class works for int (ADC value), float (Celsius conversion), string (ASCII output) |
| Motor speed vs. Voltage control | Same controller logic works with integer-based or floating-point-based motor speed values |
| Different embedded device types | Class template provides unified interface for controlling multiple hardware peripherals |

## Class Template Usage in C# Embedded Development

### Example 1: Generic List Implementation Across Types

```csharp
// Create a generic list-like structure that can hold any type of data
class LinkedList<T> {
    private LinkedListNode<T> _head;     // Internal pointer/reference to first node
    
    public void Add(T value) {   // Helper method – same interface across all types T!
        LinkedListNode<T> newNode = new LinkedListNode<T>(value);    // Create new node
        
        if (_head == null)               // Empty list?
            _head = newNode;            // Use new node as head
        else
            AppendToList(newNode);            // Link new data to end of list via reference
    }
    
    public T GetHead() {   // Access first element (any type T!)
        return _head != null ? _head.Value : default(T);  // Returns default if null
    }
}

// Using the generic list with different types!
LinkedList<int> sensorIDs = new LinkedList<int>();           // List of int IDs to track
LinkedList<string> deviceNames = new LinkedList<string>();    // List of strings (device names)
LinkedList<double> voltageReadings = new LinkedList<double>();  // List of double values

// All three lists work with same Add() and GetHead() methods!
sensorIDs.Add(10);         // Add integer ID 10 to first list
sensorIDs.GetHead();       // Return: 10 (int)

deviceNames.Add("TemperatureSensor");   // Add string "TemperatureSensor" to second list
deviceNames.GetHead();              // Returns: "TemperatureSensor" (string!)

voltageReadings.Add(3.5);           // Add double 3.5 to third list
voltageReadings.GetHead();          // Returns: 3.5 (double!)
```

### Example 2: Generic Sensor Data Processor Across Different Types

```csharp
// Single generic template that reads data from multiple types of sensors
class SensorReader<T> {
    public void Read() {                        // Helper function for reading data type T!
        int rawValue = GetRawADReading();      // Hardware-specific ADC value
        
        ConvertAndStore(rawValue);                // Apply conversion logic (same across all types)
    }

    private void ConvertAndStore(int raw) {                    // Generic processing logic
        this._rawValue = raw;               // Store in internal variable
    }
}

// Use template class with different data types
SensorReader<int> intReader = new SensorReader<int>();              // For integer sensor readings
SensorReader<float> floatReader = new SensorReader<float>();        // For float sensor data
```

## Best Practices for Class Templates in C# Embedded C Development

| **Practice** | **Why It Matters for Embedded Systems** |
|-------------|------------------------------------------|
| Keep interfaces consistent across all type instantiations | Use same APIs (method names, parameters) everywhere |
| Minimize template complexity | Overhead could affect performance on embedded devices |
| Use appropriate types (int vs float) | Match your hardware ADC/IO characteristics; avoid unnecessary conversion overhead |

Class templates (generic classes) in C# allow you to write once-use everywhere with multiple type variations, reducing memory usage and code duplication while maintaining flexibility.
