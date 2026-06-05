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

# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker

# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit
Screenshots of running each commands
