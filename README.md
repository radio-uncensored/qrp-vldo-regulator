# M9OMS VLDO V2 — Very Low Dropout (VLDO) LDO Linear Regulator for QRP radios

The **M9OMS VLDO V2** is a discrete **very low dropout (VLDO)** linear voltage regulator for QRP radios. It delivers clean, RF-quiet power — selectable **9.0 V / 12.0 V / 13.8 V** at up to **2 A** — with strict voltage control, making it ideal for sensitive HF receivers.

---
<p align="center">
  <img src="images/DSC01726.JPG" alt="M9OMS VLDO V2 assembled board — 65 × 20.5 mm discrete very low dropout (VLDO) linear regulator for QRP radios such as the QRP Labs QMX" width="600">
</p>

---

## Design Rationale

### 1. The "12V" Problem
When this project began, the QRP Labs QMX had a strict **12.0 V maximum input**. Exceeding it risked damage, but the obvious power options all involved compromise.

### 2. Compromised Options
* **Buck / buck-boost converters:** Cheap switchers can create startup spikes, add RF noise, and in the worst case damage the transceiver. Even visually identical modules often differ by batch, source, or undocumented design changes.
* **USB-C PD triggers:** Still switching converters - the same spike and noise risks apply. Actual output can exceed 12.0 V depending on the source. PD supplies are better suited to steady charging loads - not rapidly changing SSB or CW demand.
* **Cheap marketplace modules:** Many hobbyist recommendations are low-cost modules that are hard to verify. Listings reuse photos, part numbers vary. Failure modes are rarely tested or documented.
* **Rectifier diode(s):** Safe and inexpensive, but lossy. Useful for simple protection. Inefficient across most of a battery discharge curve. Not battery-agnostic.
* **Partially-charged batteries:** Partially charging a 3s LiPo is more efficient than using diodes - but requires careful monitoring.

### 3. The Discrete LDO Path
Linear regulation is the cleanest route to an RF-quiet supply, but many LDO boards require too much headroom for a nominal 12 V battery. This project follows the evolution of a discrete topology. **One** device, ideal for field and shack:

1. **SPRAT Issue 201 (G4COL):** [Ian Braithwaite’s original schematic](https://www.gqrp.com/limiter.jpg) used a BJT long-tailed pair driving a P-channel MOSFET pass device: stable and well-behaved in simulations.
2. **The ND6T variant:** [ND6T published a variant](http://www.nd6t.com/qrp/VLDO.htm) to significantly reduce quiescent current - changes include Itail, voltage divider, Vref and PMOS. Simulations suggest it weakens PMOS gate control. Further testing revealed that a change to Vref led to oscillation (visible under load).
3. **M9OMS VLDO Prototype:** A 4-layer PCB implementation of G4COL's topology, miniaturised with targeted component upgrades. DC performance [shared by KC7XE on QRP Labs groups.io](https://groups.io/g/QRPLabs/message/158202).
4. **M9OMS VLDO V1.1:** Based on prototype - final changes include output selection ladder with trim, mounting holes and cable strain relief. 65 mm x 20.5 mm. Factory assembled. Baseline for V2.
5. **M9OMS VLDO V2:** A fresh design to reduce dropout, improve transient response, and in-dropout performance beyond V1.1 & modern monolithic LDOs. Same footprint. Clearance hole added for case mounting (for applications requiring higher dissipation). See [DC improvements vs V1.1](improvements.md).

---

## Technical Electrical Specifications

> ⚠️ **Specification Note:** Figures originate from LTspice simulations (PCB parasitics, ESR/ESL, TO-220 lead inductance) and are progressively being replaced with bench measurements. The **Basis** column flags which rows are now hardware-verified; the full DC measured dataset and test conditions are in [DC Bench Measurements](measurements.md).

| Parameter | Specification | Condition / Note | Basis |
| :--- | :--- | :--- | :--- |
| **Input Voltage Range** | 8.0 V to 18.0 V DC | Continuous operation | Measured |
| **Output Voltages** | **9.0 V / 12.0 V / 13.8 V** | Set by header pins; trimmed via `R7` | Measured |
| **Max Output Current** | 2.0 A | Continuous | Measured |
| **Dropout Voltage** | **< 100 mV** | At 1.0 A load | Measured |
| **Quiescent Current ($I_q$)** | 1.13 mA to 2.48 mA | Varies with $V_{IN}$ (8.0 V – 18.0 V) | Measured with LP2950. Initial V2 release will have a higher Iq.|
| **Load Regulation** | ~20 mV / ~40 mV | 0.1 A–1.0 A / 0.1 A–2.0 A | Measured |
| **Line Regulation** | < 5.0 mV | Across $V_{IN}$ = 8.0 V–18.0 V at $I_{LOAD} = 1.0\text{ A}$ | Measured |
| **Output Noise** | < 25 µV RMS | 20 Hz – 20 kHz | Simulation |
| **Transient Undershoot** | < 15 mV | 0.5 A $\rightarrow$ 2.0 A, 1 µs edge | Simulation |
| **Transient Overshoot** | < 15 mV | 2.0 A $\rightarrow$ 0.5 A, 1 µs edge | Simulation |
| **Load Transient Recovery** | < 5 µs / < 2 µs | To within $\pm 5\text{ mV}$ / $\pm 10\text{ mV}$ | Simulation |
| **Phase Margin** | ~48° | Clean phase transition, no ringing | Simulation |

> **Measured** rows are hardware-verified on a single V2 sample (DC + thermal, taken at the board terminals); measured dropout, line, and load regulation meet or beat the simulated figures. **Simulation** rows await the dynamic bench work below. Full values, plots, and conditions: [DC Bench Measurements](measurements.md).

---

## Key Architectural Improvements: V2 vs V1.1

### 1. Pass-FET Upgrade (`IRF9Z34N` $\rightarrow$ `AOTF4185`)
* Near dropout, pass-FET performance is set by transconductance at low $V_{GS}$, not just $R_{DS(on)}$.
* The `AOTF4185` delivers 2.0 A at lower gate drive than the `IRF9Z34N`, giving V2 a clear **headroom advantage** at full load.
* Its TO-220F package also provides an isolated tab for simpler heatsink mounting.

### 2. Active Gate Drive
* In V1.1, the LTP drove the pass-FET gate through a passive $10\text{ k}\Omega$ pull-up, slowing gate charge.
* V2 adds a complementary emitter-follower stage (`Q3`/`Q4`), cutting gate-drive impedance from about $10\text{ k}\Omega$ to the low tens of ohms and enabling microsecond-scale transient response.

### 3. Pole-Splitting Compensation
* V1.1 used a large $1\text{ }\mu\text{F}$ gate-to-output Miller capacitor, slowing the loop.
* V2 uses a smaller Miller capacitor (`C3`) plus a feed-forward capacitor (`Cff`) to add phase boost near crossover, reaching **60 kHz unity-gain bandwidth**.

### 4. Symmetrical LTP Collector Loading
* V1.1 loaded only one side of the differential pair, causing collector mismatch. Temperature-dependent offset not observed.
* V2 uses matched resistors (`R1` = `Rdu1`) to equalise operating points and reduce input-referred noise. Careful placement required.

### 5. Damped Output Network
* V1.1 had no output bulk capacitor or snubber - fast load changes could appear directly at the output.
* V2 adds a polymer bulk capacitor plus a damped ceramic snubber to improve transient energy delivery whilst suppressing HF ringing.

---

## Performance Summary: V2 vs V1.1

[V2 exceeds V1.1 on measured DC performance in or near dropout](improvements.md). Faster transient response in simulation. Loop bandwidth and PSRR are also expected to improve, pending bench verification.

* **Headroom:** V2 needs about 100 mV across 30 mA–1 A and about 200 mV at 2 A; V1.1 needs 250-500 mV.
* **DC stiffness:** V2 has a small intrinsic output-resistance advantage, though wiring resistance dominates in-regulation measurements.
* **Transient response (simulation):** V2 settles a 1.9 A load step within the source’s 10 µs slew time with minimal overshoot or undershoot. V1.1 takes 1.5–3 ms.
* **Line regulation:** Both stay well under 1 mV/V in regulation.
* **Minimum load:** Both show a small no-load offset of about 20–30 mV, which resolves at roughly 30 mA on the V2 board.

---

## Outstanding Bench Work

DC and thermal characterisation is complete — full output-vs-input sweeps (0–4 A, all three output settings) plus thermal data, measured by KC7XE: see [DC Bench Measurements](measurements.md).

The following dynamic measurements remain:
* **V1.1 transient correlation:** Scope verification against simulated Figure 3a with the same 0.1 A → 2 A pulse profile.
* **V2 transient correlation:** Scope verification against simulated Figure 3b under the same conditions.
* **Loop characterisation:** Measure V2 phase margin, unity-gain bandwidth, and gain margin to confirm the simulated ~50° PM / ~60 kHz UGB.

---

## Outstanding PCB work:

### 1. Replace Cin1 electrolytic capacitor with aluminium polymer capacitor
* Simulation based PSRR improves without detriment to stability. Bench confirmation required.

### 2. Re-route header pins
* Procurement of additional 2057-MSE-G-ND 1x3 shunts is challenging.
* Re-routing of header pins allows a single 1x2 shunt to be used. Layout & function remain the same as V1.1.

### 3. Temperature-dependent drift
* Both V1.1 and V2 exhibit drift. V2 more sensitive in stress-testing (14Vin, 9Vout, 3A).
* Normal operating parameters verified - 1.5W continuous for 45 minutes (no housing). No voltage excursion observed beyond settling temperature (<0.34%, reached after 5-10 minutes).
* Remote-mounting PMOS (10cm leads) exhibits similar behaviour, though lower (<0.17%). Thermal calculator to be added to documentation.
* Re-route traces to eliminate temperature gradient across the Q1/Q2 die - thermal transfer to Q2 currently dominates.

### 4. 633 Hz oscillation — excellent work by CR7BTQ:
* Prototype board exhibited oscillation under load (633Hz, 20-30 mV).
* Various experiments pointed to Vref - 10k loading resistor reduced amplitude by 70%, but frequency entered kHz range - not a viable solution.
* Vref may need some current sinking ability to feed LTP, plus LTP current draw may be too low for LP2950 stability.
* Alternate Vref installed - stability restored.
* V2 will ship with 78L05. A low Iq alternative requires testing for later revisions.
---

## Future Project

Hybrid board (SMPS + linear) - awaiting stable V2 release with verified PSRR measurements before prototyping.
