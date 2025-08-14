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

## 7.5. Create NMOS Instance

- 1. Create a new `nmos` instance by clicking on `Instace` button

- 2. In the instance dialog, select the `library` as `SG13_dev - IHP SG13G2 Pcells`

- 3. Click on `search button`

- 4. Select `nmos`, then press `OK`

![](images/7.14-create_nmos.png)

Finally, click on the layout to place the `nmos`.

## 7.6. Create PMOS Instance

- 1. Create a new `pmos` instance by clicking on `Instace` button

- 2. In the instance dialog, select the `library` as `SG13_dev - IHP SG13G2 Pcells`

- 3. Click on `search button`

- 4. Select `pmos`, then press `OK`

![](images/7.15-create_pmos.png)

Finally, click on the layout to place the `pmos`.

## 7.7. Change the Layout Visibility

- Display all the layer in the layout by changing the depth (e.g.: `2`).

![](images/7.16-change_visibility.png)

## 7.8. Hide Empty/Unused Layers

- Right click on `layers` panel and select `Hide Empty Layers`

![](images/7.17-hide_layers.png)

## 7.9. Align NMOS and PMOS

- Click on `Move` button and move the `pmos` such that the `poly` of the `pmos` and `nmos` in the same line

![](images/7.18-move_pmos.png)

- Use the `arrow` keys on your keyboard to move the `nmos` down.

![](images/7.19-move_nmos.png)

## 7.10. Connect the Poly

- Click on `GatPoly.drawing` in the `Layers` panel

- Click on `Box` button then draw a box between the two poly

>> Note: The size needs to be exact as the one in the `pmos` and `nmos`

- You can use zoom in and out to help place it correctly.

![](images/7.20-draw_poly.png)

## 7.10. Connect the Terminals

- Click on `Metal1.drawing` on the `Layers` panel

- Draw a box between two terminals by clicking on `Box` button and start drawing

- It should cover the two small box inside the `pmos` and `nmos`

![](images/7.21-draw_terminals.png)

## 7.11. Create the Pins

- Click on `Metal1.pin` on the `Layers` panel and draw a box with the same size as the previous one

![](images/7.22-draw_pins.png)

## 7.12. Change Pin Name

- Click on `Metal1.text` on the `Layers` panel

>> Right click on `Layers` panel >> Uncheck hide empty layers

- Click on the `text` button and place it into `Metal1.pin` region (go back to select mode by press `esc`)

- Double click on the text and change it into `Y`

![](images/7.23-change_pin_name.png)

Final view is shown as follows.

![](images/7.24-final_view.png)

## 7.13. Connect Poly to Metal1

- Click on `GatPoly.Drawing` and draw a box of about `0.2um x 0.2um` to the gate terminal

- Draw a `Metal1` over the above box with the same size

>> Click on `Metal1.drawing` and draw a box

- Connect `Metal` to `GatPoly`

>> Click on `Cont.drawing` and draw a small box inside

![](images/7.25-connect_poly_metal1.png)

## 7.14. First DRC Check

- Select `Tools` >> `DRC` >> `sg13g2_minimal.lydrc`

- Click on the DRC violation, it will be highlighted in the layout view

![](images/7.26-select_drc.png)

- In the figure, `M1.b` rule is violated, the minimum `Metal1` space or notch must be `>=0.18um`

![](images/7.27-highlight_violation.png)

## 7.15. Second DRC Violation

- Rule `Cnt.a` is violated the minimum and maximum contact width `=0.16um`

![](images/7.28-second_violation.png)

## 7.16. Fixed the DRC

- Delete the gate `poly` and the `Metal1` and the `contact`

>> Select the `gate poly`, `Metal1` and the `Contact` and press `Delete` key

- Draw a new one with bigger size

![](images/7.29-fixed_drc.png)

>> Note: You can use the ruler to have some idea of the size

- After completed, rerun the DRC, it passes

![](images/7.30-final_view.png)

## 7.17. Create the A Pin

- Select `Metal1.pin` in the `Layers` panel and draw a box with the same size as the previous one

- Select `Metal1.text` in the `Layers` panel and click `Text` button to place the text inside the pin

![](images/7.31-change_pin_name.png)

- Double click on the `text` to change it into `A`

![](images/7.32-final_view.png)

## 7.18. Extend the NWell for the PMOS

- Click on `Ruler` and create a ruler approximately `0.3um` from the upper edge of `pmos`

![](images/7.33-create_ruler.png)

- Select `Nwell.drawing` and draw a box to extend the nwell `0.3um` long on the `pmos`

![](images/7.34-draw_nwell.png)

## 7.19. Create Metal 1

- Select `Metal1.drawing` and draw a box with the same size

- Select `Metal1.pin` and draw a box with the same size

![](images/7.35-draw_metal1.png)

## 7.20. Create the VDD Text

- Click on `Metal1.text` and select `Text` button

- Place the text inside `VDD` pin

- Change the text to `VDD`

![](images/7.36-create_vdd_text.png)

## 7.21. Connect the Substrate and Terminal

- Select `Act.drawing` and draw a box with the same size as `VDD` pin

- Select `Cont.drawing` and plot some small boxes inside the `VDD` pin region

>> Note that it must follow the DRC rule

- Select `Metal1.drawing` and connect the terminal to `VDD` pin

![](images/7.37-connect_substrate_terminal.png)

## 7.22. Run DRC Again

- Run DRC by selecting `Tools` >> `DRC` >> `sg13g2_minimal.lydrc`

- The results show that it is clean

>> We ignore three violation in the figure at this moment

![](images/7.38-run_drc_agin.png)



