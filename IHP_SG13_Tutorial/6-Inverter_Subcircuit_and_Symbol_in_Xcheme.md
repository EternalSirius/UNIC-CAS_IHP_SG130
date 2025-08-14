---
title: 6. Create the Inverter's Subcircuit and Symbol in Xscheme
layout: default
parent: false
has_toc: false
has_children: false
---
{: .no_toc }
#  6. Create the Inverter's Subcircuit and Symbol in Xscheme

{: .no_toc }

<!-- <details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details> -->

This section introduces how to create the inverter as a subcircuit and make its symbol with Xscheme.

## 6.1. Inverter as Subcircuit

Create an inverter schematic in Xcheme

- Input: `A` (`ipin.sym`)

- Output: `Y` (`opin.sym`)

- Power supply: `VDD` (`iopin.sym`)

- Ground: `VSS` (`iopin.sym`)

![](images/6.1-inverter_schematic.png)

Save the schematic by selecting `File` >> `Save As` >> `inverter.sch`

Next, we create the symbol for the inverter.


## 6.2. Create Symbol

Create a symbol by selecting `Symbol` >> `Make symbol from schematic`

- Click `OK` on the dialog `Do you want to make symbol view`

- A new file named `inverter.sym` will be create in the same directory

![](images/6.2-create_symbol_view.png)

The next step is to edit this symbol file.
