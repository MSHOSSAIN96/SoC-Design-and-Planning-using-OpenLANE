# SoC-Design-and-Planning-using-OpenLANE
A project based on an ASIC design's entire RTL to GDSII flow. RISC-V design (picorv32a) + open-process (google+skywater130nm) + open-lane EDA tools (efabless) are now all open-source. 
Beginning with fundamental ideas and moving through useful labs, this project provides a thorough exploration of the ASIC design process using OpenLANE and Sky130. It is constructed with open-source libraries and industry-standard EDA tools, giving users practical experience with IC design.

**Scope of work:**

I make sure users are prepared to follow the structured roadmap by outlining the prerequisites and installation procedures before they begin. The first element of the project, Theory, covers the basics of IC design, including nomenclature, components, and an outline of what distinguishes a good floorplan from a bad one. In this part, placement basics and library cells are also covered.

I explore the methods and factors needed for efficient signal routing in IC designs in the Routing section. A number of labs are included in the project to foster familiarity and practical skills.

In order to help users become accustomed to the environment, 
Lab 1 introduces with OpenLANE EDA tools.

Lab 2 demonstrates how to use OpenLANE for floorplanning and placement.

Lab 3 demonstrates the complexities of fundamental logic gates through inverter characterisation using the Sky130 model files.

Pre-layout timing analysis is covered in Lab 4, which also emphasizes the significance of a well-designed clock tree.

Lastly, Lab 5 walks users through the last stages to produce a GDSII file, which results in a comprehensive, production-ready layout of the IC design.

The goal of this roadmap is to equip users with the theoretical and practical knowledge they need to comprehend and carry out the entire IC design workflow, from theory to GDSII creation.

**Open Source Digital ASIC Design:**

1.To produce custom ASICs, Open Source Digital ASIC Design combines RTL designs, PDK data, and open-source EDA tools.

2.OpenLane, qflow, and OpenROAD are examples of EDA tools that offer design and verification software.

3.The SkyWater 130nm process is one example of PDK data that offers the specs and standards required for chip manufacture.

4.Reusable logic designs that can be incorporated into new chips are available from websites such as librecores.org and opencores.org.

5.Open-source components make ASIC design more affordable, accessible, and collaborative, enabling developers and designers to experiment without depending on pricey proprietary tools.

![F1_OpenLANE_Digital_ASIC_DESIGN](https://github.com/user-attachments/assets/bf00d03e-10f3-4526-95a0-2b3650159a77)

**Simplified RTL to GDS II flow:**

The following diagram illustrates a series of steps, from the RTL design to generating the GDSII file, which contains the layout information for chip fabrication. Each step is crucial for refining the design towards a manufacturable state:
1. Starting Points: RTL and PDK

a.RTL (Register Transfer Level): This is the initial stage of the digital design. The RTL describes the circuit behavior and structure using hardware description languages (HDLs) like Verilog or VHDL.

b.PDK (Process Design Kit): The PDK contains the design rules, standard cells, and manufacturing-specific data required to implement the design on a particular semiconductor process. It guides how the design will be physically realized on silicon.

2. Flow Stages (Middle Section):   
a.Synth (Synthesis): This step translates the RTL code into a gate-level netlist, which consists of logic gates (AND, OR, NOT, etc.) interconnected to perform the desired functionality. This process uses standard cells provided by the PDK.

b.FP + PP (Floor/Power Planning):
Floor Planning: Determines the layout of different components within the chip, defining the overall structure and size of the ASIC.
Power Planning: Involves creating a power distribution network to ensure that all parts of the chip receive adequate power without causing electrical issues.

c.Place (Placement): In this step, the synthesized logic gates (standard cells) are placed within the chip's floor plan. The goal is to optimize the placement for performance, power efficiency, and area (PPA).

d.CTS (Clock Tree Synthesis): This stage involves creating the clock distribution network. It ensures that the clock signal reaches all parts of the chip with minimal skew, which is vital for synchronizing the operations of different components.

e.Route (Routing): Routing connects the placed components (standard cells) with metal wires according to the netlist. This step establishes the physical connections needed for data and signal transfer.

f.Sign Off: This final stage involves verifying that the design meets all specifications, including timing, power, and physical constraints. It checks for issues such as design rule violations (DRC) and layout-versus-schematic (LVS) mismatches.

3. Output: GDSII
The final output of the flow is the GDSII file, which contains the complete layout of the ASIC. This file is sent to the fabrication plant (foundry) to manufacture the physical chip.

4. Summary of Steps (Right Section):

Synthesis: Converts RTL code to a gate-level netlist.

Floor/Power Planning: Establishes the layout and power distribution of the chip.

Placement: Arranges the standard cells within the floor plan.

Clock Tree Synthesis: Creates a clock network with minimal skew.

Routing: Connects components using metal wires.

Sign Off: Validates that the design is ready for manufacturing.

Overall Explanation:
This flow represents the journey of digital ASIC design from an abstract, high-level representation (RTL) to a physical layout (GDSII) ready for silicon fabrication.
The PDK provides essential manufacturing rules and data to ensure the design is feasible and can be manufactured correctly.
Each step in the flow is crucial for refining and optimizing the design to meet performance, power, and area requirements while adhering to manufacturing constraints.

![F2_Simplified_RTL_to_GDS_Flow](https://github.com/user-attachments/assets/cc51e7bd-ec2c-4c3c-a187-a77427d90448)


**OpenLANE ASIC Flow:**

Using the OpenLane ASIC pipeline, we will examine how to create an Application Specific Integrated Circuit (ASIC) from the Register Transfer Level (RTL) to the Graphical Data System (GDS) file. Starting with an RTL file and ending with a GDS file, the procedure comprises several crucial stages.

![F3_OpenLANE_ASIC_Flow](https://github.com/user-attachments/assets/6050fc37-61c1-43a6-86c8-7d8ea76607c7)

**Required tools (ASIC Flow):**
Any ASIC implementation revolves around Place and Route (PnR), and Openlane flow includes several essential open-source tools that carry out each of the PnR steps. The steps and corresponding tools that Openlane calls for the specified features are listed below:

1.Synthesis:

a.Generating gate-level netlist (yosys).

b.Performing cell mapping (abc).

c.Performing pre-layout STA (OpenSTA).

2.Floorplanning:

a.Defining the core area for the macro as well as the cell sites and the tracks (init_fp).

b.Placing the macro input and output ports (ioplacer).

c.Generating the power distribution network (pdn).

3.Placement:

a.Performing global placement (RePLace).

b.Performing detailed placement to legalize the globally placed components (OpenDP).

4.Clock Tree Synthesis (CTS):

a.Synthesizing the clock tree (TritonCTS).

5.Routing:

a.Performing global routing to generate a guide file for the detailed router (FastRoute).

b.Performing detailed routing (TritonRoute)

6.GDSII Generation/layout:

a.Streaming out the final GDSII layout file from the router def (Magic).

**How to start this project:**

Requirements:
The session goes beyond Openlane and an Ubuntu (only) machine. The user must setup a virtual machine on Windows and run the "vsdworkshop" image file; on Ubuntu, they must install "VirtualBox" and adhere to the instructions in the lab instruction file. After registering, students get access to their accounts and all required materials.

**Setting up the vdsworkshop:**
All necessary files and tools are installed along with the 'vsdworkshop' operating system. If you want to install it manually, click the link below:
**https://github.com/nickson-jose/openlane_build_script**

**A roadmap of ASIC design flow:**
Register Transfer Language (RTL) to Graphic Data System II (GDSII), a comprehensive design path in integrated circuit (IC) development, transforms a high-level hardware description into a physical layout appropriate for foundry fabrication. The RTL to GDSII process is a multi-phase process that begins with the RTL design, where the functionality of the circuit is coded into the hardware description languages using Verilog or VHDL. Synthesis, the following stage of the procedure, converts this RTL code into a gate-level netlist. After creating a netlist, the physical design process moves on to floorplanning, placement, clock-tree synthesis (CTS), and routing. After placement and routing, signoff checks are carried out, including Design Rule Checking (DRC), Layout Versus Schematic (LVS) checks, and Static Timing Analysis (STA).

![F4_Simple_ASICS_flow_chart](https://github.com/user-attachments/assets/d3438eeb-a8cc-4975-815d-19500459f271)

**The concept of IC Components, Design, and Terminology:**

Integrated circuit (IC) design is the process of joining circuit components to perform a predetermined intended purpose. Almost every electrical device you use has an integrated circuit (IC). Much has changed since Gordon Moore discovered in 1965 that the number of transistors in an integrated circuit (IC) doubles every two years (Moore's Law (opens in a new tab)). The majority of ICs in use today are a combination of the two primary IC design domains, digital and analog. IC Design Process: The IC design pipeline involves a number of steps, including:

1.Architecture design

2.Logic design

3.Physical design

4.Physical verification

5.Final step- The Signoff

![F5_IC_Design flow](https://github.com/user-attachments/assets/b36d64d8-8e1e-4ea3-adb5-223c7f7b8fd5)

1.Architecture design: 
The first step in IC design is architecture design, which establishes the high-level organization and operation of the integrated circuit. Because it lays out the IC's blueprint, defining its primary functional pieces, how they will interact, and how it will function, this phase is essential. It's comparable to creating a building's architectural blueprints before to construction.

2.Logic design:
Here, macro-level building blocks are assembled and connected to provide the IC's required functionality. Typically, pre-existing parts such as memory, processors, and sensors are used. High-level functional descriptions of circuit elements are decomposed into the corresponding low-level circuit components. This process is automated with software called logic synthesis. The set of devices is simulated in order to verify that the design is functional. Depending on the required level of modeling detail, either an analog circuit simulator or a digital logic simulator will be used.

3.Physical Design:
In this step, a layout for the connected forms of the circuit components is created. To determine the location, shape, and size of the modules inside a chip, a floorplan is first developed. Determining where to place the components and avoiding issues that could restrict speed and performance are made easier by analyzing the chip area, latency, congestion, etc. The core of the ASIC design flow, PnR, is composed of multiple stages. The following is a list of the procedures and related resources that OpenLANE uses:

a.Synthesis: establishes pre-layout STA, maps cells, and generates a gate-level netlist.The inputs are RTL design, library (standard cells and macros), and constraints (design goals, expected temporal behavior, and environment).

![F6_Synthesis](https://github.com/user-attachments/assets/f6a8ce1d-3338-4eef-8124-5aea898e4f7a)

b.Floorplanning: At this stage, important choices are made on how to organize the system's blocks on the chip, assign memory, macros, standard cells, and other resources, and split the system up into blocks and subsystems. Floorplanning includes IO cell layout and power planning.

![F7_Floorplanning](https://github.com/user-attachments/assets/2f6e5240-b303-4a95-b93b-566e89208b15)

c.Placement: The placement phases dictate the stdcell location in the design. In this step, the wire length is estimated, and the wires are positioned while taking that estimate into consideration. To complete the entire placement stage, there are three steps in the flow. Global placement, legalization, and detailed placement are the usual placement flows.

![F8_Placement](https://github.com/user-attachments/assets/ff4caeef-1494-4688-882e-1feb982008ca)

d.Clock tree synthesis: The clock network must be wired and the clock tree netlist, which contains buffers, must be implemented during the clock-tree synthesis (CTS) step. The goal of this stage is to minimize skew and power dissipation. The clock can be distributed around the network in a number of ways; here are some examples: Grids, ad hoc, hybrid, H-tree, etc. 

![F9_CTS](https://github.com/user-attachments/assets/b4531533-6eef-4be6-8f47-62f6131f01b5)

e.Routing: Routing creates the wire configuration for each net, with the exception of the clock and power supply. Details routing and global routing are the two different forms of routing. To create a routing plan for a particular net, the entire routing region is split up into rectangular tiles in the planning stage called global routing. The detailed router determines the actual routing of each pre-assigned global tile, which is where the actual wires and vias are formed.

![F10_Routing](https://github.com/user-attachments/assets/30640ded-6ca0-446c-a0c7-6ea5da587599)

**A Comparison of Good and Bad Floor Plans and an Overview of Library Cells and Palcement**
Chip Floorplanning Considerations Aspect ratio and utilization factor: In order to compute the Utilization Factor and Aspect Ratio, we must first ascertain the height and width of the core and die regions.
All of a chip's logic cells and other components are found in the core. The logic of a chip is located there.I/O-related components are positioned in the die, which encircles the core region.

![F11_Good_floorplan_bad_floorplan](https://github.com/user-attachments/assets/c876bec3-d798-4109-8dbe-88c546bd2114)

The design's netlist, which takes into account the number of components needed to execute the design logic, will determine the size of the core region. As can be seen in the image above, the height and width of the die area are therefore determined by the size of the core region. Consider a netlist that contains two flip-flops and two logic gates.

![F12_FF's_Logic_gates](https://github.com/user-attachments/assets/4359afea-d3e7-4e84-829a-5a9992bd4b9e)

if the surface area of each component is one square unit. Our netlist consists of four components, hence the core area will require at least four square units.

![F13_Surface_area _core_area](https://github.com/user-attachments/assets/65812701-ac1f-44ae-8169-7f73465527c9)

Utilization Factor: The utilization factor is the ratio of the netlist's core area to the core's total area. In an efficient floor plan, the Utilization Factor should be less than 1 since if it reaches 1, there won't be any more space for logic to be added, which leads to a subpar floor plan.

**Utilization Factor = (Area occupied by netlist / Total core area)**
Aspect ratio: The ratio of aspects The aspect ratio is the core's height-to-width proportion. When the aspect ratio is 1, the core is considered square in shape. If the aspect ratio is not 1, the core will have a rectangular shape.

**Aspect Ratio = (Height of the core / Width of the core)**

![F14_FF's_Logic_gates](https://github.com/user-attachments/assets/d40630cb-752b-4a13-aa5c-f78f4d394b71)

In this scenario, when calculated
Utilization factor = (4 sq units) / (4 sq units) = 1
Aspect Ratio = (2 units) / (2 units) = 1 which is in a square shape core.

![F15_rectangular_shape](https://github.com/user-attachments/assets/f9e21349-ec55-4b50-9a99-69558713b537)

In this scenario, when calculated
Utilization factor = (4 squints) / (8 squints) = 0.5
Aspect Ratio = (2 units)/(4 units) = 0.5 which is in a rectangular shape core.

**Decoupling Capacitor:**
The nMOS and pMOS are performed simultaneously in an input transition region of the IC. There will be a sizable short circuit current during that time. If numerous of these cells are lined up in a row and switch at the same time, a sizable current will be required. This high current requirement, sometimes referred to as ground bounce or voltage droop, may cause the ground voltage to rise or the VDD to decrease. To address this issue, decoupling capacitors or decap cells are placed adjacent to these power-hungry parts.Currently, when switching activities occur, the decoupling capacitors quickly drain to supply these components with the necessary power. When the switching is switched off, the capacitors recharge, ensuring that crucial circuit components receive a consistent and reliable power supply. In order to preserve and enhance the power distribution network, decap cells act as charge reservoirs. Decaps are essential in circuit design to maintain stable operation and prevent performance issues caused by changing power supply conditions.

![F16_Decoupling_Capacitors](https://github.com/user-attachments/assets/e0f9eb17-4fc5-48c5-84df-c9f4a3eca9e3)

Power Planning/Pre-Placement: Controlling the distribution of electricity across various blocks requires more than merely decoupling capacitors. Increased chip size and leakage power are two drawbacks of de-cap cells. Therefore, power planning is used to provide electricity effectively. In areas of the chip with high switching activity, two effects can occur: voltage drop and ground bounce. Voltage Drop: When multiple cells simultaneously flip from 0 to 1, a significant power demand results. Insufficient power from a single source necessitates a drop in input voltage for these cells. This issue gets worse as the voltage level falls below the noise margin.When multiple cells flip from 1 to 0 at the same time, power is dumped to the ground pin, causing a ground bounce. Because of this, the ground voltage briefly increases instead of remaining at zero. This results in a phenomenon known as "ground bounce." A problem arises when the voltage level exceeds the noise margin.

![F17_Power_Planning](https://github.com/user-attachments/assets/f39e85c3-fa85-451b-9d0f-3329ff1eecf9)

Library binding and placements: Each component in the netlist, including the AND, OR, and FF gates, has a square or rectangular physical dimension, which means it has width and height. These components are in the form of boxes at the library. In addition to dimensions, the library provides temporal (delay) information for these boxes or components. The library also includes information about when the output of the component is changed. Additionally, there are multiple variants of the same component, each with distinct features (size/delay).

Placement: Placement is the procedure by which the tool arranges all of the standard cells found in the netlist in the core region. During placement, the tool also optimizes the design. The tool can also be used to route trails. Placement's primary objective is to optimize timing, area, and power. 2. Reduce traffic and the areas that cause it. 3. Pin density and minimum cell density.

Three steps are involved in placement: 1. Global Placemen 2. Legalization 3. Details Placement

**Routing**

![F18_Routing](https://github.com/user-attachments/assets/c652af4b-8d8b-4a76-b46e-e39cfbca48a3)

The picorv32a design is represented by the green area in the above diagram. Whereas the red pads are for power, the blue pads are for ground. The pads provide power to the rectangular close-loop rings. The vertical lines that fasten to the rings are called power straps. The conventional cells' ground and power rails are secured by vertical straps. For proper power and ground connection, standard cells must be higher than the rail pitch. This diagram illustrates the power flow from the exterior to the pads, pads to rings, rings to strap/stripe, and strap/stripe to stdcell rows. Routing follows the same three-step process as placement. Nevertheless, the Global and Detail routing phases are slowed significantly by the TritonRoute tools.

**Global Route:** To quickly build a high-level routing solution, the global route creates a routing guide. Cell pins are represented by the boxes that make up the routing guide.

**Detail Route:** The detailed route uses the output of the global route, which includes the routing rules. Detailed routes are performed using TritonRoute. Algorithms are employed to identify the route point with the best overall connectivity.

**Lab 1 introduces with OpenLANE EDA tools:**

Useful Linux Command:

```
pwd: It displays the current working directory and its path.
cd: Using this command we can move in both ways in the directory tree.
ls: It lists all the sub-directories and files present in the current directory.
mkdir: Using this command, we can create a new directory.
rmdir: Using his command, we can delete an existing directory.
cp: For copying the file.
gedit: Open the file with a text editor (gedit).
help: Using this command we can know the working of any command.
clear: This command clears the terminal.
```
Libs file: The abbreviation for a Liberty Timing file is lib. An ASCII representation of the timing and power parameters linked to cells inside a specific technology node's standard cell library is called a LIB file. A lib file is essentially a timing model file that includes the cell's setup and hold time requirements, cell delay, and cell transition time. Therefore, the timing and electrical properties of a cell or macros are found in the lib file. If the foundry offers a standard cell library, the vendor or founder creates the lib file and sends it to the ASIC designer.

LEF file: Because it includes physical abstract information about layers and standard cells/macros, the Library Exchange Format (LEF) file is also known as a physical library. Because it is implemented in ASCII format, humans can read it. Foundries and library providers create these physical libraries. There are two kinds of physical libraries:

i) LEF technology
ii) Standard cell/macro LEF
Preparation of Design Step: Use the following command to launch bash while in the openalne directory:

`docker`

for the step-by-step openlane flow execution enter the following command

`./flow.tcl -interactive`

Now, we are in the Openlane. To input the required packages, use the following command:

`% package require openlane`

As there are various pre-built designs in the design’s subdirectory, we are choosing the "picorv32a.v" design on which we will implement the RTL to GDS flow. To carry out the synthesis of this design, we first need to set it up using the below command:

`prep -design picorv32a`

After preparation is complete, we can see a new directory with the latest date is created within the runs folder in picorv32a directory.

![2](https://github.com/user-attachments/assets/f860257d-fe5d-4c4a-b3cd-6da5035bbcc1)

`/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs`

![3](https://github.com/user-attachments/assets/6a82d895-c93d-4e04-995f-21201e5ead97)

To perform synthesis on the design, use the following command:

`run_synthesis`

The outcome of synthesis:

![4](https://github.com/user-attachments/assets/4b08cbce-0692-4d84-8582-7821252023b6)

![5](https://github.com/user-attachments/assets/23dac571-92fe-49e1-a3e0-17f42d67efa6)

From the synthesis we get- Number of D-Ff: 1613 Number of cells: 14876 Now, we can calculate the FF (Flip Flop) ratio and FF percentage from the data according to the formula:

Flip Flop Ratio (Number of D-FF) / (Total number of Cells). For FF percentage FF ratio * 100.
We get- FF ratio in our design is – 0.1084 And FF percentage is – 10.84%

For more information, look at the results directory in synthesis.

![6](https://github.com/user-attachments/assets/7ee041c2-d1d9-40ff-90d6-5e34a9c4abb6)

**Lab 2 Steps of run floorplan and placement using OpenLANE EDA tools**

To achieve an error-free floorplanning process, designers need to be aware of specific factors, referred to as switches, that might have a big influence on the floorplan. Aspect ratio and usage factor, for example, are two crucial choices. Before beginning the floorplanning phase, designers must confirm that these criteria meet the project requirements. The file README.md in the openlane configuration displays the different variables of the design flow. The path is shown below:

```
/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/configuration
```
![7](https://github.com/user-attachments/assets/a37c9832-de55-4d9a-ad74-5a4f33e27971)

The image shows different types of switches in floorplan stage after running floorplan.

```
run_floorplan
```

![10](https://github.com/user-attachments/assets/0b7d9c31-d696-4772-bd28-f218279feba3)


The image in the following section illustrates various types of switches involved in the floorplanning phase and their description.

![12](https://github.com/user-attachments/assets/4c6b2000-7065-4425-a0aa-3859c665289a)

The default value of these variables is set in the floorplan.tcl file of openlane configuration. The file path is the same as for README.md and is shown below:

![14](https://github.com/user-attachments/assets/f3def74e-fdac-4e3f-a8a9-0fe770bfc7ac)

n the figure above several floorplan variables are set by default. One important variable to mention here is FP_IO_MODE below:

```
set ::env(FP_IO_MODE) 1; # 0 matching mode - 1 random equidistant mode
```
which is set as '1' when IO pins are random equidistant.

Floorplan results After floorplan execution we go to the runs folder of picorv32a and open the latest date file name. Here one can check the implemented floorplan variables from the logs. The file name ioPlacer.log will give metal layers number for verical and horizontal IO pins. The path to the file is below:

![15](https://github.com/user-attachments/assets/16dabdfa-c4f0-41e2-875e-0ac192027bd8)

![16](https://github.com/user-attachments/assets/405016bf-cc3a-4d8d-b8e3-a2d0e6c73f6a)

Recall that the floorplan will have FP_IO_VMETAL 5 if FP_IO_VMETAL was set to 4, and the floorplan will have FP_IO_HMETAL 4 if FP_IO_HMETAL was set to 3.

![17](https://github.com/user-attachments/assets/d5487022-9aa5-4a13-807f-cbeb6bb490ed)

Layout view in Magic:

When the floorplaning is completed, to view the results go to the path as shown below:

![18](https://github.com/user-attachments/assets/fe2b94ca-5dc2-44a7-a470-7e77b01cf338)

open the design exchange file (.def): These results are useful. For example: we can see the die area:

![19](https://github.com/user-attachments/assets/2c7b0dc3-e345-4c02-b292-48df5eeeefcc)

Now, to open this ".def" file in magic, use the following command:

```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def
```

![21](https://github.com/user-attachments/assets/1fa5c536-a5d5-4380-8a51-d053b62fd32e)

Design Alignment Instructions:

Centering the design:
1. Press s to select the entire design
2. Press v to vertically align it to the middle of the screen.
Zooming In on a specific area:
1. Left click and drag to select the desired region.
2. Right-click to bring up the context menu.
3. Press Z to zoom in on the selected area.
Getting Details of a Cell:
1. Move your cursor to the cell of interest.
2. Press S to select the cell.
3. In the tkcon window, enter the command "what" to display cell details.

![Screenshot 2024-11-08 171805](https://github.com/user-attachments/assets/c3379c3d-d355-42b3-8876-18c35595f911)

![22](https://github.com/user-attachments/assets/45451704-a81b-42a6-85da-1eabfcd92c16)

![23](https://github.com/user-attachments/assets/377e2d0d-45d3-49e1-88ca-936a343acf66)

![24](https://github.com/user-attachments/assets/05c65418-894d-4407-85f8-eb65d6d790c1)

Placement To initiate the placement process, use the following command:
```
run_placement
```
During placement execution the reduction of half parameter wire length is the main focus. The placement is stop when the overflow is converged After the Placement is done. To view the results Go to the following location:
```
/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/10-08_13-18/results/placement
```
And then we can see 'picorv32a.placement.def' file. To open it using MAGIC use the following command:

```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def
```

![25](https://github.com/user-attachments/assets/1bc018e7-ecf3-44da-a69c-b649c4a18cda)

![26](https://github.com/user-attachments/assets/85a21f9a-4690-4f73-a870-ac176a2790af)


**Lab 3 demonstrates the complexities of fundamental logic gates through inverter characterisation using the Sky130 model files**

Modify while in the flow: Changing while in the open lane enables you to make adjustments without stopping the flow altogether. It is possible to change floorplan variables like IO mode and core utilization. For example, in order to change the layout's IO pin alignment, we must first make sure the pins are present. Go to the directory displayed in the picture below:

```
/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/10-08_13-18/results/floorplan
```

Then use the command to open the ‘.def' file in magic:

```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def
```
![27](https://github.com/user-attachments/assets/d16720db-175d-4b3a-9701-27e5a7c79d96)

Pins are spaced at random, as may be observed. IO Placer (an open-source EDA tool) supports four techniques. Now, open the floorplan and navigate to the following directory if you want it to switch to a different IO pin floorplan.tcl data:

![28](https://github.com/user-attachments/assets/2c0b5eaf-a649-4086-9497-8183a1abeca4)

From here we can see the switching variable FP_IO_MODE = 1, hence pins are randomly equidistant. Now, we run the following command and change the IO placer settings:

```
set ::env(FP_IO_MODE) 2
```
![29](https://github.com/user-attachments/assets/4e9476e0-a603-49ce-bd13-946a98af231d)

Now, we can check the change in the IO placer strategy: We can see that .def file has been updated from the time stamps and date:

![30](https://github.com/user-attachments/assets/f39fb406-75f6-4cf5-b40a-3eb51de954df)

Now, open it on magic

![31](https://github.com/user-attachments/assets/1c6c6ff6-f866-411c-88b2-bc43f24b0a53)

Clone ‘vsdstdcelldesign’ repo from git: The repository "vsdstdcelldesign" contains the .mag file for the inverter and spice models for sky130 nmos/pmos transistors. Git repo link:

```
git clone https://github.com/nickson-jose/vsdstdcelldesign.git
```

Now, open the sky130_inv.mag file in magic:

```
magic -T sky130A.tech sky130_inv.mag &
```
![33](https://github.com/user-attachments/assets/0922ad10-4fa5-4e71-af85-8a71f62502c9)

Sky130 INVERTER Basic Layout: The source, drain, gate, VDD, and ground terminals of the inverter opened in the magic tool are shown in Figure below. When polysilicon crosses the ndiffusion region it is termed as 'NMOS' and when it crosses the pdiffusion region it is termed as 'PMOS', the same is verified in the image below:

![WhatsApp Image 2024-11-08 at 22 17 13](https://github.com/user-attachments/assets/95dbce3c-8491-43ec-b29e-2d1958433dcc)

Create STD cell layout: Details to create a std cell layout have mentioned this website here- **(https://github.com/nickson-jose/vsdstdcelldesign?tab=readme-ov-file)**

Extract the spice netlist in Magic- In the tckon window, use the following command:

```
extract all
ext2spice cthresh 0 rthresh 0
ext2spice
```

![38](https://github.com/user-attachments/assets/4d0db55e-c749-4135-a008-f760a811e3c2)

Now let's open the extracted SPICE file of sky130A inverter:

![39](https://github.com/user-attachments/assets/e354d7a1-21f1-4862-ba7f-c8488e1ea376)

Final Spice Deck: Make the following changes in the 'sky130_inv.spic' file:

![40](https://github.com/user-attachments/assets/4b2324fa-12de-4b8c-9904-f76c0081fad9)

Now to simulate in ngspice, use the following command while in the 'vsdstdcelldesign' directory:

```
ngspice sky130_inv.spice
```
![43](https://github.com/user-attachments/assets/f0cfb4e4-4e30-429e-8a6f-dd9330d020d4)

Now, to open the plot use plot y vs time a in the ngspice terminal

![44](https://github.com/user-attachments/assets/d2c1a8b8-d231-4baf-b845-83d67617a071)

Characterization of inverter:

Rise Time: The time for the output waveforms to transition from 20% to 80% of its maximum value. From plot points: (x0 = 2.18192ns, y0 = 0.66049) to (x0 = 2.24571ns, y0 = 2.64018). Calculated Rise Time = 0.0634 ns
Fall Time: The time for the output waveform to transition from 80% to 20% of its maximum value. From plot points: (x0 = 4.0525ns, y0 = 2.63976) to (x0 = 4.09516ns, y0 = 0.659249). Calculated Fall Time = 0.0422 ns
Propagation Delay (Cell Rise Delay): The time for the output to transition 50% in response to a 50% change in the input. From plot points: Input (x0 = 2.15018ns, y0 = 1.65018) to Output (x0 = 2.21088ns, y0 = 1.65). Calculated Propagation Delay = 0.064 ns
Cell Fall Delay: The delay for the output to transition 50% due to a 50% change at the input. From plot points: (x0 = 4.04997ns, y0 = 1.65) to (x0 = 4.07748ns, y0 = 1.65). Calculated Cell Fall Delay = 0.0277 ns.

DRC Rules: The details about the MAGIC tool and its DRC rules can be seen **http://opencircuitdesign.com/magic/**

We use the following command to download the Lab files used in this tutorial. The current location should be the home directory:

```
sudo wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
```
Once downloaded the zip file we extracted.

![45](https://github.com/user-attachments/assets/190d32ee-58e3-4ff0-a02c-957774f882e3)

Introduction to Magic & Steps to load sky130 tech-rules: Run the command magic -d XR to open the Magic tool. Now open the met3.mag file in magic.

![47](https://github.com/user-attachments/assets/813ecbbd-8331-4da5-80da-8a6d427d4021)

Fixing the error (Poly.9)

![48](https://github.com/user-attachments/assets/8fc5b2e1-1ea1-44e4-8ff7-930240cf8236)

Using the "box" command, measure the distance between the poly resistor and poly when you zoom in on the "Incorrect poly.p" layout. The measurement indicates a 0.210 µm spacing, which is less than the 0.480 µm "poly.9" DRC rule. However, there is no DRC mistake. Now let's fix this issue

![Screenshot 2024-11-08 225535](https://github.com/user-attachments/assets/3584d64e-9eea-413f-80fc-4a5a4c5ecc4a)


![Screenshot 2024-11-08 225641](https://github.com/user-attachments/assets/f2cfc294-79b5-49c6-94b5-8f2fec0b3116)


![Screenshot 2024-11-08 225722](https://github.com/user-attachments/assets/24ad7eeb-bad2-4af8-ac27-1c031b3fe100)


Go to the drc_tests directory and open the Sky130a.tech file. Look up "poly.9" and make the adjustments depicted in the following pictures. Once the changes are made, save the file.


![50](https://github.com/user-attachments/assets/17944646-bbf2-40f9-ab93-9551aa56b748)


Reload the sky130A.tech file and re-run the DRC check by running the following commands in tkcon.


![Screenshot 2024-11-08 230323](https://github.com/user-attachments/assets/496b4644-1adf-4cb1-bdcc-48d388ff19c3)


**Lab 4 Pre-layout timing analysis & emphasizes the significance of a well-designed clock tree**

Commands to open the custom inverter layout

```
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
magic -T sky130A.tech sky130_inv.mag &
```
Command for tkcon window:

```
help grid
grid 0.46um 0.34um 0.23um 0.17um
```
![52](https://github.com/user-attachments/assets/c56f3f97-ff38-4180-99b3-a99b2226abdd)

The whole li1 layer is on the grid layer. The locations of the input and output ports are where the vertical and horizontal tracks converge. This fulfills the first requirement.

![53](https://github.com/user-attachments/assets/f9b7423b-3dfb-449b-803b-a04b8d4664a9)

Additionally, we can observe that the standard cell's width equals the three grid/track boxes. As previously stated, the height and breadth of the standard cell should both be odd multiples of the vertical track pitch and the horizontal track pitch. This fulfills the second requirement.

![Screenshot 2024-11-08 231207](https://github.com/user-attachments/assets/20eec447-ca7e-4175-852f-329c978f714b)

Open the complete layout after saving it with a unique name.

```
save sky130_cinv.mag
```
![54](https://github.com/user-attachments/assets/3ea716d6-d6eb-45b3-8756-692816f5c442)

Generate lef from the layout by command.

```
lef write
Let’s open the LEF file
```

![55](https://github.com/user-attachments/assets/43d43f17-072f-4dfa-b376-f0a8cd14d768)

Next, we plug in the LEF file in the picorv32a design. Introduction to timing libs and steps to include new cells in the synthesis: The Synthesis, Placement, and Route phases are now repeated. Our unique cell is added to the picorv32a Openlane Design Flow for this purpose. We ensure that the PWD we have is

```
/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign. From here, we copy the .lef file using the following commands:
```
```
cp sky130_vsdinv.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src
```
For the synthesis step, we need the std cell library files. Therefore we copy the .lib files from the directory vsdstdcelldesign/libs using the following commands:

```
cp sky130_fd_sc_hd__* /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src
```

Every standard cell's characterisation data (cell power, cell increase, cell transition, etc.) is contained in the.lib file. Different speeds, temperatures, and voltage values are described for the files sky130_fd_sc_hd__typical.lib, sky130_fd_sc_hd_fast.lib, and sky130_fd_sc_hd__slow.lib. The nmos/pmos transistors in sky130_fd_sc_hd__typical.lib are described at a temperature of 25°C and a voltage of 1.8 volts, meaning they are neither fast nor slow. Our customized cell will be added to all of the typical, slow, and fast libraries.

![56](https://github.com/user-attachments/assets/baf45bc6-c915-496d-98a5-0315e35a3cc3)

![57](https://github.com/user-attachments/assets/5461bf6b-fafd-4d0c-bf60-3595ec5f16eb)

![58](https://github.com/user-attachments/assets/bf0f9363-42e0-4e23-9038-e83353f3ecbf)

Now, we need to modify the config.tcl file: Go to the picorv32a directory and open the file using gedit and we make the following modifications:

![59](https://github.com/user-attachments/assets/9b5b1ce3-fffb-4c1f-b9a6-5f9290ec5be9)

![60](https://github.com/user-attachments/assets/fdde7e02-1181-4a2f-b545-b28faa7abcf7)

Now, launch the docker following the standard procedures as indicated, and include some commands:

```
./flow.tcl -interactive
package require openlane 0.9
#to continue the work in the already made directory in the runs folder
prep -design picorv32a -tag  18-08_15-37 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```
![61](https://github.com/user-attachments/assets/de1bb0c1-72ad-4cbd-ac38-77eacbba7f93)

Now run synthesis by command

```
run_synthesis
```
![63](https://github.com/user-attachments/assets/f0c19312-1d45-4f94-96e0-fb9a7f463c5a)

It is evident from the preceding image that synthesis was effective. 1554 instances of our cinverter are utilized in total. Additionally, we can observe that the overall negative slack is -711.59 and the worst slack is -23.89. 147712.918 is the chip area. At this point, we can attempt a timing-driven synthesis to reduce the slack. To improve the delay, we must trade off the chip area for this. We opened the README.md from the directory and saw the variable ‘SYNTH STRATEGY’ ‘SYNTH BUFFERING’ ‘SYNTH SIZING’ ‘SYNTH DRIVING CELL’. Change the variable to reduce the slack.

```
# Now once again we have to prep the design to update the variables
prep -design picorv32a -tag 18-08_15-37  -overwrite
# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
# Command to display the current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)
# Command to set a new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"
# Command to display the current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)
# Command to display the current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)
# Command to set a new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1
# Command to display the current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)
# Now that the design is prepped and ready, we can run synthesis using the following command
run_synthesis
```
![62](https://github.com/user-attachments/assets/896a60f7-b3ef-47a5-8970-58e7627baf68)

![64](https://github.com/user-attachments/assets/4ac58d96-e712-4549-b3a4-eb8447c49c03)

![65](https://github.com/user-attachments/assets/7f677c62-0053-47eb-920f-24b29a29a10a)

![66](https://github.com/user-attachments/assets/3a4d1b75-3b22-413b-8909-6b3f28f66fa1)

Now that the synthesis phase is over, we use the following command to finish the floorplan:

```
init_floorplan
place_io
tap_decap_or
```

![67](https://github.com/user-attachments/assets/92023749-0857-448b-9b7e-28a476c1b76c)

After finishing the floorplan stage, we run placement

```
run_placement
```

![68](https://github.com/user-attachments/assets/4c0929ba-ca2c-4f22-8782-2a67db38d20a)

![69](https://github.com/user-attachments/assets/a6a1cb75-5bd8-41d5-a6bb-f8caab67a62b)

Now we can see our slack problem is solved. Now, to verify if the standard cell we generated was incorporated into the design or not by magic

```
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
![70](https://github.com/user-attachments/assets/cb0ed853-6a23-406a-a139-f76e4a8075b0)

Timing analysis with ideal clocks using openSTA: Let's create an STA conf file (pre_sta.config) first in the directory /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane. In this file, we provide the fast and slow corner lib file, an old Verilog file, and an SDC file. After STA a new Verilog file is created. The file is shown below:

![71](https://github.com/user-attachments/assets/d6d603c1-1430-44a5-abe1-4eed0e20d5a1)

my_sdc in the directory sky130_cinv.lef

```
/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src

```
![72](https://github.com/user-attachments/assets/e3bc8ea2-1a16-47ce-9d62-349e8083db73)


now run the static timing analysis using the following command

```
sta pre_sta.config
```
![74](https://github.com/user-attachments/assets/f30b8fd2-63c8-4200-a4c9-4072fbfdb7a0)

Slack does not equal what we obtained during the synthesis stage, as can be seen. Still, we move forward with the CTS and routing.

CTS: TritonCTS is the EDA tool that generates CTS. This tool so far generates the CTS for typical corners of std cells.

![Screenshot 2024-11-08 234944](https://github.com/user-attachments/assets/d694b0cb-c7b6-4f7b-b55c-cdd8bf8ee727)


This will swap out the outdated layout for the optimized one. After the update is finished, use the same instructions to go on to the Floorplan stage.

```
init_floorplan
place_io
tap_decap_or
```

Following the Floorplan's successful completion, we use the following instructions to go on to the placement step: run_placement


![Screenshot 2024-11-09 105757](https://github.com/user-attachments/assets/8355937f-a096-4b97-9bd6-c31ee004ab79)

![Screenshot 2024-11-09 105846](https://github.com/user-attachments/assets/ee397963-c30e-42a5-88b6-bf799657e4ba)


```
run_cts
```

![78](https://github.com/user-attachments/assets/20253fed-4b3b-4373-8dc9-8d5750cbfa70)

The clock buffers are inserted at the cts stage, changing the netlist. We can see that a new.cts file has been created to the synthesis results directory once the cts has finished. Both the prior netlist and the clock buffers created during the CTS stage are contained in the recently added CTS file.

![79](https://github.com/user-attachments/assets/03aa6677-fea1-414c-9bfc-5d1f140de066)

Timing Analysis with real clocks: Open openroad tools by command-

```
openroad
```
We first generate the database (made from lef and def files) in openroad for time analysis. Execute the subsequent commands:


![81](https://github.com/user-attachments/assets/8f95d266-c75b-476b-83d6-212b3ccc1cd1)

```
read_def /openLANE_flow/designs/picorv32a/runs/18-08_15-37/results/cts/picorv32a.cts.def
```

![Screenshot 2024-11-09 111308](https://github.com/user-attachments/assets/688170f8-ee5e-4952-a5e7-b4ab8b64c39b)


```
write_db pico_cts.db
```

![82](https://github.com/user-attachments/assets/34b28e78-92f9-4cab-b9ec-7413c7b37132)

```
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/18-08_15-37/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -format full_clock_expanded -digits 4
```

![Screenshot 2024-11-09 113155](https://github.com/user-attachments/assets/45ee5335-c657-4c1b-a7ef-628212b56128)

The slack in the setup time is satisfied

![83](https://github.com/user-attachments/assets/a52906af-7a6b-4038-9136-e83065b4b12a)

Layers of metal are placed during routing. As a result, the arrival time will rise and we can lower the slack for hold time, but it will decrease for setup time due to the inclusion of the metals' capacitance and resistance. Now, use exit to exit from the openroad. Check the current buffer used in the CTS netlist by commanding:

```
echo $::env(CTS_CLK_BUFFER_LIST)
```
![84](https://github.com/user-attachments/assets/8286e0e9-0c01-4111-891f-cb27e1b25193)

Now remove the clkbuf_1 from the list:

set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]

run_cts again. It was fail to load, then we use

```
top
kill -9 [problem id]
```
This is because, as the figure below illustrates, the current DEF value is incorrect. We must utilize the DEF value for placement because buffer 1 has been eliminated; however, following CTS, the DEF value was modified to the CTS DEF value. set def as placement def

```
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/18-08_15-37/results/placement/picorv32a.placement.def
```
![Screenshot 2024-11-09 114012](https://github.com/user-attachments/assets/d641a242-8b6a-48f1-8a2b-517d7affccdd)

Openlane inserts buffers from left to right and verifies the skew value while constructing the CTS in an attempt to satisfy the skew value. Within the first 10% of the clock period, the skew value is found.

![Screenshot 2024-11-09 114215](https://github.com/user-attachments/assets/39f6aab8-5220-4956-9831-41720ad695d5)

![Screenshot 2024-11-09 114258](https://github.com/user-attachments/assets/8ec127d8-614f-484f-a673-51806bb67327)


We now must take the same actions as we did previously on the openroad. visit openroad periodically:

```
read_lef /openLANE_flow/designs/picorv32a/runs/18-08_15-37/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/18-08_15-37/results/cts/picorv32a.cts.def
write_db pico_cts1.db
read_db pico_cts1.db
read_verilog /openLANE_flow/designs/picorv32a/runs/18-08_15-37/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
```

![Screenshot 2024-11-09 114500](https://github.com/user-attachments/assets/d7cecea4-7093-4832-92dc-fb5d860fb7eb)

![Screenshot 2024-11-09 114546](https://github.com/user-attachments/assets/e3165af2-7a8e-47bb-8b51-acdae891bbc0)

```
report_clock_skew -hold
report_clock_skew -setup
```



**Lab 5: Final Steps to generate GDSII**

Before starting routing, we can create a power distribution network (PDN) after CTS is available. Let's use the following commands to examine our DEF file as it is now.

```
echo $::env(CURRENT_DEF)
```
![Screenshot 2024-11-09 114822](https://github.com/user-attachments/assets/5ea1ed19-9b08-42a7-81b9-bc4a4d3a270a)

```
gen_pdn
```

![Screenshot 2024-11-09 114949](https://github.com/user-attachments/assets/3d7091d4-9e1a-480d-8227-55b51d2164cd)

The PDN output seen above demonstrates how PDN generates the grid and ground straps in addition to writing the LEF file and reading the CTS DEF. Since STD cells are positioned in STD rows as is well known, STD cell power rails are positioned along the rows of STD cells. The height of the stdcell inverter is equal to the pitch of the std cell rails, which is 2.720. As a result, the GND and PWR ports of the standard cell inverter match the power and ground standard cell rails. Run the following command for routing:

```
run_routing
```

![Screenshot 2024-11-09 115117](https://github.com/user-attachments/assets/a1387a91-a9d7-4091-8e4c-e7df5523eba6)

Open with magic:

![Screenshot 2024-11-09 115223](https://github.com/user-attachments/assets/c6a7e7da-93f4-4407-855a-f9f24c942836)


![Screenshot 2024-11-09 115300](https://github.com/user-attachments/assets/00bde9c6-40f8-4991-b8c8-3719ad40dd86)

Acknowledgements
**https://github.com/efabless/openlane2**
**https://github.com/nickson-jose/vsdstdcelldesign**
**https://skywater-pdk.readthedocs.io/en/main/index.html**
https://www.vlsisystemdesign.com/nasscom-positions-vsd-at-the-forefront-of-vlsi-skilling-initiatives-in-india/







































































































