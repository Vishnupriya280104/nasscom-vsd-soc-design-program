# Nasscom-vsd-soc-design-program
Introduction to open-source EDA tools and 130nm PDKs. Floorplanning and standard cell design. Designing and characterizing a library cell. Pre-layout timing analysis and clock tree synthesis. The final leap: From RTL2GDS 

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

Screenshots of the operations
![d1_1](https://github.com/user-attachments/assets/7735f6bf-c0dd-4972-b342-163244357eb5)
![d1_2](https://github.com/user-attachments/assets/b13ec707-5916-460a-b98a-1adaa60e1b00)
![d1_3](https://github.com/user-attachments/assets/1c1f3481-1e31-42be-a011-74a17488fbe5)
![d1_4](https://github.com/user-attachments/assets/f968126c-a07c-404e-801a-08583b09ace5)

</details>
