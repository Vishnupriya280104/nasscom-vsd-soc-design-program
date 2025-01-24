# nasscom-vsd-soc-design-program

<details>
  <summary>Sky130-Day1: Inception of open-source EDA, openLANE and Sky130 PDK</summary>
  Commands to invoke the OpenLANE flow and perform synthesis:

```bash
  # Change directory to OpenLANE flow directory
  $cd Desktop/work/tools/openlane_working_dir/openlane

  # Invoke the OpenLANE flow Docker subsystem
  # (Ensure Docker is installed and configured on your system)
  $docker

  # Start the OpenLANE interactive flow
  %./flow.tcl -interactive

  # Load OpenLANE required packages
  %package require openlane 0.9

  # Prepare the design for synthesis
  %prep -design picorv32a

  # Run the synthesis process
  %run_synthesis
```
</details>
