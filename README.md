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
2. Load the custom inverter layout in magic and explore.

Screenshot of custom inverter layout in magic

![](https://raw.githubusercontent.com/varshithagurram322/OpenLane_VSDWorkshop/nmos.png)




