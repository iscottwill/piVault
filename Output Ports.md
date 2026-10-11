# Output Ports in C# for Embedded Applications

An output port provides your application with a way to send commands and values back to hardware peripherals (e.g., motors, displays, LEDs).

## What is an Output Port?

Output ports write data or control signals that affect the physical state of embedded devices:
- **Control Command**: Write "start" or "stop" to a motor driver
- **Signal Level**: Set LED on/off or high/low voltage level
- **Display Data**: Send characters or pixels to an LCD/OLED display

## Hardware Interaction Example

```csharp
// Create an output port for controlling motors
OutputPort<MotorControl> port = new MotorControl();

// Enable the motor via hardware interface
port.EnableMotor(motorState);

// Check if output is enabled/active
bool isEnabled = port.IsEnabled();

// Write a value to control an output device
int port.Write(int pin, int value) {
    // Pin: Which port (GPIO number), Value: Digital value (0 or 1)
}
```

## Types of Output Ports in C# Embedded Development

| **Type** | **Example** | **Use Case** |
|----------|-------------|--------------|
| LED DisplayPort | GPIO pins for on/off control | Lighting, status indicators |
| Motor Control Port | Pulse width modulation (PWM) output | Steering motors |
| Serial Output | UART data to console/monitor | Logging, communication |
| LCD/OLED Port | Pixel values or ASCII characters | Displays |
| Speaker Output | Digital audio waveform | Audio feedback |

## Key Methods for Output Ports

```csharp
// Enable/disable an output device via hardware state
void Port.Enable(bool enabled) {
    // Set output GPIO pin to active/high value
}

// Check if the output is in a specified state/active
bool Port.IsEnabled() {
    // Return whether the output port is currently driving the output
}

// Write digital value (0 or 1) to an output device
int Port.Write(int pin, int value) {
    // Pin: Which GPIO number
    // value: Value to write (0=false, 1=true)
}

// Read current state of an output device
int Port.Read() {
    // Return the current output level
}
```

C# embedded development uses Output Ports to provide consistent interface patterns for controlling hardware peripherals.
