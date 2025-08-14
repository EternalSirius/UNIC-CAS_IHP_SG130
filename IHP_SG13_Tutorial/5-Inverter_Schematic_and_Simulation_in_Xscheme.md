---
title: 5. Make an Inverter's Schematic and Simulation in Xscheme
layout: default
parent: false
has_toc: false
has_children: false
---
{: .no_toc }
# 5. Make an Inverter's Schematic and Simulation in Xscheme

{: .no_toc }

<!-- <details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details> -->

This section introduces an example how to make an inverter's schematic and simulate it.

## 5.1. Create an Inverter Schematic in Xscheme

This requires two transistors, PMOS and NMOS.

- M1: sg13_lv_pmos

- M2: sg13_lv_nmos

- V1, V2: vsource.sym

The overview schematic of an inverter is illustrated as follows.

![](images/5.1-overview_inverter_schematic.png)

## 5.2. Create the Power Supply and Input Signal

With the above schematic, change the voltage source as follows.

- Change `V1` into `VIN` with `value=0`

- Change `V2` into `VDD` with `value=1.2`

![](images/5.2-change_power_and_input_signal.png)

The final schematic is shown as follows.

![](images/5.3-final_schematic.png)

## 5.3. Add the Lab Pins

- Create the lab pins for the input signal `vin` and the output signal `vout` by using the `lab_pin.sym`

- Similarly, create a lab pin for the power supply `vdd`

![](images/5.4-create_lab_pins.png)
