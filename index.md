---
title: "VLDO V2 — Very Low Dropout Regulator for QRP"
description: "Discrete, RF-quiet linear voltage regulator for QRP radios. Selectable 9.0 / 12.0 / 13.8 V at up to 2 A, with very low dropout and no switching noise."
image: /images/DSC01726.JPG
---

# M9OMS VLDO V2

A discrete **very low dropout (VLDO)** linear voltage regulator for QRP radios. Selectable **9.0 V / 12.0 V / 13.8 V** at up to **2 A**.

<p align="center">
  <img src="images/DSC01726.JPG" alt="M9OMS VLDO V2 assembled board — 65 × 20.5 mm discrete very low dropout linear regulator for QRP radios" width="560">
</p>

## Where to buy

- **[VLDO V2 on eBay](https://www.ebay.com/itm/267709192002)** https://www.ebay.com/itm/267709192002
- **[Nylon Housing on eBay](https://www.ebay.com/itm/267715531314)** https://www.ebay.com/itm/267715531314



## V2 at a glance

| | |
| :--- | :--- |
| **Type** | Discrete low-dropout (LDO) **linear** regulator |
| **Output** | 9.0 V / 12.0 V / 13.8 V (jumper-selectable, trimmed via `R7`) |
| **Max current** | 2.0 A continuous |
| **Dropout** | < 100 mV (regulation threshold) at 1 A |
| **Switching noise** | None — linear topology |
| **Designed for** | QRP radios and other portable HF rigs |

## Why a discrete LDO?

Modern QRP rigs need a stable rail, but hobbyist switching modules can introduce noise. Many 'ready' LDO boards need too much headroom to hold regulation as a battery discharges. The VLDO V2 stays quiet, keeps regulating close to the input voltage, and is built for rapid RX-TX current changes.

## Documentation

- **[Design rationale, schematic lineage & full specification table](design.md)** — the complete project README.
- **[Oscilloscope measurements](https://radio-uncensored.github.io/qrp-vldo-regulator/transient.html)** — oscilloscope captures of 0.1 A ↔ 1.5 A load steps at the 12 V setting.
- **[Static DC measurements](measurements.html)** — hardware-verified DC and thermal data (KC7XE, June 2026).
- **[V1.1 vs V2 comparison](improvements.html)** — like-for-like bench comparison of dropout and load regulation.

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
  "category": "Amateur Radio Power Supply",
  "image": "https://radio-uncensored.github.io/qrp-vldo-regulator/images/DSC01726.JPG",
  "url": "https://radio-uncensored.github.io/qrp-vldo-regulator/",
  "offers": {
    "@type": "Offer",
    "url": "https://www.ebay.co.uk/itm/267709192002",
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
