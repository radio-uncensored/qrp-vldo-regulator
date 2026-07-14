# M9OMS VLDO V2 — Transient Response (Load-Step Measurements)

Oscilloscope captures of the VLDO V2 output during load steps between **0.1 A and
1.5 A**, at the **12 V setting** with a **13.8 V input**. This page records the
measurements behind the load-step rows of the
[specification table](design.html#electrical-specifications). It supplements the
[DC and thermal bench measurements](measurements.html); loop characterisation
(phase margin, gain margin, unity-gain bandwidth), PSRR and broadband noise remain
**simulation-only** and are not addressed here.

> **Measurements by [CALLSIGN]** (June 2026), on a single production-representative
> V2 board, 12 V jumper setting.

---

## Test setup and conditions

- **Board:** production-representative V2, 12 V jumper setting.
- **Input:** 13.8 V DC.
- **Load:** electronic load pulsing between 0.1 A and 1.5 A. The edge rate of the
  load transition was **not characterised**; settling figures are representative
  of this setup rather than a specification against a defined load slew rate.
- **Measurement point:** output terminals, through test leads.
- **Oscilloscope:** Tektronix [MODEL], 10 MS/s sample rate, 25 µs/div timebase,
  Ch1 at 10 mV/div, AC-coupled, 20 MHz bandwidth limit enabled.
- **Trigger:** Ch1 edge at −12.6 mV, HF Reject trigger coupling.
- **Captures:** single-shot acquisitions; times measured with on-screen cursors.

---

## Load applied: 0.1 A → 1.5 A

![Output transient, 0.1 A to 1.5 A load step: output dips and recovers within approximately 25 µs](images/transient/TEK00026.png)

*0.1 A → 1.5 A load step, 12 V setting, 13.8 V in. AC-coupled, 10 mV/div,
25 µs/div. Cursors: 25.0 µs.*

When the load is applied, the output dips by roughly 15–20 mV and recovers
monotonically, settling back to within the measurement noise floor in
approximately **25 µs** by cursor measurement.

---

## Load released: 1.5 A → 0.1 A

![Output transient, 1.5 A to 0.1 A load step: output recovers upward within approximately 40 µs](images/transient/TEK00024.png)

*1.5 A → 0.1 A load step, 12 V setting, 13.8 V in. AC-coupled, 10 mV/div,
25 µs/div. Cursors: 40.0 µs.*

When the load is released, the output recovers upward by a similar 15–20 mV,
settling to within the measurement noise floor in approximately **40 µs** by
cursor measurement, with a slight, slow excursion of a few millivolts before
final settling.

---

## Observations

- **Settling:** approximately 25 µs (load applied) and 40 µs (load released) to
  within the measurement noise floor, measured by cursor on single captures.
- **Damping:** recovery is monotonic and well damped in both directions; no
  ringing was observed.
- **Overshoot:** no overshoot or undershoot beyond the ~2–3 mV noise floor of the
  measurement was observed at this resolution (10 mV/div).

---

## Measurement limitations

Read the captures with the following in mind:

- **AC coupling.** The channel is AC-coupled, so the captures show the transient
  excursion and recovery but **not** the static load-regulation shift between the
  0.1 A and 1.5 A operating points. For that figure see the
  [DC bench measurements](measurements.html).
- **Noise floor.** The settled trace shows a band of roughly 2–3 mV p-p, which
  includes probe and ground-loop pickup at this sensitivity. This is an upper
  bound on what the setup can resolve — **these captures are not a ripple
  measurement**, and the timebase and sample rate here are chosen for the
  transient, not for characterising high-frequency content.
- **Coupled spikes.** Narrow, periodic, alternating-polarity spikes visible on
  both captures are consistent with switching-edge pickup coupled into the probe
  ground loop from test equipment. They are present independent of the load-step
  event and are not attributed to the regulator; their source was not
  conclusively identified.
- **Single captures, single board.** Both traces are single-shot acquisitions on
  one board at one output setting; treat the figures as representative rather
  than guaranteed limits.

---

## Relationship to the specification table

These captures are the source of the following rows in the
[specification table](design.html#electrical-specifications):

- **Load-step overshoot / undershoot** — none observed beyond the measurement
  noise floor.
- **Load-step settling time** — ~25 µs (load applied), ~40 µs (load released).

Loop characterisation, PSRR and output-noise measurements remain outstanding, as
noted under [Validation Status](design.html#validation-status).

---

*Transient measurements: **[CALLSIGN]**, June 2026, single V2 sample, 12 V
setting, 13.8 V input, electronic load 0.1 A ↔ 1.5 A. See the
[project README](README.md) for design rationale and the full specification
table.*
