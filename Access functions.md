# Access Functions in C# for Embedded Applications

Access functions (also called **property getters** and **property setters**) provide controlled access to member variables, allowing you to expose values without directly exposing the underlying storage.

## What are Access Functions?

An access function is a method that operates on a specific variable:
- **Property Getters**: Return a value
- **Property Setters**: Assign/modify a value

Example usage in C#:
```csharp
public class TemperatureReading {
    // Raw storage – not accessible directly from outside
    private float _temperature = 25.0f;          // Internal storage
    
    // Access function for reading (getter property)
    public float Value {               // Called when you access .Value
        get {                             // Runs when getting the value
            return _temperature;
        }
    }
    
    // Access function for writing (setter property with validation)
    public float Value 
    {
        set {                              // Runs when setting the value
            validate(value);                 // Check before updating
            _temperature = value;          // Internal storage updated
        }
    }
}
```

## Syntax of Access Functions in C#

### Property with Getters and Setters

```csharp
public class SensorReading {
    private int rawValue = 0;     // Internal storage (private)
    
    // Read-only property (getter only, no setter)
    public int Value { get; }      // Only get, never set
    
    // Property with both getter and setter
    public float Temperature {        // Can read AND write
        get => _reading.value;       // Returns the raw value as float
        set {
            // Validation logic for embedded device
            if(value < 0 || value > 100) {
                Console.WriteLine("Value out of valid range");
            }
            _reading.value = value;   // Update internal storage
        }
    }
}
```

### Static Property (Class-Wide vs Instance-Wide)

```csharp
public class SensorReading {
    // Instance property - stores data for this single reading sensor object
    private float _value = 0f; 
    public float Value { 
        get => _value; 
        set { /* update internal storage */ } 
    }

    // Static property - shared by all instances of this class
    public static int EnabledCount = 0;              // Class-level counter
    
    // You don't create "new SensorReading.EnabledCount" in most cases
}
```

## When to Use Access Functions vs Direct Variable Access

| **Scenario** | **When to Use** |
|--------------|-----------------|
| **Need validation logic** | Use accessor functions (e.g., check if reading is valid) |
| **Want to read/write data** | Property getters are ideal for exposure, setters allow validation |
| **Don't need any control** | Direct variable access is fine, but may leak more than intended |
| **Need different return types** | Accessor functions let you convert raw internal values (e.g., raw bytes → human-readable) |

## Example: Sensor Reading Class Using Access Functions

```csharp
// Embedded system example – use accessor functions to safely expose sensor reading
public sealed class TemperatureSensor {
    private int _rawValue = 0;         // Raw A/D converter output (0-255 or 0-4095)
    
    // Public read-only property exposes the reading as degrees Celsius
    public float Value 
    {
        get => ToCelsius(this._rawValue);          // Convert raw value to °C
    }
    
    // Property with validation – prevents invalid writes
    public int RawValue {                    // User can set/get raw value
        get => _rawValue;
        set {                                 // Validate and store
            if (value < 0 || value > 4095) {
                Console.WriteLine("Invalid raw value");
            }
            else {
                _rawValue = value;             // Internal storage updated
            }
        }
    }
    
    private float ToCelsius(int raw) {         // Helper conversion method
        return (float)raw / 4096.0f - (float)0f;     // Convert to Celsius
    }
}
```

### How to Use Access Functions in Code

```csharp
// Creating an object – use properties to interact with it
TemperatureSensor sensor = new TemperatureSensor();

// Read the actual temperature value from hardware using accessor property
float currentTemp = sensor.Value;           // Calls getter, returns °C

// Can't directly change internal _rawValue – must update via setter
sensor.RawValue = 2048;                      // Valid raw value → sets internal storage
float newTemp = sensor.Value;                 // Read it back as °C

// You can NEVER set temperature through .Value property if you don't need to expose internally too
float t = sensor.Value;                       // Gets the current °C
```

Access functions help encapsulate internal data while exposing necessary functionality, which is critical for embedded C# apps where hardware state must be managed carefully.
