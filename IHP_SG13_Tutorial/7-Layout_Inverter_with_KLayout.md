---
title: 7. Layout an Inverter in IHP SG130 with KLayout including DRC and LVS
layout: default
parent: false
has_toc: false
has_children: false
---
{: .no_toc }
# 7. Layout an Inverter in IHP SG130 with KLayout including DRC and LVS

{: .no_toc }

<!-- <details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details> -->

This section introduces how to layout the inverter in IHP SG130 PDK with KLayout including DRC and LVS.

## 7.1. KLayout GUI

KLayout is capable of:

- Drawing layout of complex structures

>> Standard cells

>> Analog blocks

>> MEMs, etc.

- Parametric cell supports

>> Change cell parameters

- Capability of doing DRC/LVS

- Morden user interface

![](images/7.1-klayout_gui.png)

## 7.2. IHP-SG13G2 Process Cross Section

![](images/7.2-overview_metal_layer.png)

- BEOL detail cross-section below `Metal1` for passive modeling

![](images/7.3-BEOL.png)

### Remark:

- ILDO consists of oxide (`590nm`) and nitride (`50nm`)

- For a homogenous ILDO with `$\varepsilon_R$=4.1`, the effective thickness corresponds to `deff=620nm`.

### 7.2.1. Design Rules in IHP-SG13G2 - Rule check schematics

![](images/7.4-rule_check_schematic_1.png)

![](images/7.5-rule_check_schematic_2.png)

### 7.2.2. Design Rules in IHP-SG13G2 - NWell

| **Rule** | **Description**                                                                 | **Value (µm)** |
|----------|----------------------------------------------------------------------------------|----------------|
| NW.a     | Minimum NWell width                                                             | 0.62           |
| NW.b     | Minimum NWell space or notch (same net). NWell regions separated by less than this value will be merged. | 0.62           |
| NW.b1    | Minimum PWell width between NWell regions (different net) (Note 3)              | 1.80           |
| NW.c     | Minimum NWell enclosure of P+Activ not inside ThickGateOx                       | 0.31           |
| NW.c1    | Minimum NWell enclosure of P+Activ inside ThickGateOx                           | 0.62           |
| NW.d     | Minimum NWell space to external N+Activ not inside ThickGateOx                  | 0.31           |
| NW.d1    | Minimum NWell space to external N+Activ inside ThickGateOx                      | 0.62           |
| NW.e     | Minimum NWell enclosure of NWell tie surrounded entirely by NWell in N+Activ not inside ThickGateOx | 0.24           |
| NW.e1    | Minimum NWell enclosure of NWell tie surrounded entirely by NWell in N+Activ inside ThickGateOx | 0.62           |
| NW.f     | Minimum NWell space to substrate tie in P+Activ not inside ThickGateOx          | 0.24           |
| NW.f1    | Minimum NWell space to substrate tie in P+Activ inside ThickGateOx              | 0.62           |

![](images/7.6-nwell.png)

### 7.2.3. Design Rules in IHP-SG13G2 - Active

| **Rule** | **Description**                     | **Value (µm)** |
|----------|-------------------------------------|----------------|
| Act.a    | Minimum Activ width                 | 0.15           |
| Act.b    | Minimum Activ space or notch        | 0.21           |
| Act.c    | Minimum Activ drain/source extension| 0.23           |
| Act.d    | Minimum Activ area                  | 0.122          |
| Act.e    | Minimum Activ enclosed area         | 0.15           |

![](images/7.7-active.png)


