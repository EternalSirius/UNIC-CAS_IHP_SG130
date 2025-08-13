---
title: 4. Spice Simulation using IHP SG130 PDK with Xscheme and NGSpice
layout: default
parent: false
has_toc: false
has_children: false
---
{: .no_toc }
# 4. Spice Simulation using IHP SG130 PDK with Xscheme and NGSpice

{: .no_toc }

<!-- <details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details> -->

This section introduces the spice simulation with Xscheme and NGSpice 

## 4.1. IHP Open PDK Simulation Model

Transistor Models are written in Verilog-A

- Compiled by OpenVAF before used

Use corner `.lib` for simulation

- cornerHBT.lib

- MOS model: cornerMOShv/lv.lib

- Resistor models: cornerRES.lib

Abbreviation

- mod: model

- parm: parameter of the model

- stat: statistical model

- mismatch: local statistical model

```
ihp-sg13g2/libs.tech/ngspice
.
├── models
│   ├── capacitors_mod.lib
│   ├── capacitors_stat.lib
│   ├── cornerCAP.lib
│   ├── cornerHBT.lib
│   ├── cornerMOShv/lv.lib
│   ├── cornerRES.lib
│   ├── diodes.lib
│   ├── resistors_mod[_mismatch,stat].lib
│   ├── sg13g2_bondpad.lib
│   ├── sg13g2_esd.lib
│   ├── sg13g2_hbt_mod[_mismatch,stat].lib
│   ├── sg13g2_moshv/lv_mismatch.lib
│   ├── sg13g2_moshv/lv_mod.lib
│   ├── sg13g2_moshv/lv_mod_mismatch.lib
│   ├── sg13g2_moshv/lv_parm.lib
│   ├── sg13g2_moshv/lv_stat.lib
│   ├── sg13g2_svaricaphv_mod.lib
│   ├── sg13g2_svaricaphv_mod_mismatch.lib
└── osdi // compiled models
    ├── mosvar.osdi
    ├── psp103_nqs.osdi
    └── r3_cmc.osdi
```
