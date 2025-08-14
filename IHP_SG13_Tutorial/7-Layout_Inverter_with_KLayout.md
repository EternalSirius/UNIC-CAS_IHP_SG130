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

- For a homogenous ILDO with `$$\varepsilon_R$$=4.1`, the effective thickness corresponds to `deff=620nm`.

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

### 7.2.4. Design Rules in IHP-SG13G2 - GatPoly

| **Rule** | **Description**                                                                 | **Value (µm)** |
|----------|----------------------------------------------------------------------------------|----------------|
| Gat.a    | Minimum GatPoly width                                                           | 0.13           |
| Gat.a1   | Minimum GatPoly width for channel length of 1.2 V NFET                          | 0.13           |
| Gat.a2   | Minimum GatPoly width for channel length of 1.2 V PFET                          | 0.13           |
| Gat.a3   | Minimum GatPoly width for channel length of 3.3 V NFET                          | 0.45           |
| Gat.a4   | Minimum GatPoly width for channel length of 3.3 V PFET                          | 0.40           |
| Gat.b    | Minimum GatPoly space or notch                                                  | 0.18           |
| Gat.b1   | Minimum space between unrelated 3.3 V GatPoly over Activ regions                | 0.25           |
| Gat.c    | Minimum GatPoly extension over Activ (end cap)                                  | 0.18           |
| Gat.d    | Minimum GatPoly space to Activ                                                  | 0.07           |
| Gat.e    | Minimum GatPoly area                                                            | 0.09           |
| Gat.f    | 45-degree and 90-degree angles for GatPoly on Activ area are not allowed        | —              |
| Gat.g    | Minimum GatPoly width for 45-degree bent shapes if the bend GatPoly length is > 0.39 µm | 0.16     |

![](images/7.8-GatPoly.png)

### 7.2.5. Design Rules in IHP-SG13G2 - pSD

| **Rule**  | **Description**                                                                 | **Value (µm)** |
|-----------|----------------------------------------------------------------------------------|----------------|
| pSD.a     | Minimum pSD width                                                               | 0.31           |
| pSD.b     | Minimum pSD space or notch (Note 1)                                             | 0.31           |
| pSD.c     | Minimum pSD enclosure of P+Activ in NWell                                       | 0.18           |
| pSD.c1    | Minimum pSD enclosure of P+Activ in PWell                                       | 0.03           |
| pSD.d     | Minimum pSD space to unrelated N+Activ in PWell                                 | 0.18           |
| pSD.d1    | Minimum pSD space to N+Activ in NWell                                           | 0.03           |
| pSD.e     | Minimum pSD overlap of Activ at one position when forming abutted substrate tie (Note 2) | 0.30   |
| pSD.f     | Minimum Activ extension over pSD at one position when forming abutted NWell tie (Note 2) | 0.30   |
| pSD.g     | Minimum N+Activ or P+Activ area when forming abutted tie (Note 2)               | 0.09           |
| pSD.i     | Minimum pSD enclosure of PFET gate not inside ThickGateOx                       | 0.30           |
| pSD.i1    | Minimum pSD enclosure of PFET gate inside ThickGateOx                           | 0.40           |
| pSD.j     | Minimum pSD space to NFET gate not inside ThickGateOx                           | 0.30           |
| pSD.j1    | Minimum pSD space to NFET gate inside ThickGateOx                               | 0.40           |
| pSD.k     | Minimum pSD area                                                                | 0.25           |
| pSD.l     | Minimum pSD enclosed area                                                       | 0.25           |
| pSD.m     | Minimum pSD space to n-type poly resistors                                      | 0.18           |
| pSD.n     | Minimum pSD enclosure of p-type poly resistors                                  | 0.18           |

![](images/7.9-pSD.png)

### 7.2.6. Design Rules in IHP-SG13G2 - Cont

| **Rule**  | **Description**                                                                 | **Value (µm)** |
|-----------|----------------------------------------------------------------------------------|----------------|
| Cnt.a     | Minimum and maximum Cont width                                                  | 0.16           |
| Cnt.b     | Minimum Cont space                                                              | 0.18           |
| Cnt.b1    | Minimum Cont space in a contact array of more than 4 rows and more than 4 columns (Note 1) | 0.20   |
| Cnt.c     | Minimum Activ enclosure of Cont                                                 | 0.07           |
| Cnt.d     | Minimum GatPoly enclosure of Cont                                               | 0.07           |
| Cnt.e     | Minimum Cont on GatPoly space to Activ                                          | 0.14           |
| Cnt.f     | Minimum Cont on Activ space to GatPoly                                          | 0.11           |
| Cnt.g     | Cont must be within Activ or GatPoly                                            | —              |
| Cnt.g1    | Minimum pSD space to Cont on nSD-Activ                                          | 0.09           |
| Cnt.g2    | Minimum pSD overlap of Cont on pSD-Activ                                        | 0.09           |
| Cnt.h     | Cont must be covered with Metal1                                                | —              |
| Cnt.j     | Cont on GatPoly over Activ is not allowed                                       | —              |

![](images/7.10-Cont.png)

### 7.2.7. Design Rules in IHP-SG13G2 - Metal1

| **Rule** | **Description**                                                                 | **Value** |
|----------|----------------------------------------------------------------------------------|-----------|
| M1.a     | Minimum Metal1 width                                                            | 0.16 µm   |
| M1.b     | Minimum Metal1 space or notch                                                   | 0.18 µm   |
| M1.c     | Minimum Metal1 enclosure of Cont                                                | 0.00 µm   |
| M1.c1    | Minimum Metal1 endcap enclosure of Cont (Note 1)                                | 0.05 µm   |
| M1.d     | Minimum Metal1 area                                                             | 0.09 µm²  |
| M1.e     | Minimum space of Metal1 lines if at least one line is wider than 0.3 µm and the parallel run is more than 1.0 µm | 0.22 µm   |
| M1.f     | Minimum space of Metal1 lines if at least one line is wider than 10.0 µm and the parallel run is more than 10.0 µm | 0.60 µm   |
| M1.g     | Minimum 45-degree bent Metal1 width if the bent metal length is > 0.5 µm        | 0.20 µm   |
| M1.i     | Minimum space of Metal1 lines of which at least one is bent by 45-degree        | 0.22 µm   |
| M1.j     | Minimum global Metal1 density                                                   | 35.0 %    |
| M1.k     | Maximum global Metal1 density                                                   | 60.0 %    |

![](images/7.11-Metal1.png)

## 7.3. Launch KLayout

- Run the following command in the terminal to launch `klayout`.

```sh
$ source $HOME/unic-cass/env.sh
$ export KLAYOUT_PATH=$PDK_ROOT/$PDK/libs.tech/klayout:$HOME/.klayout
$ export KLAYOUT_HOME=$HOME/.klayout
$ klayout -e
```

![](images/7.12-klayout.png)

## 7.4. Create a New Layout

Create a new layout by selecting `File` >> `New Layout` and change the information as follows.

- Technology: `sg13g2 - IHP SiGe 130nm technology`

- Top cell: `inverter`

- Database unit: `0.005`

![](images/7.13-create_new_layout.png)


