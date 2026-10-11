# Analog-to-Digital (A/D) Converter in C# for Embedded Applications

A/B converters transform continuous voltage signals from sensors into digital values that computers can process. This is foundational for embedded systems using C#.

## What is an A/D Converter?

An ADC is a piece of hardware that converts continuous analog signals (like voltages from sensors) into discrete digital values (0 or 1, which your microcontroller reads as data):
- **Input**: Continuous voltage signal from physical world
- **Processing**: Hardware performs conversion internally (A → D = Analog-to-Digital)
- **Output**: Binary value (0, 1, ... etc.) stored in memory

## Example: Converting Sensor Data to Digital Values

```csharp
// Create an A/D converter for reading sensor values
ADConverter<TemperatureReading> port = new TemperatureReading();

// Enable ADC conversion
port.EnableConversion();

// Read a value from the A/D converter
int tempRead = port.Read();     // Returns integer reading in degrees C (e.g., 25)

// Or read as float with finer resolution
float tempHighRes = port.Read<float>();  // Higher precision (e.g., 25.06C)

// Convert the A/D reading to a readable unit
float valueMilliCelsius = tempRead / 100.0f;        // e.g., 25 * C/100 = 250mC = 0.250C

// Store result in memory
System.Diagnostics.Debug.Write(tempRead);            // Print to console/debug
```

## Types of ADCs and Their Uses

| **ADC Type** | **Resolution** | **Range** | **Use Case** |
|--------------|----------------|-----------|--------------|
| 8-bit | 256 levels (0-255) | ±1.2V or ±3.6V | General-purpose sensing |
| 10-bit | 1024 levels | ±5V | Higher precision sensors |
| 12-bit | 4096 levels | High/low range | Temperature, voltage, current |

## Key Methods for A/D Converters

```csharp
// Enable/dispatch an ADC conversion request
void Port.EnableConversion() {
    // Request the hardware to convert the next analog signal
}

// Read a value from A/D converter
int Port.Read() {
    // Return digital value in range [0, max] (where max = resolution - 1)
}

// Set voltage scale for ADC (calibrate sensor)
void Port.SetRange(float min, float max) {
    // Tell hardware to use this voltage range instead of default
}

// Convert raw A/D reading into a usable value
float Port.Convert(int rawValue) {
    return (rawValue - minimum)/maximum * scaleFactor + offset;
}
```

C# embedded developers use A/D converters to interface with real-world sensors, enabling applications like temperature monitoring and light detection in devices.
