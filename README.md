# OpenLane_VSDWorkshop
OpenLane Sky130 Workshop
Overview

This repository contains my learning notes, lab work, commands, screenshots, and results from the OpenLane Sky130 Workshop. The workshop covers the complete open-source ASIC Physical Design flow from RTL to GDSII using the Sky130 PDK and OpenLane toolchain.

Topics Covered
Day 1 - Inception of Open-Source EDA and OpenLANE
Introduction to ASIC Design Flow
Open-source EDA tools
Sky130 PDK overview
RTL to GDSII flow
Day 2 - Good Floorplan vs Bad Floorplan
Floorplanning concepts
Utilization factor
Aspect ratio
Placement basics
Standard cell characterization
Day 3 - Design Library Characterization
Cell design flow
Library characterization
Timing parameters
SPICE simulations
Day 4 - Pre-Layout Timing Analysis
Static Timing Analysis (STA)
Setup and Hold Time
Timing constraints
OpenSTA implementation
Day 5 - Final Steps for RTL2GDS
Power Distribution Network (PDN)
Placement optimization
Clock Tree Synthesis (CTS)
Routing using TritonRoute
Routing topology algorithms
Post-route analysis
GDSII generation
Tools Used
OpenLane
OpenROAD
OpenSTA
TritonRoute
Magic VLSI
Netgen
Sky130 PDK
Linux (Ubuntu)
Git & GitHub
Flow Implemented

RTL Design
↓
Synthesis
↓
Floorplanning
↓
Power Planning (PDN)
↓
Placement
↓
Clock Tree Synthesis (CTS)
↓
Routing (TritonRoute)
↓
Static Timing Analysis
↓
DRC/LVS Verification
↓
GDSII Generation

Learning Outcomes
Understanding complete ASIC design flow
Working with Sky130 Process Design Kit
Performing RTL-to-GDSII implementation
Analyzing timing reports
Implementing routing using TritonRoute
Exploring open-source VLSI design methodologies
References
VSD OpenLane Workshop
OpenLane Documentation
OpenROAD Documentation
SkyWater SKY130 PDK

Author: Varshitha
Domain: VLSI Design | Physical Design | ASIC Design Flow | Open-Source EDA Tools


This format looks professional and is suitable for a GitHub repository created specifically for the OpenLane Sky130 workshop.



Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK
Theory
Expand or Collapse
Implementation

Section 1 tasks:-

    Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
    Calculate the flop ratio.

F l o p   R a t i o = N u m b e r   o f   D   F l i p   F l o p s T o t a l   N u m b e r   o f   C e l l s
P e r c e n t a g e   o f   D F F ′ s = F l o p   R a t i o ∗ 100

    All section 1 logs, reports and results can be found in following run folder:

Section 1 Run - 15-03_15-51
1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform synthesis

Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
 Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker

 Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

 Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

 Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

 Exit from OpenLANE flow
exit

 Exit from OpenLANE flow docker sub-system
exit
Screenshots of running each commands
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/41cac55cbdecaf963acd0193cdfa298524029669/Screenshot%20from%202026-06-05%2021-08-05.png)
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/cbacfcafd0a5851f061498c52d714ece5520dd6b/Screenshot%20from%202026-06-05%2014-25-08.png)
2. Calculate the flop ratio.
Screenshots of synthesis statistics report file with required values highlighted
![[](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/356d3a30d08224a6b260ea636f428317fea7da17/Screenshot%20from%202026-06-03%2000-40-41.png)
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/356d3a30d08224a6b260ea636f428317fea7da17/Screenshot%20from%202026-06-03%2000-40-56.png)
Calculation of Flop Ratio and DFF % from synthesis statistics report file
F l o p   R a t i o = 1613 14876 = 0.108429685
P e r c e n t a g e   o f   D F F ′ s = 0.108429685 ∗ 100 = 10.84296854   % 
Section 2 - Good floorplan vs bad floorplan and introduction to library
Theory
Implementation

Section 2 tasks:-

    Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
    Calculate the die area in microns from the values in floorplan def.
    Load generated floorplan def in magic tool and explore the floorplan.
    Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
    Load generated placement def in magic tool and explore the placement.

A r e a   o f   d i e   i n   m i c r o n s = D i e   w i d t h   i n   m i c r o n s ∗ D i e   h e i g h t   i n   m i c r o n s

    All section 2 logs, reports and results can be found in following run folder:

Section 2 Run - 17-03_12-06
1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
2.  Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

 alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
 Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker

 Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

 Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

 Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

 Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

 Now we can run floorplan
run_floorplan

1. Calculate the die area in microns from the values in floorplan def.

Screenshot of contents of floorplan def
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/8412348413054495fda5688424a09b05fe05084a/Screenshot%20from%202026-06-05%2019-21-35.png)
Screenshots of floorplan def in magic
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/1787786932ed2da710dc61423354d469141889c8/Screenshot%20from%202026-06-05%2015-38-50.png)
Equidistant placement of ports
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/49eb7d65118f33bfd9188cc62615e14d0dafd290/Screenshot%20from%202026-06-05%2015-47-12.png)
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/d0d0defb6d056cad358a0fc8a83a5a124af5e21f/Screenshot%20from%202026-06-05%2015-50-38.png)
4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.

Command to run placement

# Congestion aware placement by default
run_placement

Screenshots of placement run
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/72a044a00220dd7e47855a879120754f5a5d42b3/Screenshot%20from%202026-06-05%2018-14-00.png)
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/27c2e34d992e462707a596b910ab3de2fcf704d9/Screenshot%20from%202026-06-05%2018-14-06.png)
5.Load generated placement def in magic tool and explore the placement.
Commands to load placement def in magic in another terminal
Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/placement/

Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
Screenshots of floorplan def in magic
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/e55f31e4f717c48fd5b7e69314683b80efabdc52/Screenshot%20from%202026-06-05%2016-33-49.png)
Commands to exit from current run
Exit from OpenLANE flow
exit

Exit from OpenLANE flow docker sub-system
exit
Exit from OpenLANE flow
exit

Exit from OpenLANE flow docker sub-system
exit
Section 3 - Design library cell using Magic Layout and ngspice characterization (18/03/2024 - 21/03/2024)
Theory
Implementation

Section 3 tasks:-

    1.Clone custom inverter standard cell design from github repository: Standard cell design and characterization using OpenLANE flow.
    2.Load the custom inverter layout in magic and explore.
    3.Spice extraction of inverter in magic.
    4.Editing the spice model file for analysis through simulation.
    5.Post-layout ngspice simulations.
    6.Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

Section 3 - Tasks 1 to 5 files, reports and logs can be found in the following folder:

Section 3 - Tasks 1 to 5 (vsdstdcelldesign)

 
 Section 3 - Task 6 files, reports and logs can be found in the following folder:
 1. Clone custom inverter standard cell design from github repository
    ![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/9025e0889bfe7596f568a64bf64e14ab1965d205/Screenshot%20from%202026-06-05%2017-07-23.png)
 2. Load the custom inverter layout in magic and explore.
Screenshot of custom inverter layout in magic
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/d63a1c54e93decb74b196236da0f96879825f801/Screenshot%20from%202026-06-05%2017-23-43.png)
polysilicon identified

3. Post-layout ngspice simulations.

Commands for ngspice simulation

# Command to directly load spice file for simulation to ngspice
ngspice sky130_inv.spice

 Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
plot y vs time a

Screenshots of ngspice run
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/6ee4b732be39e9f1b3385c3acaba64d2e47a86f6/waveform.png)
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/6ee4b732be39e9f1b3385c3acaba64d2e47a86f6/82waveform.png)
20% Screenshots
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/03f73bc391d8093159ee96e6e106a2af353d1f22/20waveform.png)
6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

Link to Sky130 Periphery rules: https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html

Commands to download and view the corrupted skywater process magic tech file and associated files to perform drc corrections
 Change to home directory
cd

 Command to download the lab files
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

 Since lab file is compressed command to extract it
tar xfz drc_tests.tgz

 Change directory into the lab folder
cd drc_tests

 List all files and directories present in the current directory
ls -al

 Command to view .magicrc file
gvim .magicrc

 Command to open magic tool in better graphics
magic -d XR &
Screenshot of .magicrc file
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/fc5710a01ba9ee0bd613a21f2e8f3970b6e281b5/magicrc.png)
Incorrectly implemented difftap.2 simple rule correction
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/910a48c68aa2ca1d39ea91c37f5c969d8e9dddfb/incorrectpoly.png)

Section 4 - Pre-layout timing analysis and importance of good clock tree
Theory
Implementation

    Section 4 tasks:-

    Fix up small DRC errors and verify the design is ready to be inserted into our flow.
    Save the finalized layout with custom name and open it.
    Generate lef from the layout.
    Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
    Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
    Run openlane flow synthesis with newly inserted custom inverter cell.
    Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
    Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
    Do Post-Synthesis timing analysis with OpenSTA tool.
    Make timing ECO fixes to remove all violations.
    Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.
    Post-CTS OpenROAD timing analysis.
    Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.

    Section 4 - Tasks 1 to 4 files, reports and logs can be found in the following folder:

Section 4 - Tasks 1 to 4 (vsdstdcelldesign)

    Section 4 - Task 4 files, reports and logs can be found in the following folder:

Section 4 - Task 4 (src)

    Section 4 - Task 5 files, reports and logs can be found in the following folder:

Section 4 - Task 5 (picorv32a)

    Section 4 - Tasks 6 to 8 & 11 to 13 logs, reports and results can be found in following run folder:

Section 4 - Tasks 6 to 8 & 11 to 13 Run (24-03_10-03)

    Section 4 - Tasks 9 to 11 logs, reports and results can be found in following run folder:

Section 4 - Tasks 9 to 11 Run (25-03_18-52)
1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.

Conditions to be verified before moving forward with custom designed cell layout:

    Condition 1: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
    Condition 2: Width of the standard cell should be odd multiples of the horizontal track pitch.
    Condition 3: Height of the standard cell should be even multiples of the vertical track pitch.

Commands to open the custom inverter layout

 Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

 Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &

Condition 2 verified
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/99d9118529cd50842d7c10702fc16bdc53a2c1c1/condition2.png)


 Perfrom detailed routing using TritonRoute and explore the routed layout.
Command to perform routing
 Check value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

 Check value of 'ROUTING_STRATEGY'
echo $::env(ROUTING_STRATEGY)

 Command for detailed route using TritonRoute
run_routing
Screenshots of routed def
![](https://github.com/varshithagurram322/OpenLane_VSDWorkshop/blob/4292d5f35540d2a962022927bfbaeb613c1d2a10/routeddef1.png?raw=true)
![](https://github.com/varshithagurram322/OpenLane_VSDWorkshop/blob/4292d5f35540d2a962022927bfbaeb613c1d2a10/routeddef2.png?raw=true)
Screenshots of commands run and timing report generated
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/3ce6cd9da0a31908dfddf1494fa03b791b8a079d/Screenshot%20from%202026-06-05%2022-26-31.png)
![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/3ce6cd9da0a31908dfddf1494fa03b791b8a079d/Screenshot%20from%202026-06-05%2022-26-43.png)
Acknowledgements

    Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd.
    Nickson P Jose, Physical Design Engineer, Intel Corporation.
    R. Timothy Edwards, Senior Vice President of Analog and Design, efabless Corporation.
