# SoC-Design-and-Planning-using-OpenLANE
A project based on an ASIC design's entire RTL to GDSII flow. RISC-V design (picorv32a) + open-process (google+skywater130nm) + open-lane EDA tools (efabless) are now all open-source. 
Beginning with fundamental ideas and moving through useful labs, this project provides a thorough exploration of the ASIC design process using OpenLANE and Sky130. It is constructed with open-source libraries and industry-standard EDA tools, giving users practical experience with IC design.

**Scope of work:**

I make sure users are prepared to follow the structured roadmap by outlining the prerequisites and installation procedures before they begin. The first element of the project, Theory, covers the basics of IC design, including nomenclature, components, and an outline of what distinguishes a good floorplan from a bad one. In this part, placement basics and library cells are also covered.

I explore the methods and factors needed for efficient signal routing in IC designs in the Routing section. A number of labs are included in the project to foster familiarity and practical skills.

In order to help users become accustomed to the environment, 
Lab 1 introduces them to the OpenLANE EDA tools.

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

****Lab 1 introduces with OpenLANE EDA tools:

Useful Linux Command:

```pwd: It displays the current working directory and its path.
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


























