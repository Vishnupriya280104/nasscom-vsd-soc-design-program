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
![spice_file (3)](https://github.com/user-attachments/assets/cb2c0dc4-826f-4e8d-a285-57b8135bff38)
  
  3.Editing the spice model file for analysis through simulation.
  Edited spice file  
![spice_file (2)](https://github.com/user-attachments/assets/bc559ae5-feca-48cb-8d67-151382265256)

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

<details>
  <summary>Sky130-Day-4: Timing modelling using delay tables. Timing analysis with ideal clocks using openSTA. Clock tree synthesis TritonCTS and signal integrity. Timing analysis with  real clocks using openSTA</summary>
  1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.
  Commands to open the custom inverter layout
  
```bash
  #Change directory to vsdstdcelldesign
  cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

  #Command to open custom inverter layout in magic
  magic -T sky130A.tech sky130_inv.mag &
```

![2_tracks_info](https://github.com/user-attachments/assets/71258c28-989c-4749-b516-aa5273f9eef1)  

  Commands for tkcon window to set grid as tracks of locali layer

```bash
  #Get syntax for grid command
  help grid

  #Set grid values accordingly
  grid 0.46um 0.34um 0.23um 0.17um
```
![3](https://github.com/user-attachments/assets/1d4db088-b744-445e-9068-e9afeb8ed090)  

  Def_port layer
![4_def_port_layer](https://github.com/user-attachments/assets/5a48e68f-89df-4e0d-a74b-e64cb68dd7ef)  

  Command for tkcon window to save the layout with custom name
  
```bash
  #Command to save as
  save sky130_vsdinv.mag

  #Command to open custom inverter layout in magic
  magic -T sky130A.tech sky130_vsdinv.mag &
```

![1](https://github.com/user-attachments/assets/c63f4ea8-a284-4484-bfcd-e8b325c07a6a)  

  Lef file  
![5_lef](https://github.com/user-attachments/assets/b6f7be5a-d984-4b13-9f40-62f6a4a0ddeb)  

  2.Run openlane flow synthesis with newly inserted custom inverter cell.  
Commands to invoke the OpenLANE flow include new lef and perform synthesis  

```bash
  #Change directory to openlane flow directory
  cd Desktop/work/tools/openlane_working_dir/openlane

  #alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e  PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
  #Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
  docker
  #Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
  ./flow.tcl -interactive

  #Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
  package require openlane 0.9

  #Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
  prep -design picorv32a

  #Adiitional commands to include newly added lef to openlane flow
  set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
  add_lefs -src $lefs

  #Now that the design is prepped and ready, we can run synthesis using following command
  run_synthesis
```

![6](https://github.com/user-attachments/assets/ce3e0fb0-c1b4-4e0e-b8e2-8634011bc313)
![7](https://github.com/user-attachments/assets/e87e4f1e-c5ca-49db-85ae-7fe72b1e4851)

  3.Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.  
![9_chiparea](https://github.com/user-attachments/assets/2d97ffc8-ed09-4325-a52d-98450afcebd5)  

  Commands to view and change parameters to improve timing and run synthesis
```bash
  # Command to display current value of variable SYNTH_STRATEGY
  echo $::env(SYNTH_STRATEGY)

  #Command to set new value for SYNTH_STRATEGY
  set ::env(SYNTH_STRATEGY) "DELAY 3"

  #Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
  echo $::env(SYNTH_BUFFERING)

  #Command to display current value of variable SYNTH_SIZING
  echo $::env(SYNTH_SIZING)

  #Command to set new value for SYNTH_SIZING
  set ::env(SYNTH_SIZING) 1

  #Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
  echo $::env(SYNTH_DRIVING_CELL)

  #Now that the design is prepped and ready, we can run synthesis using following command
  run_synthesis
```

![8](https://github.com/user-attachments/assets/93c96605-368d-456d-9d22-844d24b1e5b5)  
![10](https://github.com/user-attachments/assets/f23b6f3c-31ba-4d9e-ae40-a6f26a9beca8)  

Commands to load placement def in magic in another terminal

```bash
  #Change directory to path containing generated placement def
  cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/24-03_10-03/results/placement/

  #Command to load the placement def in magic tool
  magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

![11](https://github.com/user-attachments/assets/9e68ef74-2463-43ce-b579-603c157c3bb2)
![12](https://github.com/user-attachments/assets/fd268ad7-8726-4b62-a259-45cf681562b2)  

  Command for tkcon window to view internal layers of cells

```bash
  #Command to view internal connectivity layers
  expand
```

![13](https://github.com/user-attachments/assets/480afabe-a63b-4dca-82e2-cac072f48b2c)
![14](https://github.com/user-attachments/assets/895a93ed-5515-4d72-ad61-5dc297f6d2d1)  

  4.Do Post-Synthesis timing analysis with OpenSTA tool.  
  Commands to invoke the OpenLANE flow include new lef and perform synthesis
```bash
  #Change directory to openlane flow directory
  cd Desktop/work/tools/openlane_working_dir/openlane

  #Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
  docker
  #Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
  ./flow.tcl -interactive

  #Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
  package require openlane 0.9

  #Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
  prep -design picorv32a

  #Command to set new value for SYNTH_SIZING
  set ::env(SYNTH_SIZING) 1

  #Now that the design is prepped and ready, we can run synthesis using following command
  run_synthesis
```

  Newly created pre_sta.conf for STA analysis in openlane directory
![15](https://github.com/user-attachments/assets/66f4c70a-b0a1-41ff-8e08-f0109e0ab40b)  

  Newly created my_base.sdc for STA analysis in openlane/designs/picorv32a/src directory based on the file openlane/scripts/base.sdc
![16](https://github.com/user-attachments/assets/87e0e195-6740-4fbc-84ac-24ab86742427)  

  Commands to run STA in another terminal

```bash
  #Change directory to openlane
  cd Desktop/work/tools/openlane_working_dir/openlane

  #Command to invoke OpenSTA tool with script
  sta pre_sta.conf
```

![17](https://github.com/user-attachments/assets/e8dbff08-c7bb-45b8-a4f4-2eb58dafc5ca)
![18](https://github.com/user-attachments/assets/13991cd5-5a9b-4b45-9db4-e60e97c4bfb0)
![19](https://github.com/user-attachments/assets/1490147b-04d8-49dc-8738-90acb59ae6b8)
![20](https://github.com/user-attachments/assets/994437fa-1353-4704-940a-c14871ce73ad)  

  Commands to write verilog

```bash
  #Check syntax
  help write_verilog

  #Overwriting current synthesis netlist
  write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/synthesis/picorv32a.synthesis.v

  #Exit from OpenSTA since timing analysis is done
  exit
```

![21](https://github.com/user-attachments/assets/a038f772-36ed-413f-944d-5d97dd0d28aa)  

```bash
  # Now we are ready to run placement
  run_placement

  #With placement done we are now ready to run CTS
  run_cts
```

![23](https://github.com/user-attachments/assets/9431e790-45a0-4bb2-bcfc-8d0cd6c7d8db)
![24](https://github.com/user-attachments/assets/832ea0f9-2826-4aca-bf80-3b6f1267a2b3)
![25](https://github.com/user-attachments/assets/e95818a9-fa44-4acb-a077-290fc1201d3d)
![26](https://github.com/user-attachments/assets/5863f01e-6583-4f06-be08-3e4fc1c8dd19)
![27](https://github.com/user-attachments/assets/2d0adb2f-2b27-4006-9ae1-b6e5fd2ecd7d)
![28](https://github.com/user-attachments/assets/8819bfe3-3a5a-4a3f-a41c-9427c1a51c80)
![29](https://github.com/user-attachments/assets/7bff2b55-73b4-4a71-bc94-d7e3d2478ef6)


</details>
