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
  
  Commands to run placement using RePlAce:  
  
```bash
  #Change directory to path containing generated placement def
  $ cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/27-01_18-04/results/placement/

  #Command to load the placement def in magic tool
  magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

![placement](https://github.com/user-attachments/assets/0fea020c-87b5-4f41-8495-8cdd89534a06)
![standard cells  (1)](https://github.com/user-attachments/assets/133263f3-f1e2-42d8-8e16-24bab6115ea8)
![unpaced cells](https://github.com/user-attachments/assets/9a6b365f-9e18-4b1c-ae60-721e5d60dcd0)

</details>

<details>
  <summary>Sky130-Day-3: Labs for CMOS inverter ngspice simulations. Inception of layout and CMOS fabrication process. Sky130 tech file labs</summary>
  1.Git clone vsdstdcelldesign    
  Commands to open inverter layout in magic  
  
```bash
  #Change directory to openlane
  cd Desktop/work/tools/openlane_working_dir/openlane

  #Clone the repository with custom inverter design
  git clone https://github.com/nickson-jose/vsdstdcelldesign

  #Change into repository directory
  cd vsdstdcelldesign

  #Copy magic tech file to the repo directory for easy access
  cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

  #Check contents whether everything is present
  ls

  #Command to open custom inverter layout in magic
  magic -T sky130A.tech sky130_inv.mag &
```

![cmos_layout_command](https://github.com/user-attachments/assets/402e1da1-ffab-4b8f-9082-652c77168924)

CMOS layout  
![cmos_layout](https://github.com/user-attachments/assets/82aac6c2-1a37-4dee-8065-c25a349ecfcc)
NMOS
![nmos](https://github.com/user-attachments/assets/022da420-49eb-4d3e-b0b8-6ab0b81bdf96)
PMOS
![pmos](https://github.com/user-attachments/assets/7549b7fb-ea4f-400a-8036-4c4704607fe0)
Y connectivity to PMOS and NMOS drain  
![nmos_ _pmos_drain](https://github.com/user-attachments/assets/9b08d842-1dbe-48dc-8ab9-b1e975b73f25)
VDD(VPWR)
![connected_to_vdd](https://github.com/user-attachments/assets/23c5111d-6049-43dc-a275-9c176e986a95)
VSS(VGND)  
![connected_to_vss](https://github.com/user-attachments/assets/b1bbb857-dcd5-4846-803c-1a84e1362b49)

  2.Spice extraction of inverter in magic.  

```bash
  #Check current directory
  pwd

  #Extraction command to extract to .ext format
  extract all

  #Before converting ext to spice this command enable the parasitic extraction also
  ext2spice cthresh 0 rthresh 0

  #Converting to ext to spice
  ext2spice
```
![create_spice_file](https://github.com/user-attachments/assets/5fdc75fa-211d-4a14-8ded-1285fb1c59a1)  
Spice file  
![spice_file](https://github.com/user-attachments/assets/99f66866-adc1-4f24-ae74-c0d9303edbac)  

  3.Editing the spice model file for analysis through simulation.
  Edited spice file  
![create_spice_file](https://github.com/user-attachments/assets/a8cde3c9-a3a6-4e9d-96e7-ba7d57aba040)  

  4.Ngspice simulation
  Commands for ngspice simulation
  
```bash
  #Command to directly load spice file for simulation to ngspice
  ngspice sky130_inv.spice

  #Now that we have entered ngspice with the simulation spice file loaded we just have to  load the plot
  plot y vs time a
```

![ngspice](https://github.com/user-attachments/assets/32b16492-d610-49e3-b14f-b2d5636884f8)
  Transient Response 
![transient_response](https://github.com/user-attachments/assets/275e19fe-9e8c-4a11-8125-289cec81aa73)  
  20%  
![20%](https://github.com/user-attachments/assets/e27a8906-b62f-4447-b0f4-0fdd1f7bbc97)
![Screenshot from 2025-02-03 14-17-02](https://github.com/user-attachments/assets/e948724e-c47c-4fa3-81e7-721d3c254a35)
  Cell rise delay
![cell_rise_delay](https://github.com/user-attachments/assets/4784926b-6f26-4a62-af4f-8eb0cf665a7e)  
![Screenshot from 2025-02-03 14-17-11](https://github.com/user-attachments/assets/6d597c8c-f8bf-4435-b542-e9fd73efd380)  

  5.Find problem in the DRC section of the old magic tech file and fix them
  Commands to download and view the corrupted skywater process magic tech file

```bash
  
  #Command to download the lab files
  wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

  #Since lab file is compressed command to extract it
  tar xfz drc_tests.tgz

  #Change directory into the lab folder
  cd drc_tests

  #List all files and directories present in the current directory
  ls -al

  #Command to view .magicrc file
  gvim .magicrc

  #Command to open magic tool in better graphics
  magic -d XR &
```
![drc_tests](https://github.com/user-attachments/assets/6b596976-46c4-4e3c-bcab-149e0caba4ba)

![open_magicrc](https://github.com/user-attachments/assets/85864c52-7709-4706-8105-25c4b8a68b04)  

  .magicrc file
![magicrc_file](https://github.com/user-attachments/assets/c70354f2-a65d-4bad-b33a-744521b19940)  

  Poly rules for metal3
![m3_rules](https://github.com/user-attachments/assets/bb556488-95d3-48c2-b894-af097d2fcc6a)  
  Contact Cuts
![contact cuts](https://github.com/user-attachments/assets/c52cc50e-5110-479f-85d6-5c706449c1af)

  Incorrectly implemented poly.9 rule no drc violation even though spacing < 0.48u
![incorrects](https://github.com/user-attachments/assets/a3a14a0a-bcfd-46bd-adae-1b3051e090b9)
![incorrectly_poly9](https://github.com/user-attachments/assets/e23cd9e6-f7f6-412f-acfc-a0adae5cd4f0) 

  New commands inserted in sky130A.tech file to update drc
![incorrectly_poly9(2)](https://github.com/user-attachments/assets/fe99564b-1eed-4a0c-a892-d4e5eaaa2529)
![incorrectly_poly9(3)](https://github.com/user-attachments/assets/9a597734-094e-4921-ad83-82609b3da8fe)  

  Commands to run in tkcon window
  
```bash
  #Loading updated tech file
  tech load sky130A.tech

  #Must re-run drc check to see updated drc errors
  drc check

  #Selecting region displaying the new errors and getting the error messages 
  drc why
```

![incorrect_poly9](https://github.com/user-attachments/assets/120817b9-e503-497f-b022-155de67f593c)
![diff](https://github.com/user-attachments/assets/954bb75b-976b-4b1d-b4e3-8ad6e4d090af)  

  Nwell 
![nwell](https://github.com/user-attachments/assets/7f0c4cc8-216e-456c-9117-0b35deab7322)   

  Incorrectly implemented nwell.4 rule no drc violation even though no tap present in nwell
![error_nwell](https://github.com/user-attachments/assets/949fa6d0-f78c-4502-9e09-149ad4da804d)  

  New commands inserted in sky130A.tech file to update drc
![Screenshot from 2025-02-03 14-43-27](https://github.com/user-attachments/assets/425182e5-819d-47c1-b72f-7a47ecee86d0)
![Screenshot from 2025-02-03 14-42-57](https://github.com/user-attachments/assets/57259d20-97ca-4fcb-b01c-d40b6a70de6e)  

  Commands to run in tkcon window

```bash
  #Loading updated tech file
  tech load sky130A.tech

  #Change drc style to drc full
  drc style drc(full)

  #Must re-run drc check to see updated drc errors
  drc check

  #Selecting region displaying the new errors and getting the error messages 
  drc why
```

</details>
