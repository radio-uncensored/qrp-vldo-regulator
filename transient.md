---
title: "Oscilloscope Measurements — M9OMS VLDO V2"
description: >-
  Oscilloscope measurements of the M9OMS VLDO V2 linear regulator at 13.8 V in:
  noise floor, reference, constant load, load steps, power-on and power-off.
---

# M9OMS VLDO V2 — Oscilloscope Measurements (Noise Floor, Load Steps, Power-On and Power-Off)

Oscilloscope captures of the M9OMS VLDO V2 - **NEW V2.1 board revision**, under a
**13.8 V input**, covering the measurement noise floor, the voltage reference,
output voltage at constant loads from **0 mA to 2 A**, transient response to load
steps between **0.1 A and 1.5 A**, and power-on and power-off ramps. This page
records the measurements behind the corresponding rows of the
[specification table](design.md#electrical-specifications). It supplements the
[DC and thermal bench measurements](measurements.md); loop characterisation
(phase margin, gain margin, unity-gain bandwidth), PSRR and broadband noise are
not addressed here.

> **Measurements by CR7BTQ** (August 2026), on a single V2.1 board.

**Product page:** [M9OMS VLDO V2 — RF-quiet power supply for QRP Labs QMX](index.md)

---

## Test setup and conditions

- **Board:** production-representative V2.1 board - 12 V or 9 V jumper setting.
- **Input:** 13.800 V DC, maintained at the PCB input pads by a four-terminal
  connection to the power supply, compensating for voltage drop in the
  supply leads. Current limit set to 5 A; supply is a Tenma 72-2540 (30 V / 5 A).
- **Load:** electronic load pulsing between 0.1 A and 1.5 A. The edge rate of the
  load transition was **not characterised**; settling figures are representative
  of this setup rather than a specification against a defined load slew rate.
- **Measurement point:** directly at the PCB output pads.
- **Oscilloscope:** Tektronix TDS 784D; sample rate and timebase are labelled on
  the individual captures.
- **Bandwidth limit:** 20 MHz, enabled for every capture on this page, to reject
  external noise picked up by the probes. See
  [Measurement noise floor](#1-measurement-noise-floor) below.
- **Probes:** Tektronix P6139A, 500 MHz bandwidth.
- **Channels:** Ch1 is the regulator output throughout, except where stated. For
  the power-on and power-off captures, Ch2 is the input.
- **Power switching:** power was applied and removed using the bench supply's
  output On/Off button, not by interrupting the supply leads.
- **Vertical scale and coupling:** the reference, constant-load and load-step
  captures are AC-coupled at 10.0 mV/div. The power-on and power-off captures are
  DC-coupled at 2.00 V/div on both channels.
- **Trigger:** set per capture rather than held constant. Ch1 falling edge at
  −5.6 mV for the ground-reference, reference and constant-load captures; Ch1
  falling edge at −3.0 mV for the load-application step; Ch1 rising edge at
  −18.2 mV for the load-release step; Ch2 rising edge at 480 mV for the 12 V
  power-on captures and at 8.00 V for the 9 V ones; Ch2 falling edge at 11.0 V
  for the power-off captures.
- **Acquisition:** the load-step captures are Sample-mode acquisitions (2 and 17
  acquisitions respectively); the reference, constant-load, power-on and
  power-off captures were taken in Hi Res mode. Times and voltages measured with
  on-screen cursors.

---

## 1. Measurement noise floor

Before measuring the regulator, the probe was measured against ground to
establish what the setup itself contributes. Everything later on this page is
read against this floor.

### TEK00027 — Ground reference, no bandwidth limit

![Ground reference with no bandwidth limit, showing broadband noise pickup](images/transient/TEK00027.png)

*Ground reference, no bandwidth limit. AC-coupled, 10.0 mV/div, 5.00 µs/div,
10.0 MS/s, Sample mode.*

Without a bandwidth limit the trace shows a continuous band of grass with
occasional narrow spikes — all of it picked up by the probes rather than
originating in the regulator. Part of it was traced to a magnifier lamp at the
bench; a component at around **80 MHz** was also present, most likely from
computers running in the same small room. The remainder was not identified.

### TEK00028 — Ground reference, 20 MHz bandwidth limit

![Ground reference with 20 MHz bandwidth limit, showing a substantially reduced noise band](images/transient/TEK00028.png)

*Ground reference, 20 MHz bandwidth limit. AC-coupled, 10.0 mV/div, 100 µs/div,
500 kS/s, Hi Res mode.*

With the 20 MHz bandwidth limit enabled the externally coupled content is largely
removed and the trace collapses to a thin band. **Every capture on this page was
taken with this limit enabled.**

The two captures are not a like-for-like comparison: they differ in timebase
(5.00 µs/div against 100 µs/div), sample rate (10.0 MS/s against 500 kS/s) and
acquisition mode (Sample against Hi Res). The reduction in visible noise between
them is therefore not attributable to the bandwidth limit alone.

---

## 2. Voltage reference

### TEK00029 — REF5050 output

![REF5050 reference output, flat at the measurement noise floor](images/transient/TEK00029.png)

*REF5050 reference output. AC-coupled, 10.0 mV/div, 100 µs/div, 500 kS/s,
Hi Res mode.*

The reference trace is indistinguishable from the ground-reference capture above:
no periodic content and no structure above the measurement floor at this
sensitivity. The REF5050 measures **4.995 V**; this capture is AC-coupled at
10.0 mV/div and so shows the noise on the reference rather than its absolute
value, and the 4.995 V figure is from a separate DC measurement.

---

## 3. Output voltage at constant load

Output voltage captured at six constant load currents from no load to 2 A.

### TEK00030 — 0 mA constant load

![Output voltage at 0 mA constant load](images/transient/TEK00030.png)

*Output voltage, 0 mA constant load. AC-coupled, 10.0 mV/div, 5.00 ms/div,
10.0 kS/s, Hi Res mode.*

### TEK00031 — 100 mA constant load

![Output voltage at 100 mA constant load](images/transient/TEK00031.png)

*Output voltage, 100 mA constant load. AC-coupled, 10.0 mV/div, 5.00 ms/div,
10.0 kS/s, Hi Res mode.*

### TEK00032 — 500 mA constant load

![Output voltage at 500 mA constant load](images/transient/TEK00032.png)

*Output voltage, 500 mA constant load. AC-coupled, 10.0 mV/div, 5.00 ms/div,
10.0 kS/s, Hi Res mode.*

### TEK00033 — 1 A constant load

![Output voltage at 1 A constant load](images/transient/TEK00033.png)

*Output voltage, 1 A constant load. AC-coupled, 10.0 mV/div, 5.00 ms/div,
10.0 kS/s, Hi Res mode.*

### TEK00034 — 1.5 A constant load

![Output voltage at 1.5 A constant load](images/transient/TEK00034.png)

*Output voltage, 1.5 A constant load. AC-coupled, 10.0 mV/div, 5.00 ms/div,
10.0 kS/s, Hi Res mode.*

### TEK00035 — 2 A constant load

![Output voltage at 2 A constant load](images/transient/TEK00035.png)

*Output voltage, 2 A constant load. AC-coupled, 10.0 mV/div, 5.00 ms/div,
10.0 kS/s, Hi Res mode.*

Across the full 20:1 load range, no trace departs meaningfully from the
measurement noise floor established in section 1, and there is no progressive
worsening as load increases. Each capture covers 50 ms, and none shows periodic
content, drift or any repeating disturbance.

What that does demonstrate is the absence of low-frequency instability: no
motorboating, no load-dependent oscillation, and no marginal behaviour appearing
at any point between no load and the 2 A rating. What it does **not** provide is
a ripple or noise figure. At 10.0 mV/div a 2 mV p-p artefact occupies a fifth of
a division, so these captures bound the answer rather than measure it — a proper
figure needs a dedicated low-noise measurement, which remains outstanding.

Any faint texture visible on the loaded traces is an artefact of the electronic
load rather than of the regulator. This was confirmed by repeating the
measurements with resistive loads, where the texture is absent; the electronic
load was necessary only for the load-step captures that follow.

---

## 4. Transient response

### TEK00036 — 0.1 A → 1.5 A, load applied

![Output transient, 0.1 A to 1.5 A load step: output falls 32 mV and reaches its final value in approximately 30 µs with no undershoot](images/transient/TEK00036.png)

*0.1 A → 1.5 A load step, 13.8 V in. AC-coupled, 10.0 mV/div, 10.0 µs/div,
5.00 MS/s. Cursors: 32.2 mV, 30.4 µs.*

When the load is applied, the output falls by **32 mV**, reaching its final value
in approximately **30 µs**. The falling edge is largely slew-limited — a straight
midsection rather than an exponential — which is the pass device being driven
hard by the gate-drive stage, then a soft knee onto the new level. There is no
excursion beyond the final value and no ringing.

### TEK00037 — 1.5 A → 0.1 A, load released

![Output transient, 1.5 A to 0.1 A load step: output rises 32 mV and reaches its final value in approximately 100 µs with no overshoot](images/transient/TEK00037.png)

*1.5 A → 0.1 A load step, 13.8 V in. AC-coupled, 10.0 mV/div, 20.0 µs/div,
2.50 MS/s. Cursors: 31.6 mV, 99.6 µs.*

When the load is released, the output rises by the same **32 mV**, reaching its
final value in approximately **100 µs**. The recovery is a clean first-order
approach with no overshoot.

**The two excursions agree to within 0.6 mV.** Both are the load-regulation
difference between the two operating points, not a transient glitch: the rail
moves to its new regulated level and stays there. The excursion corresponds to an
effective output impedance of roughly **23 mΩ** (32 mV across a 1.4 A change).

Settling is slower on release than on application, and the reason is inherent to
a series linear regulator: it can source current but cannot sink it. On release
the pass device is still conducting for 1.5 A while the load takes only 0.1 A, so
the surplus charge on the output capacitance can be removed only by the load
itself — at 100 mA, that is unavoidably slower than the load-application case,
where the loop simply drives the pass device harder. Of the two directions, the
load-application case is the more consequential in normal use, and it is the
faster of the two.

For context, both figures are three orders of magnitude shorter than a CW element
at 20 WPM.

---

## 5. Power-on, 12 V setting

Output (Ch1) and input (Ch2) captured as power is applied, at six constant load
currents.

### TEK00038 — 0 mA constant load

![Power-on ramp at 0 mA constant load](images/transient/TEK00038.png)

*Power-on, 0 mA constant load. DC-coupled, Ch1 and Ch2 2.00 V/div, 500 µs/div,
100 kS/s, Hi Res mode. Cursors: 11.80 V, 910 µs.*

### TEK00039 — 100 mA constant load

![Power-on ramp at 100 mA constant load](images/transient/TEK00039.png)

*Power-on, 100 mA constant load. DC-coupled, Ch1 and Ch2 2.00 V/div, 500 µs/div,
100 kS/s, Hi Res mode. Cursors: 11.84 V, 1.01 ms.*

### TEK00040 — 500 mA constant load

![Power-on ramp at 500 mA constant load](images/transient/TEK00040.png)

*Power-on, 500 mA constant load. DC-coupled, Ch1 and Ch2 2.00 V/div, 500 µs/div,
100 kS/s, Hi Res mode. Cursors: 11.84 V, 1.01 ms.*

### TEK00041 — 1 A constant load

![Power-on ramp at 1 A constant load](images/transient/TEK00041.png)

*Power-on, 1 A constant load. DC-coupled, Ch1 and Ch2 2.00 V/div, 500 µs/div,
100 kS/s, Hi Res mode. Cursors: 11.80 V, 1.24 ms.*

### TEK00042 — 1.5 A constant load

![Power-on ramp at 1.5 A constant load](images/transient/TEK00042.png)

*Power-on, 1.5 A constant load. DC-coupled, Ch1 and Ch2 2.00 V/div, 500 µs/div,
100 kS/s, Hi Res mode. Cursors: 11.80 V, 1.46 ms.*

### TEK00043 — 2 A constant load

![Power-on ramp at 2 A constant load](images/transient/TEK00043.png)

*Power-on, 2 A constant load. DC-coupled, Ch1 and Ch2 2.00 V/div, 500 µs/div,
100 kS/s, Hi Res mode. Cursors: 11.80 V, 1.72 ms.*

The output behaves identically at every load: flat at zero while the input ramps,
then a single steep, monotonic rise, then a soft knee onto the settled level.
**No overshoot at any load**, no steps, no retriggering and no disturbance on the
knee.

Two features of the input trace explain the rest. First, Ch2 shows a distinct dip
as Ch1 rises — the input sagging while the output capacitance charges — and the
dip deepens with load, from a barely visible notch at 0 mA to a pronounced sag at
2 A that takes the remainder of the frame to recover. Second, the input ramp
itself slows as load increases, which is why the cursor interval from trigger to
settled output grows from 910 µs to 1.72 ms across the series. Both are
properties of the bench supply feeding a capacitive load, not of the regulator;
see [Input ramp rate](#measurement-limitations) below.

At the two highest currents the output rise merges into the input ramp and the
traces run parallel for a time. That is the regulator still in dropout, tracking
the input up until it clears the setpoint — the same behaviour the DC sweeps
show, captured dynamically.

---

## 6. Power-off, 12 V setting

Output (Ch1) and input (Ch2) captured as power is removed, at five constant load
currents. No cursors were set on these captures, so the figures below are
qualitative.

### TEK00044 — 100 mA constant load

![Power-off ramp at 100 mA constant load](images/transient/TEK00044.png)

*Power-off, 100 mA constant load. DC-coupled, Ch1 and Ch2 2.00 V/div, 10.0 ms/div,
5.00 kS/s, Hi Res mode.*

### TEK00045 — 500 mA constant load

![Power-off ramp at 500 mA constant load](images/transient/TEK00045.png)

*Power-off, 500 mA constant load. DC-coupled, Ch1 and Ch2 2.00 V/div, 10.0 ms/div,
5.00 kS/s, Hi Res mode.*

### TEK00046 — 1 A constant load

![Power-off ramp at 1 A constant load](images/transient/TEK00046.png)

*Power-off, 1 A constant load. DC-coupled, Ch1 and Ch2 2.00 V/div, 10.0 ms/div,
5.00 kS/s, Hi Res mode.*

### TEK00047 — 1.5 A constant load

![Power-off ramp at 1.5 A constant load](images/transient/TEK00047.png)

*Power-off, 1.5 A constant load. DC-coupled, Ch1 and Ch2 2.00 V/div, 10.0 ms/div,
5.00 kS/s, Hi Res mode.*

### TEK00048 — 2 A constant load

![Power-off ramp at 2 A constant load](images/transient/TEK00048.png)

*Power-off, 2 A constant load. DC-coupled, Ch1 and Ch2 2.00 V/div, 10.0 ms/div,
5.00 kS/s, Hi Res mode.*

The output falls with the input in every case, riding just below it by the
dropout voltage until the input can no longer sustain the setpoint, at which
point the output falls away to zero. The collapse is clean at every current: no
oscillation, no ringing, no partial recovery.

The series differs only in timing, and systematically so. At 100 mA the decline
is gradual and occupies most of the 100 ms window; by 2 A the collapse arrives
shortly after the input is removed. This is the load discharging the supply's
reservoir at proportionally higher current, not a change in the regulator's
behaviour. No 0 mA capture was taken: with no load the output remains present for
several seconds after power is removed.

---

## 7. Power-on, 9 V setting

The 9 V setting was tested for the first time in this round.

### TEK00050 — Input threshold at the 9 V setting

![Power-on ramp at the 9 V setting, showing output capacitor charging once the input reaches 8.76 V](images/transient/TEK00050.png)

*Power-on, 9 V setting. DC-coupled, Ch1 and Ch2 2.00 V/div, 500 µs/div,
100 kS/s, Hi Res mode. Ch2 cursors: 560 mV, 1.13 ms, at 8.76 V.*

The Ch2 cursors put the input at **8.76 V** where the output capacitor begins
charging, which appears to be the limiting factor on this capture. The same input
dip seen at the 12 V setting is present here. In practice the circuit starts up
correctly from an input as low as **6.5 V** at the 9 V setting.

### TEK00051 — Output overshoot at the 9 V setting

![Power-on ramp at the 9 V setting, same capture, cursors repositioned to show slight output overshoot](images/transient/TEK00051.png)

*Power-on, 9 V setting — same capture as above, cursors repositioned.
Ch1 cursors: 9.32 V, 1.13 ms, at 9.28 V.*

A slight overshoot is present at the 9 V setting: the output rises to a peak and
then declines gently to its settled value across the remainder of the frame. It
is a soft, well-damped hump rather than a spike, and no ringing follows it.

The oscilloscope reads **9.28 V** at the peak. The instrument's voltage readout
runs consistently low, so the true figure is higher, but the peak has not been
established with a more accurate instrument and no exact value is claimed here.
An oscilloscope should not be relied on for absolute voltage accuracy.

Even with this overshoot, a 9 V QMX should not see a damaging surge originating
from the regulator — though every load is its own case.

---

## Observations

- **Reference:** REF5050 output measures 4.995 V, with no structure above the
  measurement noise floor.
- **Constant load:** no departure from the noise floor at any load from 0 mA to
  2 A, and no periodic content; no low-frequency instability at any point in the
  operating range.
- **Load-step excursion:** 32 mV in both directions, for a 0.1 A ↔ 1.5 A step —
  an effective output impedance of roughly 23 mΩ.
- **Settling:** approximately 30 µs (load applied) and 100 µs (load released) to
  within the measurement noise floor, measured by cursor on single captures.
- **Damping:** recovery is well damped in both directions; no ringing was observed.
- **Overshoot:** during load step measurements, no overshoot or undershoot beyond
  the noise floor of the measurement was observed at the resolution used.
- **Asymmetry:** recovery is slower on load release than on load application. A
  series linear regulator cannot sink current, so surplus charge on the output
  capacitance is removed only by the load — at 100 mA, slower than the loop can
  drive the pass device on.
- **Power-on, 12 V:** no overshoot at any load from 0 mA to 2 A.
- **Power-on at 9 V:** the output capacitor begins charging at 8.76 V input on the
  captured ramp, while the circuit itself starts correctly from 6.5 V in.
- **Power-on overshoot at 9 V:** slight and well damped; scope reads 9.28 V at the
  peak, and the instrument reads low, so the true peak is higher but not
  established.
- **Power-off:** output tracks the input down under load until it collapses below
  dropout, cleanly and without oscillation at every load; the collapse arrives
  sooner at higher currents because the load discharges the supply reservoir
  faster. Unloaded, the output persists for several seconds.
- **Power-on interval:** the cursor interval from trigger to settled output grows
  with load — 910 µs at 0 mA, 1.01 ms at 100 mA and 500 mA, 1.24 ms at 1 A,
  1.46 ms at 1.5 A and 1.72 ms at 2 A. This is dominated by the input ramp and is
  not a regulator start-up figure; see the limitations below.
- **Settled output at 2.00 V/div:** the power-on cursors read 11.88 V at 0 mA to
  500 mA, 11.84 V at 1 A and 1.5 A, and 11.80 V at 2 A. At this vertical scale
  the readings are coarse and the instrument reads low; treat them as indicative,
  not as a load-regulation measurement.

---

## Measurement limitations

Read the captures with the following in mind:

- **AC coupling.** For the load-step captures the channel is AC-coupled, so those
  captures show the transient excursion and recovery but **not** the static
  load-regulation shift between the
  0.1 A and 1.5 A operating points. For that figure see the
  [DC bench measurements](measurements.md).
  AC coupling is also a practical necessity here: no commonly available
  oscilloscope has the vertical resolution to resolve millivolt-level detail
  superimposed on a 12 V DC level, so the DC component must be removed to observe
  the transient at this sensitivity. The power-on and power-off captures show the
  absolute output and input voltages as they ramp, and are therefore not
  AC-coupled; the sensitivity argument above does not apply to them.
- **Settling-time criterion.** The settling times were read subjectively from the
  waveform, as the point beyond which the trace no longer visibly approaches its
  final value, rather than by the standard 10 %–90 % rise/fall-time convention
  used for digital circuits. This criterion was chosen deliberately: it better
  reflects the time between the load change and the output reaching its final
  voltage, at the cost of appearing to take longer. It also depends on how far
  into the noise the trace can be followed: the quieter settled band on the V2.1
  revision extends the visible tail, placing the cursor later than the ~2 mV p-p
  band on V2 allowed. The effect is largest on release, where the final approach
  is asymptotic. **The figures on this page and on the
  [V2 page](transient.md) are therefore not directly comparable, and the longer
  V2.1 figures do not indicate slower recovery.**
- **Noise floor.** The settled trace shows a band of noise, which includes probe
  and ground-loop pickup and, on the captures taken with the load connected,
  artefacts from the electronic load at this sensitivity. The ground-reference
  captures in section 1 show the same setup measured against ground, without the
  electronic load contributing; repeating the constant-load captures with
  resistive loads removes the texture, confirming its origin.
  This is an upper bound on what the setup can resolve — **these captures are not
  a ripple measurement although no ripple is observed** — and the timebase and
  sample rate here are chosen for the transient, not for characterising
  high-frequency content.
- **Input ramp rate.** The input does not rise instantaneously when the supply
  output is switched on. The ramp is shaped by the supply's current limiting and
  internal electronics, by cable inductance, and by other factors not isolated
  here; the load-dependent dip visible on Ch2 in section 5 is part of the same
  effect. **No accurate figure for regulator start-up time can be taken from
  these captures**, since the input transition itself dominates.
- **Oscilloscope voltage accuracy.** The instrument's voltage readout runs low
  against reality, as noted for the 9 V overshoot above. Absolute voltages read
  from these captures should be treated as approximate.
- **Single captures, single board.** Each trace is one capture on one board;
  treat the figures as representative rather than guaranteed limits.

---

## Relationship to the specification table

These captures are the source of the following rows in the
[specification table](design.md#electrical-specifications):

- **Reference voltage** — 4.995 V.
- **Load-step excursion** — 32 mV, 0.1 A ↔ 1.5 A.
- **Load-step overshoot / undershoot** — none observed beyond the measurement
  noise floor.
- **Load-step settling time** — ~30 µs (load applied), ~100 µs (load released).
- **Power-on overshoot, 9 V setting** — slight; scope reads 9.28 V at the peak.
- **Minimum input voltage, 9 V setting** — 6.5 V.

Loop characterisation, PSRR and output-noise measurements remain outstanding, as
noted under [Validation Status](design.md#validation-status).

---

*Oscilloscope measurements: **CR7BTQ**, August 2026, single V2.1 sample, 12 V and 9 V
settings, 13.800 V input at 5 A limit, constant loads 0 mA to 2 A, electronic
load steps 0.1 A ↔ 1.5 A. See the [project README](design.md) for design
rationale and the full specification table.*
