---
title: 2. Xscheme and NGSpice Demonstration
layout: default
parent: false
has_toc: false
has_children: false
---
{: .no_toc }
# 2. Xscheme and NGSpice Demonstration

{: .no_toc }

<!-- <details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details> -->

This section demonstrates the usage of Xschem and NGSpice opensource tools.

## 2.1. Run Xscheme

- Open a Ubuntu 22.04 terminal and run the following commands (assuming that you already installed the tools):

![](images/2.1-command_view.png)

```sh
$ source $HOME/unic-cass/env.sh
$ xschem
```

- The window pops up successfully as follows.

![](images/2.2-xschem_main_window.png)

### Source

- [Xscheme Tutorial](https://xschem.sourceforge.io/stefan/xschem_man/tutorial_run_simulation.html).


## 2.2. Schematic capture - Create instances

Draw a RLC circuit in Xscheme:

- Create a new instance by selecting `Tools` >> `Insert Symbol` ``(Shift + i)``

![](images/2.3-insert_symbol.png)

- Create a resistor by `xscheme_library/devices` >> `res.sym` >> `OK` >> Click on the schematic windows

![](images/2.4-library_manager.png)

![](images/2.5-res_symbol.png)

- Create an inductor (``ind.sym``)

![](images/2.6-create_inductor.png)

- Create a capacitor (``capa.sym``)

![](images/2.7-create_capacitor.png)

- Create an arithmetic source (``vsource_arith.sym``)

![](images/2.8-create_arithmetic_symbol.png)
