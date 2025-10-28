<div id="top" align="center">
<h1 align="center">⚡ 15W Digital Flyback Converter<br/>Fully Automated CCCV Power Supply with STM32 Control</h1>
</div>

<br />
<div align="center">
  <img src="images/V5.png?raw=true" alt="15W Flyback PSU Final Design" width="600" height="500">
  <p align="center">
    <strong>A sophisticated power electronics project combining digital control, embedded firmware, and precision PCB design</strong>
  </p>
</div>

---

## 📋 Project Overview

This project demonstrates the complete design and implementation of a **15W Constant Current / Constant Voltage (CCCV) Flyback Converter** with **full digital control via STM32L011 microcontroller**. The system demonstrates expertise in **power electronics, embedded systems, firmware development, and industrial automation**.

### 🎯 Core Challenge
Development of a production-grade power supply capable of:

- **Wide Input Range:** 230V AC compatibility (multi-national)
- **Dual Output Modes:** Automatic CC→CV switching for LED applications
- **Digital Control:** MCU-based regulation with ±2% accuracy
- **User Interface:** Computer software for real-time output configuration and monitoring
- **Industrial Features:** Relay feedback contact, 4-stage dimming, external control, comprehensive protection
- **Reliability:** Production-ready firmware with error handling and EMC compliance

### ✅ Solution Delivered
A complete power supply system consisting of:

- **STM32L011F4U3TR MCU:** ARM Cortex-M0+ with integrated ADC and PWM capabilities
- **Flyback Topology:** Galvanically isolated 230V AC to variable DC output
- **Digital Regulation:** PWM-based feedback via digital isolator
- **Communication:** Serial UART interface for computer control
- **Precise Measurement:** ADC measurements for voltage and current
- **KiCad PCB Design:** 6 iterative versions from prototype to production (V1-V6)
- **Comprehensive Testing:** EMC compliance (CISPR 32 Class A), efficiency measurements, thermal characterization

---

## 🛠️ Technical Architecture

### Hardware Stack
- **MCU:** STM32L011F4U3TR (ARM Cortex-M0+, 32KB Flash, 8KB RAM)
- **Power Topology:** Galvanically isolated Flyback Converter
- **Input Stage:** 230V AC rectification with EMI filter
- **Output Control:** PWM switching (MOSFET) with frequencies from 22-120kHz
- **Measurement:** 12-bit ADC (base resolution)
- **Communication:** UART interface
- **Feedback Elements:** Digital isolator (CA-IS3722HS), relay output for status indication

### Software Stack
| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Application** | C (STM32CubeIDE) | Digital control algorithm (PI/Cascade), state machine, command processing |
| **Driver** | LL-Driver (Low-Level) | Direct register access for GPIO, ADC, PWM, UART, DMA |
| **Control Algorithm** | PI / Cascaded Control Loop | Maintains stable CC/CV setpoints |
| **Memory** | EEPROM | Persistent configuration storage |
| **Monitoring** | MCU Tracer | Real-time debugging and performance metrics logging |
| **Communication Protocol** | Serial UART | Command interface for PC software integration |

### System Architecture Diagram
```
┌─────────────────────────────────────────────────────────────┐
│            PC Control Software (Serial Interface)            │
│  ┌────────────────────────────────────────────────────────┐ │
│  │  Configuration │ Real-Time Monitoring │ Logging        │ │
│  │  • Output V/I  │ • Voltage/Current    │ • Data Export  │ │
│  │  • Dimming     │ • Temperature        │ • Waveforms    │ │
│  │  • Limits      │ • Power Efficiency   │ • Events       │ │
│  └────────────────────────────────────────────────────────┘ │
└────────────────────┬────────────────────────────────────────┘
                     │ UART
        ┌────────────┴────────────┐
        │                         │
    ┌───▼──────────┐      ┌──────▼────────┐
    │  STM32L011   │      │  Power Stage  │
    │  MCU         │      │  & Sensing    │
    │              │      │               │
    │ • ADC Sampl. │      │ • PWM Driver  │
    │ • PI Control │      │ • MOSFET Gate │
    │ • PWM Gen.   │      │ • Voltage FB  │
    │ • UART Comm. │      │ • Current FB  │
    │ • Protection │      │ • Temp Sense  │
    └───┬──────────┴──────┬─────────────┘
        │                 │
    ┌───▼─────────────┬──▼──────────┐
    │                 │             │
┌──▼──┐  ┌────────┐ ┌▼────┐  ┌───▼──┐
│Relay│  │Dimming │ │Gate │  │Feedback│
│Out  │  │Input   │ │Drv  │  │Digital │
└─────┘  └────────┘ └─────┘  └ Isolator┘

230V AC Input → Rectification → Flyback Transformer
→ Secondary Output → Measurement → MCU Feedback → PWM Adjustment
```

---

## 🎓 Key Technical Achievements

### 🚀 **From Prototype to Production**
<div align="center">
  <table>
    <tr>
      <td align="center">
        <img src="images/3D_V1-P.png?raw=true" alt="First Prototype V1-P" width="800" height="600">
        <p><strong>V1-P: First Prototype</strong></p>
      </td>
      <td align="center">
        <img src="images/V5.png?raw=true" alt="Final Production V5" width="800" height="600">
        <p><strong>V5: Final Production</strong></p>
      </td>
    </tr>
  </table>
</div>

The evolution from initial concept to market-ready product, demonstrating continuous refinement through 6 design iterations.

---

### 1️⃣ **Digital Power Conversion with Precision Feedback**
<div align="center">
  <img src="images/15W.png?raw=true" alt="15W Flyback PSU" width="800" height="600">
</div>

**Challenge:** Maintain voltage/current stability across the entire load range.

- **Solution:** Cascaded/PI control loop with 16kHz (62.5µs) cycle time.
- **Innovation:** Software-based regulation enables dynamic adjustments and protection functions.

### 2️⃣ **Multi-Mode Power Supply with Automatic Switching**
<div align="center">
  <img src="images/15W-Side.png?raw=true" alt="15W Flyback Converter Side" width="800" height="600">
</div>

**Challenge:** Seamless CC/CV operation for diverse loads (LEDs, laboratory applications).

**Constant Current Mode (CC):**
- Fixed current output (programmable 0.1A - 1.2A)
- Automatic voltage limiting
- Ideal for LED strings

**Constant Voltage Mode (CV):**
- Fixed voltage output (programmable 10V - 60V)
- Current limiting for protection
- Standard laboratory power supply functionality

**Technical Implementation:**
- Software regulation automatically selects the most restrictive controller (voltage or current).
- Seamless transition without overshoot.

### 3️⃣ **Comprehensive Hardware Integration & Protection**
<div align="center">
  <img src="images/V5.png?raw=true" alt="Final PCB Design V5" width="800" height="600">
</div>

**Challenge:** Integration of analog control, digital MCU, high-voltage power stage, and protection circuits.

**Solution:** Integrated multi-layer PCB design with:
- **Isolated Feedback:** PWM transmission via digital isolator (CA-IS3722HS) for safe control.
- **Measurement Acquisition:** Voltage and current measurement via shunt and differential amplifier.
- **Relay Feedback:** Status output for relay contact.
- **Dimming Input:** 4-stage external dimming.

### 4️⃣ **Robust Firmware Architecture for Production Readiness**
<div align="center">
  <img src="images/reg.png?raw=true" alt="Regulation System" width="700" height="450">
</div>

**Challenge:** Creation of reliable, maintainable firmware for embedded power control.

**Solution:** Structured C codebase with:
- **State Machine:** Manages boot, regulation, fault detection, and shutdown.
- **Safety Features:** Overvoltage (OVP) and overcurrent protection (OCP), brownout detection, and watchdog.
- **Monitoring System:** "MCU Tracer" logs performance metrics for debugging and validation.

### 5️⃣ **PCB Evolution & Design Iteration**

**Six Production Iterations:**

| Version | Focus | Status |
|---------|-------|--------|
| **V1-P** | IC voltage supply prototype | ✅ Learning phase |
| **V1** | First Flyback LED converter | ✅ Validated |
| **V2-P** | Enhanced design iteration | ✅ Refined |
| **V3-P** | Further optimization | ✅ Tested |
| **V4-Release** | Production candidate | ✅ Manufacturing ready |
| **V5** | **Final Production** | ✅ **Active** |
| **V6** | Next-generation planning | ✅ **In Production** |

**Design Improvements:**
- Thermal management optimization (V1→V5)
- PCB layout for EMC compliance
- Component placement for manufacturing efficiency
- High-voltage isolation routing

---

## 📊 Project Specifications

| Category | Details |
|----------|---------|
| **Input Voltage** | 230V AC, RMS |
| **Output Power** | 15W |
| **Output Modes** | Constant Current (0.1A - 1.2A) / Constant Voltage (10V - 60V) |
| **Accuracy** | ±2% (design target) |
| **Isolation** | Galvanic isolation via Flyback transformer |
| **Communication** | Serial UART |
| **MCU** | STM32L011F4U3TR |
| **ADC Resolution** | 12-bit base, 14-bit with oversampling |
| **PWM Frequency** | 22kHz - 120kHz (depending on load) |
| **Protection Features** | OVP, OCP, OTP, UVP, short-circuit protection, no-load protection |
| **Relay Output** | Status contact |
| **Dimming Control** | 4-stage via external contacts |
| **Efficiency** | > 80% (typical) |
| **Development Time** | Bachelor thesis |
| **Team Size** | Individual contributor (Anselm Scherr) |

---

## 🔧 Technical Implementation Highlights

**Real-Time Digital Control**
- Control cycle at 16kHz (62.5µs cycle time)
- DMA-based data transfer from ADC
- PWM resolution optimized via Farey sequence
- Multi-mode operation with automatic CC/CV transition

**Precision Measurement & Feedback**
- Current measurement via shunt resistor and differential amplifier
- Voltage measurement via voltage divider and differential amplifier
- ADC calibration and offset correction in firmware
- Thermal management

**Embedded Communication Protocol**
- ASCII-based UART commands
- Real-time telemetry streaming (voltage, current)
- Error reporting

**Power Electronics Design**
- Storage transformer dimensioning (370 µH)
- MOSFET selection (OSG80R1K4DF) and snubber design
- EMC compliance (CISPR 32) via EMI filtering
- Longevity through elimination of electrolytic capacitors

**Why This Matters:** The system demonstrates understanding of complete power supply design—from AC mains to regulated DC output—combining digital control with analog power electronics.

---

## 📈 Simulation & Analysis

### Comprehensive Design Validation

**SPICE Simulation (LTspice):**
- Flyback converter operation modeling
- Transient response analysis (load steps)
- Efficiency calculations

**Power Flow Analysis (Plecs):**
- System-level power distribution modeling
- Harmonic analysis for EMC prediction
- Thermal loss estimation

**Results:**
- ✅ Output current ripple below 133mApp
- ✅ Transient settling within design specification
- ✅ EMC compliance validated

---

## 📊 Measurement Results & Characterization

### Performance Validation

```
┌──────────────────────────────────────────────────────┐
│     15W Flyback Converter Performance Data           │
├──────────────────────────────────────────────────────┤
│ Constant Current Accuracy   │ ±1.8% @ 1.2A setpoint│
│ Constant Voltage Accuracy   │ ±2.1% @ 48V setpoint │
│ Load Transient Response     │ 45ms (design target)  │
│ Output Voltage Ripple       │ 85mV peak @ 1.2A CC  │
│ Output Current Ripple       │ < 133mA peak @ 24V   │
│ Full-Load Efficiency        │ 82.5% @ 15W (target) │
│ Thermal Steady-State (25°C) │ +22.9°C (MOSFET @ 47.7°C) │
│ Protection Response Time    │ < 2ms (software)     │
│ UART Command Latency        │ < 10ms (design target) │
└──────────────────────────────────────────────────────┘
```

### EMC Testing (Electromagnetic Compatibility)

- ✅ CISPR 32 Class A (conducted emissions)
- ✅ EN 55015 Radiated Emissions (below limits)
- ✅ EN 61000-4-2 ESD Immunity (±8kV contact)
- ✅ EN 61000-4-4 Burst Immunity (2kV)
- ✅ EN 61000-6-2 Industrial Immunity

---

## 🛠️ Created With

* **[KiCad](https://www.kicad.org/)** - PCB design and schematic capture (all 6 iterations)
* **[STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html)** - Embedded firmware development
* **[LTspice](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html)** - Power electronics simulation
* **[Plecs](https://www.plexim.com/de/products/plecs)** - Energy system modeling
* **[STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html)** - MCU peripheral configuration
* **[J-Link](https://www.segger.com/products/debug-probes/j-link/)** - SWD debugger for firmware upload & debugging

---

## 🚀 Key Learning Outcomes

This project demonstrates comprehensive competencies in:

| Competency | Implementation |
|---|---|
| **Power Electronics Design** | Flyback topology, transformer dimensioning, MOSFET selection, thermal analysis |
| **Digital Control Systems** | PI/cascaded control loops, ADC sampling, PWM modulation |
| **Embedded Firmware** | STM32 LL drivers, interrupt handling, UART communication, DMA |
| **PCB Design & Manufacturing** | KiCad schematic & layout, layer stackup, EMC-compliant routing, 6+ design iterations |
| **Testing & Validation** | EMC compliance (CISPR 32), efficiency measurement, thermal characterization |
| **System Integration** | Combination of analog power, digital control, and communication |
| **Problem Solving** | Iterative refinement, simulation-driven design, experimental validation |

---

## 🎯 Why This Project Stands Out

1. **Complete System Design:** Not just firmware or just hardware—full integration from AC mains to regulated DC output.
2. **Production-Grade Quality:** 6+ design iterations demonstrate mature engineering approach.
3. **Real-World Complexity:** Mastery of galvanically isolated power conversion with digital feedback.
4. **Comprehensive Validation:** Simulation, measurement, and EMC testing all documented.
5. **Scalability:** Architecture supports future enhancements.
6. **Documentation:** Mathematical models, technical datasheets, and detailed measurements included.

---

## 💡 Technical Insights & Design Decisions

### Challenge 1: Stability in Flyback Converter Operation
- **Problem:** Flyback converters tend to exhibit ripple and load-dependent variations.
- **Solution:** Tight digital PI control loop and careful hardware design (snubber).
- **Learning:** Digital control can effectively compensate for analog non-idealities.

### Challenge 2: PCB Layout for High-Voltage Isolation & EMC
- **Problem:** AC mains and isolated secondary side require careful routing.
- **Solution:** Proper creepage/clearance, separate ground planes, EMI filtering.
- **Learning:** EMC compliance must be designed in from the start.

### Challenge 3: Firmware Reliability in a Power Supply
- **Problem:** Watchdog timeouts or firmware crashes could damage the load.
- **Solution:** Redundant protection mechanisms (hardware OCP/OVP + software OVP/UVP), safe-state defaults.
- **Learning:** Mission-critical embedded systems require defensive programming.

### Challenge 4: Thermal Management at 15W in Compact Package
- **Problem:** Limited PCB area with high power dissipation.
- **Solution:** Thermal measurements, optimal placement of power components (MOSFET, diode).
- **Learning:** Thermal design is integral to electrical design (hottest spot 47.7°C).

---

## 📞 Project Contact

For questions about the architecture, implementation details, or technical decisions:

- **Dr. Michael Heidinger** - michael.heidinger@digitalpowersystems.eu
- **Anselm Scherr** - anselm.scherr@digitalpowersystems.eu

---

## 📄 Additional Resources

- **Product Datasheet:** `Datasheet/DIG-CCCV-15W_datasheet.pdf` - Official technical specifications and operating guidelines
- **Bachelor Thesis PDF:** `Bachelor_thesis/BA_Anselm_Scherr.pdf` - Complete technical documentation including:
  - Detailed design methodology and derivations
  - Comprehensive measurement results and characterization
  - Simulation analysis and validation
  - PCB layout and manufacturing considerations
  - Firmware architecture and control algorithms
  - EMC testing and compliance documentation

---

<div align="center">
  <strong>Engineered with precision. Tested for reliability. Built to production standards.</strong>
  
  <br/><br/>
  
  <a href="#top">↑ Back to Top</a>
</div>
