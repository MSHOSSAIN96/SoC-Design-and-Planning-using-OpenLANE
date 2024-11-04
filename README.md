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









