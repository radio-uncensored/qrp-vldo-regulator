## VLDO V1

BOM, Gerber and CPL available for download. SEE NOTES BELOW.

---

<p align="center">
  <img src="images/vldo_v1_schematic.JPG" alt="M9OMS VLDO V1 schematic - low dropout (LDO) linear regulator for QRP radios such as the QRP Labs QMX" width="800">
</p>

---

## Notes

Based on G4COL's schematic, with the following changes (final, V1.2 revision):
1- Additional input bypass capacitor.
2- Voltage selection ladder & trim potentiometer.
3- SMD components.

PCB dimensions: 65mm x 20.5mm x 25mm.
3D printed housing: [https://www.thingiverse.com/thing:7246700](https://www.thingiverse.com/thing:7246700)

BOM, Gerber and CPL are shared on a **CC BY-NC-ND** basis. **Verify schematic before committing to fabrication.**

[**Download V1 BOM & Gerber here:**](downloads/bom-gerber)

Additional materials required:
- 1x 2.54mm shunt.
- 1x TO-220 isolation kit (including M3 machine screw).

## Why CC BY-NC-ND?

The BOM, Gerber and CPL files are shared on a **CC BY-NC-ND** basis to preserve the validated design configuration.

Derivatives of G4COL's original design have been published with component changes that may affect stability. In particular, changes affecting pass-device capacitance, amplifier drive capability, feedback network impedance, and reference-node behaviour should be treated carefully.

The BOM reflects the component set validated for this implementation. However, stability should still be verified, as component tolerances, substitutions, layout differences, and other factors may affect performance.
