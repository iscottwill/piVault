# 4.1.InputPorts

## Overview
Input ports in embedded OOP programs represent physical I/O interfaces that allow microcontrollers or devices to receive external data signals and convert them into internally accessible states. These are fundamental for interfacing with sensors, buttons, switches, and other peripheral hardware—critical when designing object-oriented systems that manage real-world device connections.

### Key Definitions
| Term | Definition |
|------|------------|
| **Input Port** | Hardware interface (e.g., GPIO pin) that receives electrical signals from external devices into an embedded system |
| **Digital Input Signal** | Binary signal levels (0V/5V or LOW/HIGH) representing boolean data from sensors/buttons |
| **Analog Reading** | Continuous voltage readings converted to discrete digital values for processing by OOP embedded software |

### Core Concepts
1. **Hardware Abstraction**: Input port handling abstracts low-level hardware details into high-level OOP methods for easier code management
2. **Polling vs Interrupt Model**: Embedded systems can use both polling (periodic reading) or interrupt-driven (event-triggered) input handling, each with trade-offs in latency and power consumption
3. **State Management**: Input port values maintain persistent state during object lifecycles; changes should be reflected immediately when hardware updates occur

### Main Content

#### Input Port Implementation Patterns (.NET Embedded OOP Context)

```csharp
// Visual Studio generated code for embedded input ports in .NET context
{
    // DigitalPort class manages single input port with interrupt handling patterns
    public class DigitalInputPort {
        public bool IsHigh() => ReadData() >= HighVoltageThreshold; // Polling check
        
        // Event-based handling using OOP callback mechanisms for hardware signals
        public event EventHandler<PortChangeEvent> InputChanged = null;
        
        // Method triggers input change notification when value flips state (HIGH/LOW)  
        private void OnInputChange(object sender, EventArgs e) => 
            Console.WriteLine($"Pin changed: {(IsHigh() ? "HIGH" : "LOW")}"); 
    }

    public class EmbeddedOOPInputPort {
        // Class-based input management with internal polling frequency configuration
        private volatile bool _currentState = false; 
        
        // Property allows external code to set/get input value without hardware exposure  
        public bool State { get => _currentState; set => ReadHardwarePin(); } 
    }

    // Input port state management using OOP principles (e.g., Polling model)
}
```

### Examples and Applications

#### Example 1: Digital Input Port Pattern with Interrupt Support (.NET Embedded C# Pattern)

| Component | Description | Code Pattern (.NET Context) |
|-----------|-------------|-----------------------------|
| **Class** | Represents single input port abstraction as object | `public class GPIOInputPort` |
| **Instance State** | Tracks current HIGH/LOW state at any time | `_state = true/false` field |
| **Event Handler** | Callback when hardware signal changes from one state to another | `EventHandler InputChanged` |

```csharp
// File: EmbeddedOOP_InputPorts.cs (Visual Studio auto-generated template structure for .NET OOP embedded systems)
public class DigitalInputPort {
    // Class-level input port management via instance variable tracking hardware state  
    private bool _portValue = false; 
    
    // Initialize port by reading initial hardware state into object internal state  
    public void OnInitialize(PinNumber pinIndex, int pullUpConfig = true) { 
        _portValue = Hardware.ReadPin(pinIndex); // Read from GPIO device into OOP object state
    }

    // Event handler triggers when input value changed (HIGH to LOW toggle detection)  
    private bool IsHigh() => _portValue == 1; 

    // Method returns true if port reads HIGH voltage level currently  
    public bool GetState() => _portValue == 1;
}
```

#### Example 2: Polling-Based vs Interrupt-Driven Input Handling (.NET Embedded Design Patterns)

| Pattern | Implementation Approach | Pros | Cons |
|---------|------------------------|------|------|
| **Polling** | Periodic hardware state reading in fixed intervals | More predictable latency control | Higher CPU usage due to repeated reads |
| **Interrupt-Driven** | Hardware triggers event when input changes; OOP handles callback | Low CPU usage, immediate response | Can cause jitter in time-critical applications |

### Examples and Applications

#### Example 2: Polling-Based vs Interrupt-Driven Input Handling (.NET Embedded Design Patterns)

```csharp
// File: InputPortPatterns.cs (Visual Studio auto-generated template structure for .NET embedded design patterns)
{
    // Polling Model - Periodic State Checking (OOP approach with fixed intervals)
    public class PollingInputPort {
        private int _pollInterval = 50; // ms
        
        private const int HIGH_THRESHOLD = 1000;
        private volatile bool _currentValue = false;

        // Polling reads hardware state repeatedly within application main loop  
        public void OnPollLoop() {
            ReadPinFromHardware(_currentValue); 
            if (_pollInterval > 0) return; 
        }
    }

    // Interrupt-Based Event Handler (OOP approach with callback triggers)
    public class InterruptInputPort {
        private int _triggerSource = null; 
        private int _interruptHandlerId = 1000; 

        // Hardware event fires immediately on state change via OOP pattern  
        public void OnHardwareTriggered() => ReadPinFromHardware();
        
        // Callback function triggered when interrupt occurs during execution  
        private void ProcessInterrupt(EventArgs e) => 
            Console.WriteLine($"Interrupt detected: {e.Message}"); 
    }

    // Polling vs Interrupt comparison example showing different latency patterns  
}
```

### Important Notes & Reminders

- **Power Efficiency**: Polling models consume more power (frequent reads); interrupt-driven handles reduce consumption when infrequently accessed devices are involved
- **Signal Debouncing**: Input ports require input signal debouncing to filter out noise-induced false-positive readings; hardware or software debounce implementations affect latency significantly
- **Pull-Up/Down Resistors**: Some ports need manual resistor configuration to stabilize HIGH/LOW signal levels—use OOP abstractions to encapsulate this configuration logic for maintainability
- **Thread-Safety Concerns**: When input ports are accessed from multiple threads, implement synchronization (lock, semaphore) to prevent state corruption or race conditions in OOP designs

## Quiz / Review Questions
1. What is the primary difference between polling-based and interrupt-driven input handling in embedded OOP systems?
2. Why might you choose software debounce over hardware debounce when handling high-velocity input port signals?
3. How does a pull-up resistor configuration differ from a pull-down resistor in .NET embedded input port implementations?
4. In what scenario would implementing a polling input port be more appropriate for an OOP application versus interrupt-based design?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_OutputPortConfigurations]] [[#Reference_SignalProcessingHardware]]
