# Abstract Data Types in C# for Embedded Applications

An abstract data type (ADT) is a user-defined data structure that defines data only through its behavior, hiding the internal representation from users.

## What are Abstract Data Types?

An ADT specifies:
1. **Operations**: Methods you can call on this data type
2. **Behavior**: What those operations return or do
3. **NOT** How they work internally (implementation details)

Example ADTs in C# for Embedded Development:
- `List<T>` – stores and retrieves T items
- `Queue` – FIFO queue of items
- `Dictionary<TKey, TValue>` – key-value pairs lookup/storage

## Abstract vs Concrete Classes in C#

```csharp
// Abstract class - defines behavior but cannot be instantiated directly
abstract public class Device {
    // Define interface/methods without implementation
    protected abstract void Actuate();
    
    // Base implementation for children classes
    public virtual void Initialize() { /* Common setup code */ }
}

// Concrete subclass - provides full implementation
public sealed class Motor : Device {
    override void Actuate() { /* Motor-specific behavior */ }
    
    // Can instantiate directly: Motor motor = new Motor();
}

// Try to create abstract class directly (won't compile)
// AbstractDevice device = new AbstractDevice();  // ERROR!
```

## Why Use ADTs in C#

### Benefit 1: Separation of Concerns
Separate **interface** from **implementation**.

```csharp
// Interface/ADT definition - what clients should know
public class SensorManager {
    public void Read() { /* reads from sensor */ }
}

// Implementation details – internal only, client doesn't see
class TemperatureSensor : SensorManager {
    override void Read() {
        int reading = GetTemperatureFromHardware();
        this.value = reading;  // Internal storage - hidden detail
    }
}
```

## Benefits of ADTs for Embedded Applications

| **Advantage** | **Explanation** |
|---------------|-----------------|
| **Modularity** | Different implementations can replace each other without breaking client code |
| **Extensibility** | Add new device types without modifying shared interfaces |
| **Encapsulation** | Internal storage details (RAM, registers) are hidden from clients |
| **Consistency** | Same interface guarantees consistent access regardless of underlying type |

## Example: ADT for File Access

```csharp
// Abstract data type – what users expect
public class FileReader {
    // Open and close a file
    public void Open() { /* internal implementation */ }
    
    // Read characters/strings from the file
    public string ReadLine() { /* read next line as string */ }
    
    // Close the file and ensure it's not left open forever
    public void Close() { /* close underlying file handle */ }
}

// User code – only sees interface, not implementation details!
Reader reader = new FileReader("filename.txt");

reader.Open();
string line1 = reader.ReadLine();     // Read entire first line
string line2 = reader.ReadLine();     // Read second line
reader.Close();                       // Free up resources and close file

// The user does NOT know: whether it reads from hard drive, USB, or network!
```

Abstract Data Types in C# provide flexible interfaces that hide the complexity of internal implementations—perfect for embedded systems with diverse hardware configurations.
