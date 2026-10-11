# 7.1.FM_Stereo

## Overview  
**FM Stereo Broadcasting**—multiplexes stereo audio onto standard FM broadcast carrier using pilot tone techniques—advanced RF protocol for OAP GUI frameworks supporting high-quality wireless data links across AM/FM bands in embedded audio systems.

### Key Definitions  
| Term | Definition |
|------|------------|
| **Pilot Signal**: 57kHz carrier frequency component embedded in baseband message signal—synchronization reference for embedded stereo decoder circuits |
| **Pre-emphasis Filter**: High-frequency amplification (60dB/decade) across RF channels to improve SNR before frequency modulation stage (OAP transmission design) |
| **De-emphasis filter**: 75Hz-5kHz attenuation bandpass equalizer per embedded receiver standard, inverses pre-emphasis to recover clean audio output |

### Core Concepts  
1.  **Stereo Multiplex Format**: FM stereo encodes two audio channels by modulating sidebands around pilot carrier (OAR protocol standard: M = L-R signal) |
2.  **De-muxing Technique**: Embedded receivers separate Left+Right sum channel from M-difference component—requires precise timing across RF communication protocols |
3.  **SNR Tradeoff**: Stereo increases bandwidth overhead (~40kHz vs ~180kHz mono per Carson's rule analysis) but preserves audio intelligibility in OAP embedded systems  

### Main Content  

#### FM Stereo Pilot Detection (.NET C# Implementation)

```csharp
// File: FM_Stereo.cs (Visual Studio auto-generated template for stereo decoder pilot extraction patterns)

public class FMStereoDecoder {
    private const double PilotFrequency = 57000.0;   // Standard 57kHz pilot carrier (OAR protocol standard)  
    private const double LeftChannelFreq = 82e6;       // L (Left) channel base: ~10kHz audio bandwidth per stereo design
    
    public void ExtractSumDifference(double L_Amp, double R_Amp) => {
        // Stereo signal: S = L + R, M = L - R, Pilot = PilotTone amplitude modulation
        var sumSignal = L_Amp + R_Amp;              // Sum channel for mono compatibility across OPR bands
        var diffSignal = Math.Abs(L_Amp - R_Amp);   // Difference signal for stereo (L-R) in embedded design
        
        Console.WriteLine($"Stereo multiplex components:");
        Console.WriteLine($"  [Sum] {sumSignal:F3} V — Compatible with monochrome OAP systems");
        Console.WriteLine($"  [Diff] {diffSignal:F3} V — Stereo channel (L-R) via pilot carrier");
    }

// Usage: Embedded OAR stereo decoder recovering dual-channel audio quality output across RF protocol bands  
var decoder = new FMStereoDecoder();
decoder.ExtractSumDifference(5.0, 3.0);  // Output shows stereo multiplex component separation  
```

#### Pre-Emphasis vs De-Emphasis (.NET Design Pattern)

| Stage | Frequency Response | OAP Embedded Design Implication |
|-------|---------------------|----------------------------------|
| **Pre-emphasis **(Transmitter) L+20dB/decade boost @ 15kHz (OAR protocol specification) | High-frequency SNR improvement for FM transmission across RF channels |
| **De-emphasis **(Receiver) -20dB/decade roll-off starting at 30Hz (standard OPR filter) | Cancels boosting—restores flat audio envelope but amplifies pre-eliminated floor noise |

### Example: Embedded Stereo Demodulation Circuit (.NET Implementation)

```csharp
public class StereoDMux_Circuit {
    // FM stereo demodulator circuit using pilot detection + sum/difference extraction patterns
    
    private const double PilotFreq = 57e3;           // 57kHz pilot carrier for OAR standard (OAP design constant)
    
    public void SimulateStereoDeMux() => {
        Console.WriteLine("[FM Stereo] Decoding components:");
        Console.WriteLine($"  [Component 1] 38kHz ± modulation signal from stereo encoding");
        Console.WriteLine($"  [Component 2] Pilot carrier detection at 57kHz—OAR decoder sync reference for embedded systems");
    }

// Usage: Stereo audio quality output for OAP GUI audio playback across FM protocols  
var stereoMux = new StereoDMux_Circuit();
stereoMux.SimulateStereoDeMux();  // Output shows stereo-decoding process results
```

### Important Notes & Reminders  
- **Standard Deviation Requirement**: ±75kHz modulation envelope per FM broadcast standard—embedded receiver design must filter noise above pilot tone frequency |
- **Timing Synchronization**: Stereo decode relies on precise timing across RF channels to separate L-M-R components from sum signal carrier output |

---
**Related Topics:** [[#Reference_FM_Stereo]] | [[E250_ACom_6.1.FM_ModulationIndex]] | [[#Reference_RF_Broadcasting]]
