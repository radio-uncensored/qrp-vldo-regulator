---
title: "Quiescent Current vs Stability — M9OMS VLDO V2"
description: >-
  Quiescent current measurements for the M9OMS VLDO V2 with three voltage
  reference candidates, and the stability history that led to the choice of a
  higher-Iq reference for the first V2 release.
---

# M9OMS VLDO V2 — Quiescent Current vs Stability

*By M9OMS and CR7BTQ.*

Quiescent current (Iq) measurements for the VLDO V2 across an **8 V to 18 V**
input range, with three voltage reference candidates. This page records why the
first release of V2 uses a non-traditional Vref, and highlights the importance
of oscilloscope verification: two of the three candidates measure well on a
multimeter, but only one has been verified stable on the bench.

> **Iq measurements by M9OMS**; oscillation investigation and stability
> verification by M9OMS and CR7BTQ.

---

## Background: the sawtooth oscillation

A substantial delay to this project was caused by a sawtooth oscillation on the
output. This was traced back to the voltage reference — originally an OnSemi
LP2950, chosen to keep Iq low. The LP2950 has a reputation for being somewhat
challenging to stabilise, but no matter what we tried, the oscillation remained.

![Sawtooth oscillation on the VLDO V2 output with the LP2950 reference, 633 Hz, ~60 mV p-p](images/iq/1.png)

*Sawtooth oscillation with the LP2950 reference. 20 mV/div, 1 ms/div;
cursor measurement 633 Hz.*

![Sawtooth oscillation with the LP2950 reference on a longer timebase](images/iq/2.png)

*The same oscillation on a 5 ms/div timebase.*

Loading the reference with a 10 kΩ resistor reduced the amplitude by two thirds,
but the frequency increased from 633 Hz to approximately 7 kHz. This was not
acceptable.

![Reduced-amplitude, higher-frequency oscillation with the LP2950 loaded by a 10 kΩ resistor](images/iq/3.jpg)

*LP2950 loaded with 10 kΩ: amplitude reduced by two thirds, frequency raised to
approximately 7 kHz.*

Sergio suspected that, due to the topology, some current (microamps) flows from
the LTP back into the Vref. We tried the OnSemi LP2950 in a V1.1 board with the
same result — albeit a slower oscillation, due to the slow response of this
regulator.

![Slower oscillation with the LP2950 fitted to a V1.1 board](images/iq/4.jpg)

*LP2950 in a V1.1 board: the same behaviour at a lower frequency.*

---

## The fix: 78L05 as the reference

Having had a stable V1 prototype verified by Stan, M9OMS suggested a 78L05.
Whilst not a traditional voltage reference, being a regulator it would have
*some* current-sinking ability — although we have not been able to find any
documentation that cites this. Not only that, it is a legacy workhorse that is
stable. An additional benefit is that it is quieter (see the
[transient response measurements](transient.html)).

It worked: the 20 mV sawtooth disappeared and was replaced with a 2 mV ripple.
No sawtooth. This is why the first release of V2 uses a higher-Iq component.

---

## V2.1: next steps

V2.1 is underway. We are trying a different Vref — a precision reference that
can sink up to 10 mA. This requires thorough testing, and we are some weeks away
from dynamic characterisation.

---

## Quiescent current measurements

For reference, the Iq values for the VLDO V2 using the different Vref
candidates, across the 8 V to 18 V input range.

> **Measured by M9OMS.** Power supply: Agilent E3631A; Iq measured on an
> Agilent 34401A 6½-digit multimeter.

![Test setup: Agilent E3631A power supply and Agilent 34401A multimeter](images/iq/5.jpeg)

*Iq measurement setup: Agilent E3631A power supply and Agilent 34401A
6½-digit multimeter.*

### LP2950 reference — **unstable**

| Input voltage | Measured Iq |
|---------------|-------------|
| 8 V           | 1.13 mA     |
| 9 V           | 1.25 mA     |
| 10 V          | 1.38 mA     |
| 11 V          | 1.51 mA     |
| 12 V          | 1.85 mA     |
| 13 V          | 1.96 mA     |
| 14 V          | 2.07 mA     |
| 15 V          | 2.17 mA     |
| 16 V          | 2.27 mA     |
| 17 V          | 2.38 mA     |
| 18 V          | 2.48 mA     |

### ST 78L05ACZ reference — **stable** ([transient measurements](transient.html))

| Input voltage | Measured Iq |
|---------------|-------------|
| 8 V           | 4.54 mA     |
| 9 V           | 4.69 mA     |
| 10 V          | 4.83 mA     |
| 11 V          | 4.97 mA     |
| 12 V          | 5.28 mA     |
| 13 V          | 5.45 mA     |
| 14 V          | 5.56 mA     |
| 15 V          | 5.67 mA     |
| 16 V          | 5.77 mA     |
| 17 V          | 5.89 mA     |
| 18 V          | 5.99 mA     |

### V2.1 with new Vref — **stability not yet verified**

| Input voltage | Measured Iq |
|---------------|-------------|
| 8 V           | 1.88 mA     |
| 9 V           | 2.00 mA     |
| 10 V          | 2.13 mA     |
| 11 V          | 2.26 mA     |
| 12 V          | 2.52 mA     |
| 13 V          | 2.72 mA     |
| 14 V          | 2.83 mA     |
| 15 V          | 2.93 mA     |
| 16 V          | 3.03 mA     |
| 17 V          | 3.16 mA     |
| 18 V          | 3.25 mA     |

---

## Summary

This page clarifies why the first release of V2 uses a non-traditional Vref,
and highlights the importance of oscilloscope verification: the lowest-Iq
candidate produced a sustained sawtooth oscillation that a multimeter alone
would not reveal.

---

*Iq measurements: **M9OMS**, Agilent E3631A supply, Agilent 34401A 6½-digit
multimeter, 8 V–18 V input. Stability verification by oscilloscope; see the
[transient response measurements](transient.html). See the
[project README](README.md) for design rationale and the full specification
table.*
