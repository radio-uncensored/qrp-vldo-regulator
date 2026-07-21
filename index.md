---
title: "M9OMS VLDO V2 - RF-Quiet Power Supply for QRP Labs QMX"
description: "Discrete very low dropout (VLDO) linear voltage regulator for QRP Labs QMX and other QRP radios. RF-quiet, selectable 9.0 / 12.0 / 13.8 V output up to 2 A."
image: /images/DSC01726.JPG
---

# M9OMS VLDO V2

A discrete **very low dropout (VLDO)** linear voltage regulator for QRP radios. Selectable **9.0 V / 12.0 V / 13.8 V** at up to **2 A**.

<p align="center">
  <img src="images/DSC01726.JPG" alt="M9OMS VLDO V2 assembled board — 65 × 20.5 mm discrete very low dropout linear regulator for QRP radios" width="560">
</p>

## Where to buy

- **[eBay Shop](https://www.ebay.co.uk/usr/m9oms-radio)** https://www.ebay.co.uk/usr/m9oms-radio
- **[VLDO V2](https://www.ebay.com/itm/267709192002)** https://www.ebay.com/itm/267709192002
- **[Nylon Housing](https://www.ebay.com/itm/267715531314)** https://www.ebay.com/itm/267715531314



## V2 at a glance

| | |
| :--- | :--- |
| **Type** | Discrete low-dropout (LDO) **linear voltage regulator** |
| **Output** | 9.0 V / 12.0 V / 13.8 V (jumper-selectable, trimmed via `R7`) |
| **Maximum current** | 2.0 A continuous |
| **Dropout voltage** | < 100 mV (regulation threshold) at 1 A |
| **Switching noise** | Not a switching converter — linear topology |
| **Designed for** | QRP radios and other portable HF rigs |

## Why a discrete LDO?

Modern QRP rigs need a stable supply rail, but hobbyist switching modules can introduce noise. Many conventional LDO boards require too much voltage headroom to maintain regulation as a battery discharges. The VLDO V2 remains RF-quiet, regulates very close to the input voltage, and is designed for rapid RX-TX current changes.

## Documentation

- **[Design rationale, schematic lineage & full specification table](design.md)** — the complete project README.
- **[Oscilloscope measurements](transient.md)** — oscilloscope captures of 0.1 A ↔ 1.5 A load steps at the 12 V setting.
- **[Static DC measurements](measurements.md)** — hardware-verified DC and thermal data (KC7XE, June 2026).
- **[V1.1 vs V2 comparison](improvements.md)** — like-for-like bench comparison of dropout and load regulation.

## Credits

V2 design and hardware by **M9OMS**. DC evaluation by **KC7XE**. Stability evaluation by **CR7BTQ**.

---

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "M9OMS VLDO V2",
  "description": "Discrete very low dropout linear voltage regulator for QRP radios. Selectable 9.0 / 12.0 / 13.8 V at up to 2 A, with very low dropout and no switching noise.",
  "brand": {
    "@type": "Brand",
    "name": "M9OMS"
  },
  "category": "Linear Voltage Regulator for Amateur Radio",
  "image": "https://radio-uncensored.github.io/qrp-vldo-regulator/images/DSC01726.JPG",
  "url": "https://radio-uncensored.github.io/qrp-vldo-regulator/",
  "offers": {
    "@type": "Offer",
    "url": "https://www.ebay.co.uk/usr/m9oms-radio",
    "priceCurrency": "GBP",
    "price": "13.00",
    "availability": "https://schema.org/InStock",
    "seller": {
      "@type": "Organization",
      "name": "M9OMS"
    }
  }
}
</script>
