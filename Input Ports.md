# Input Ports in C# for Embedded Applications

An input port allows an application to read values from physical hardware that changes over time (e.g., sensor data, switch states).

## What is an Input Port?

Input ports are part of embedded peripheral devices. They allow your code to "listen" to signals coming from the outside world:
- **Sensor Value**: Temperature, pressure, light level readings
- **Switch State**: User input (e.g., turning on a motor)
- **Communication Signal**: Data received over UART, I2C connections

## Hardware Interaction Example

```csharp
// Create an input port for reading temperature sensor data
InputPort<TemperatureSensor> port = new TemperatureSensor();

// Enable the input port to start reading
port.EnableInput();

// Read a value from the input port
int ambientTemp = port.Read();     // Returns the reading in milliseconds or as integer
float tempCelsius = (float)ambientTemp / 4096.0f; // Convert milliseconds to Celsius

// Check if reading is complete
bool hasData = port.HasData();

// Request a new read from hardware
port.RequestRead();
```

## Types of Input Ports in C# Embedded Development

| **Type** | **Example** | **Use Case** |
|----------|-------------|--------------|
| Temperature Sensor | Analog-to-digital converter reading | Reading temperature values |
| Motion Sensor | Accelerometer/Gyroscopes | Detecting movement or tilt |
| Light Sensor | Photodiode, LDR | Measuring light intensity |
| Digital Input | GPIO pin (high = 1, low = 0) | Button/state detection |
| UART Input | Serial port | Reading text data from keyboard/serial device |

## Key Methods for Input Ports

```csharp
// Check if input is ready without taking it out of the pipeline immediately
bool Port.IsReady(T value) {
    if (Port.HasData()) {
        return true;  // Read will succeed, wait
    }
    else {
        return false; // No data available yet, wait
    }
}

// Read from input port without processing
int Port.Read() {
    // Read data into value and store it in memory
    value = ...
    
    // Return the read result (or empty if none)
    if (!hasValue) {
        return -1;  // No data available
    }
    else {
        return ...  // Data from input port
    }
}
```

C# embedded applications use Input Ports to create reusable, well-structured input handling.
