---
title: 3. IHP SG130 PDK Organization
layout: default
parent: false
has_toc: false
has_children: false
---
{: .no_toc }
# 3. IHP SG130 PDK Organization

{: .no_toc }

<!-- <details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details> -->

This section describes the organization of the IHP SG130 PDK


## 3.1. IHP-SG130 Open PDK

- Github repo: [Link](https://github.com/IHP-GmbH/IHP-Open-PDK/)

- PDK docs: [Link](https://ihp-open-pdk-docs.readthedocs.io/en/latest/index.html)

- Open libraries: [Link](https://github.com/IHP-GmbH/IHP-Open-DesignLib)

Tapeouts:

- November 2024: [Link](https://github.com/IHP-GmbH/TO_Apr2025)

- April 2025: [Link](https://github.com/IHP-GmbH/TO_Apr2025)

- Next tapeout: `September 2025`.

![](images/3.1-overview_pdk.png)

### Comparison Table

| **SiGe-HBT**           | SG13S              | SG13G2             | SG13G3Cu           |
|------------------------|--------------------|--------------------|--------------------|
| f<sub>T</sub> / f<sub>max</sub> | 250 / 340 GHz     | 350 / 450 GHz     | 470 / 650 GHz     |
| W<sub>Emitter</sub>    | 170 nm             | 130 nm             | 110 nm             |
| HBT BV<sub>CEO</sub>   | 1.7 V              | 1.6 V              | 1.5 V              |
| **CMOS node**          | **130 nm**         | **130 nm**         | **130 nm**         |
| Active devices         | Schottky diodes, Antenna diodes, PN diodes, ESD | Schottky diodes, Antenna diodes, PN diodes, ESD | Schottky diodes, Antenna diodes, PN diodes, ESD |
| Varactors              | NMOS Varactor      | NMOS Varactor      | NMOS Varactor      |
| Resistors              | Poly-Si, Thin Film | Poly-Si, Thin Film | Poly-Si            |
| MIM Caps               | 1.5 fF / µm² (Al), 2.1 fF / µm² (Cu) | 1.5 fF / µm² (Al), 2.1 fF / µm² (Cu) | 2.1 fF / µm²       |
| Metallization          | 7 Layers AL incl. 2 & 3 µm layers or *Cu: 4 + 2 (3µm), AL: 2 (3µm) | 7 Layers AL incl. 2 & 3 µm layers or *Cu: 4 + 2 (3µm), AL: 2 (3µm) | 7 Layers AL incl. 2 & 3 µm layers or *Cu: 4 + 2 (3µm), AL: 2 (3µm) | *Cu BEOL from X FAB
