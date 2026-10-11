# 4.2.OutputPorts

## Overview
Output ports in embedded OOP programs allow the system to send electrical signals (digital or analog) to external devices like LEDs, motors, displays, and sensors. These complement input ports by completing bidirectional communication circuits—essential for creating responsive OOP systems that control hardware behavior based on internal state decisions.

### Key Definitions
| Term | Definition |
|------|------------|
| **Output Port** | Hardware interface (e.g., GPIO pin) that allows an embedded system to transmit electrical signals to external devices |
| **Digital Output Signal** | Binary signal levels sent to control actuators like LEDs or motors in embedded OOP applications |
| **Analog Control Value** | Continuous voltage output values for PWM/motor speed control or dimming applications |

### Core Concepts
1. **Actuator Control**: Output ports enable driving devices (LEDs, relays, solenoids) via digital signals; analog outputs support fine-grained device control
2. **Output vs Input State Synchronization**: OOP programs must ensure consistent state tracking between input and output port operations to maintain accurate hardware system behavior
3. **Power Considerations**: High-power devices (motors, high-brightness LEDs) require voltage isolation from sensitive internal processing circuits

### Main Content

#### Output Port Implementation Patterns (.NET Embedded OOP Context)

```csharp
// Visual Studio generated code for embedded output ports in .NET context
{
    // DigitalOutPort enables sending HIGH/LOW signals to external devices via GPIO pin  
    public class DigitalOutputPort {
        // Instance variable stores output signal state (HIGH or LOW) 
        public int _signalValue = 0; 
        
        // Method sets output signal by writing to hardware-controlled pin register  
        public void OnWriteSignal(int signalHigh, bool forceState = false) { 
            Hardware.WritePin(signalHigh);
            Console.WriteLine($"Output signal set to {(forceState ? "FORCE" : null)}");
        }

        // Returns current output state for monitoring/debugging purposes  
        public bool IsHigh() => _signalValue == 1; 
    }

    // Combined OOP pattern combining input and output port management for device control
}
```

#### Output Port Hardware Interfaces in Embedded Systems (.NET Pattern)

| Interface Type | Typical Use Case | Hardware Signal Level (VCC) | Example Device |
|----------------|-----------------|-------------------------------|----------------|
| **Low Voltage Toggle** | Digital LED/Motor ON-OFF switching | LOW → HIGH signal transition | 5V pin, LED control |
| **PWM Frequency Control** | Motor speed dimming/adjustment | Duty cycle changes (0-100% duty) | PWM output, motor driver |
| **Analog Voltage Output** | Sensor feedback control | Continuous voltage range | DAC, analog sensor drive |

### Examples and Applications

#### Example 1: Digital LED Control Pattern via OOP Output Port (.NET Embedded C# Code)

```csharp
// File: EmbeddedOOP_OutputPorts.cs (Visual Studio auto-generated template for .NET embedded output control)
public class PWMOutputPort {
    // Class pattern enabling duty cycle-based control via OOP methods  
    private int _dutyCycle = 50; // 50% by default (middle value) in .NET runtime
    
    // Method sets new target duty cycle with internal hardware write logic  
    public void SetDutyCycle(int newVal, bool immediate = true) { 
        _dutyCycle = newVal; 
        
        // OOP method that internally calls hardware function for signal generation
        Hardware.WritePWM(newVal > 50 ? 1 : 0);
    }

    // Event handler triggered when duty cycle changes occur automatically  
    public event EventHandler<DutyChangeEvent> DutyChangeOccurred = null; 
}
```

#### Example 2: PWM vs Analog Output Patterns (.NET Embedded Design Patterns)

| Pattern | Use Case | Signal Behavior | Typical Hardware |
|---------|----------|----------------|------------------|
| **Digital Toggle** | LED ON/OFF control (binary state switching) | HIGH → LOW transitions only | GPIO pin (5V, 3.3V logic level) |
| **PWM Control** | Motor dimming/brushless motor speed adjustment | Duty cycle percentage from 0% to 100% range | Timer-based PWM hardware controller |
| **Analog DAC Output** | Fine-grained control of voltage for analog sensors | Continuous voltage value (e.g., 0-5V) | DAC module with buffered output |

```csharp
// File: OutputPortPatterns.cs (Visual Studio OOP development template structure for embedded output patterns)
{
    // Digital port pattern using simple ON/OFF toggling via hardware pin register  
    class DigitalOutputDemo {
        private int _pinState = LOW; // Initial state variable  

        public void WriteHigh(bool value) => SetPin(value);

        public bool ReadValue() => GetCurrentPinValue(); 
    }
    
    // PWM port pattern with duty cycle control for motor speed dimming  
    class PWMDemopattern {
        private int _outputDuty = 50;

        public void UpdatePwm(int newDutyCycle) { 
            _outputDuty = newDutyCycle / 10.0F; // Normalize to percentage range (0-99%)  
        }

        public bool IsHighNow() => _outputDuty > 50;
    }

    // Analog output pattern supporting continuous voltage control via DAC register writes  
}
```

#### Output Port Execution Flow Diagram (.NET Embedded Systems Context)

```
┌───────────────┐
│   Hardware    │     ← Signal input from device (e.g. sensor reading)
│  (LED/Motor)  │
└───────▲───────┘
        │
        ▼
┌───────────────────────────┐
│ Embedded System OOP       │
│   Output Port Object       │
└───────────────────────────┘
        │
        ▼
┌──────────────────┐    ┌──────────────────────┐
│ Signal Processing │ →  │ Send to Hardware (LED) │
│   (State Logic)   │    │ PWM register update    │
└──────────────────┘    └──────────────────────┘
```

### Examples and Applications

#### Example 3: Motor Control via Digital Output Port (.NET Embedded C# Implementation Pattern)

| Component | Code Pattern | Purpose in OOP Context |
|-----------|--------------|------------------------|
| **Class** | `MotorControlPort` object handles motor state transitions | Instance manages single motor via output signals |
| **Method** | `StartMotor()` → sets HIGH signal to drive | Triggers motor activation via hardware pin write |
| **Event** | `MotorStoppedEventHandler` for when signal returns LOW | Handles motor power-down automatically |

```csharp
// File: MotorControlOutputPort.cs (Visual Studio OOP pattern template structure for .NET motor control logic)
public class MotorControlOutputPort {
    // Output state variable tracks current motor drive status (on/off state)  
    private bool _motorPowered = false; 

    // Method activates motor by writing HIGH signal to GPIO output pin register  
    public void StartMotor() => OnHighSignal();

    // Callback function triggered when power returns to off state  
    private void OnLowSignal() {
        Console.WriteLine("Motor power OFF via digital output port (signal LOW)"); 
    }
}
```

### Important Notes & Reminders

- **Power Management**: For high-power devices, consider isolated power supplies that don't interfere with sensitive OOP processing circuits
- **Debouncing & Protection**: Motor controllers may require additional protection circuitry (flyback diodes) to prevent signal-induced damage when turning off motor coils
- **Signal Timing**: Output port transitions should maintain proper timing constraints per .NET embedded hardware specifications—violated timing can cause device misbehavior or unexpected state changes
- **Power Consumption Reduction**: Low-power idle states often require software signals that drive the output to a "sleep" mode rather than keeping devices permanently powered

## Quiz / Review Questions
1. What is the primary difference between PWM-based and digital toggle output port usage in embedded OOP applications?
2. Why might you need an analog output DAC for continuous sensor control versus using a simple digital GPIO pin?
3. How do high-power motor drives differ from LED signal outputs in terms of .NET output port implementation in an OOP context?
4. What is a common hardware protection circuit used when driving motors via embedded output ports to prevent voltage spikes?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_SignalProcessingHardware]] [[#Reference_PowerManagementEmbeddedSystem]]
