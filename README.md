# Nasscom-vsd-soc-design-program
Introduction to open-source EDA tools and 130nm PDKs. Floorplanning and standard cell design. Designing and characterizing a library cell. Pre-layout timing analysis and clock tree synthesis. The final leap: From RTL2GDS 

<details>
  <summary>Sky130-Day1: Inception of open-source EDA, openLANE and Sky130 PDK</summary>
  Commands to invoke the OpenLANE flow and perform synthesis:

```bash
  #Change directory to OpenLANE flow directory
  $cd Desktop/work/tools/openlane_working_dir/openlane

  #Invoke the OpenLANE flow Docker subsystem
  #(Ensure Docker is installed and configured on your system)
  $docker

  #Start the OpenLANE interactive flow
  %./flow.tcl -interactive

  #Load OpenLANE required packages
  %package require openlane 0.9

  #Prepare the design for synthesis
  %prep -design picorv32a

  #Run the synthesis process
  %run_synthesis
```

Screenshots of the operations
![d1_1](https://github.com/user-attachments/assets/7735f6bf-c0dd-4972-b342-163244357eb5)
![d1_2](https://github.com/user-attachments/assets/b13ec707-5916-460a-b98a-1adaa60e1b00)
![d1_3](https://github.com/user-attachments/assets/1c1f3481-1e31-42be-a011-74a17488fbe5)
![d1_4](https://github.com/user-attachments/assets/f968126c-a07c-404e-801a-08583b09ace5)

</details>

<details>
  <summary>Sky130-Day2: Chip Floor planning considerations, Library Binding and Placement, Cell design and characterizatio flows, General timing characterization parameters.</summary>
  1.Run floorplan using openlane and steps to view floorplan
  Commands to review floorplan layout in Magic
![run_fp](https://github.com/user-attachments/assets/9d9326db-f332-48d2-9441-ea1ff53c9ab6)
![run_fp2](https://github.com/user-attachments/assets/fb49396e-b79f-451c-8e69-85e5fa8d58cc)
```bash
  #Change directory to path containing generated floorplan def
  $ cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/27-01_18- 
  04/results/floorplan/

  #Command to load the floorplan def in magic tool
  magic -T home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
![fp](https://github.com/user-attachments/assets/fc4c04f1-ff62-4d7e-ab98-1632f4789374)
![fp_port_layer_in_config](https://github.com/user-attachments/assets/052d4db7-9083-4d15-b84f-7b48131d0bd4)

 
  2.Congestion aware placement using RePlAce
![run_pc](https://github.com/user-attachments/assets/ef81ef61-3a60-403e-91a1-a43851219e3f)
![run_pc2](https://github.com/user-attachments/assets/6ab74807-6bf1-47e8-84e3-e136890711cd)
  Commands to run placement using RePlAce
```bash
  #Change directory to path containing generated placement def
  $ cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/27-01_17-23/results/placement/

  #Command to load the placement def in magic tool
  magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
![placement](https://github.com/user-attachments/assets/0fea020c-87b5-4f41-8495-8cdd89534a06)
![standard cells  (1)](https://github.com/user-attachments/assets/133263f3-f1e2-42d8-8e16-24bab6115ea8)
![unpaced cells](https://github.com/user-attachments/assets/9a6b365f-9e18-4b1c-ae60-721e5d60dcd0)

</details>
