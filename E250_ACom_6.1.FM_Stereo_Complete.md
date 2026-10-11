# 6.1.FM_Stereo_Complete

## Overview  
**FM Stereo Broadcasting**—uses pilot tone and quadrature modulation to transmit two audio channels on standard AM carrier—critical embedded system feature for OAR GUI frameworks handling high-fidelity wireless data links across RF protocols.

### Key Definitions  
| Term | Definition |
|------|------------|
| **Stereo Multiplex Protocol**: S = L+R (Sum), I_L+R = 10-75kHz audio difference, π = 57kHz pilot carrier per OAR broadcast standard |
| **Pre-emphasis Filter**: Amplifies high-frequency components (60dB/decade) across RF channels to improve SNR before frequency modulation stage in embedded transmitters |
| **De-emphasis Filter**: Invesely attenuates message frequencies (75Hz-5kHz range)—standard OAR receiver design to restore flat audio response |

### Core Concepts  
1.  **Pilot Tone Synchronization**: Embedded receivers detect π signal at 57kHz standard for stereo de-multiplexing across all RF channels per broadcast protocol |
2.  **Bandwidth Tradeoff**: Stereo systems require wider channel allocation (~20-40kHz extra) vs mono (8.1MHz FM band)—OAR protocol mandates higher bandwidth for audio quality |
3.  **Capture Effect**: Stereo signal suppresses weaker adjacent carriers—advantageous for embedded receivers in noisy RF environments with multipath propagation |

### Main Content  

#### FM Stereo Signal Structure (.NET C# Pattern)

```csharp
// File: FM_Stereo_Complete.cs (Visual Studio auto-generated template showing stereo modulation patterns)

public class FMStereoProtocol {
    // Embedded OAR stereo broadcast system using standard multiplexing across FM channels
    
    private const double PilotCarrier = 57e3;    // 57kHz π carrier for standard OAR decoding  
    private const double SumChannelMax = 10e3;    // L+R baseband max: ~10kHz audio bandwidth per protocol
  
    public void SimulateStereoDecoding(double L_Channel, double R_Channel) => {
        var sumComponent = L_Channel + R_Channel;  // S = L+R (mono compatible output for OAP playback)
        var difference = Math.Abs(L_Channel - R_Channel); // I_L-R stereo component  
        
        Console.WriteLine($"[FM Stereo] Decoding:");
        Console.WriteLine($"  [L+R Sum]: {sumComponent} V — Compatible with mono OAR system playback");
        Console.WriteLine($"  [L-R Diff]: {difference} V — Stereo signal (embedded in I channel via modulation)");
    }

// Usage: Embedded stereo receiver recovering full-channel audio quality from FM broadcast across RF bands  
var steroDec = new FMStereoProtocol();
steroDec.SimulateStereoDecoding(5.0, 3.0);  // Output shows stereo-decoding process results
```

#### Pre/De-emphasis Implementation (.NET Design)

| Stage | Frequency Response (OAR Standard) | Embedded Impact |
|-------|-----------------------------------|-----------------|
| **Pre-emphasis **(Tx): +20dB/decade boost @ 15kHz across RF channels | Improves SNR on FM carrier before modulation—critical for high-quality audio output |
| **De-emphasis **(Rx): -20dB/decade roll-off starting at 30Hz | Cancels pre-boosting per OAR protocol spec but amplifies noise floor for embedded receiver design consideration |

### Example: Embedded Stereo Quality Output (.NET C# Pattern)

```csharp
public class Stereo_OAReceiver {
    // Audio output quality using FM stereo pilot tone extraction across RF channels
    
    private const double LeftChannelMax = 12.5e6;      // L (Left) channel baseband amplitude (OAR design standard)
    
    public void AnalyzeStereoQuality() => {
        Console.WriteLine("[FM Stereo Analysis]");
        Console.WriteLine($"[Component 1]: 38kHz ± modulation signal from stereo encoding (L+R, L-R separation per OAR spec)");
        Console.WriteLine($"[Component 2]: Pilot carrier detection at 57kHz—timing synchronization key for all embedded receivers");
    }

// Output should show: Stereo audio quality metrics across radio protocol bands  
```

### Important Notes & Reminders  
- **Standard Deviation Requirement**: -75kHz deviation minimum per broadcast standard—embedded receiver design must support stereo-compatible de-multiplexing |
- **Timing Synchronization**: FM stereo decode relies on precise timing for L-M-R component separation from sum signal carrier output |

---
**Related Topics:** [[#Reference_FM_Stereo]] | [[E250_ACom_8.3.CarsonRule_Complete]] | [[#Reference_RF_Broadcasting]] | [[#Reference_FM_Modulation]]
