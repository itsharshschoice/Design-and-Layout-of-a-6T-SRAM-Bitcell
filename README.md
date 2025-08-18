
# **Design and Layout of a 6T SRAM Bitcell**

## **Introduction**

Static Random Access Memory (SRAM) is one of the most widely used memory technologies in VLSI systems, especially in caches, register files, and high-speed memory structures. Unlike DRAM, which requires periodic refreshing, SRAM retains its data as long as power is supplied.  

At the heart of every SRAM array lies the SRAM bitcell, the fundamental building block responsible for storing a single bit of information (`0` or `1`). Among different architectures, the 6-Transistor (6T) SRAM bitcell is the industry standard due to its balance between density, stability, performance, and power**.


## **Overview of 6T SRAM Bitcell**

A 6T SRAM cell consists of:
- Two cross-coupled CMOS inverters → form a bistable latch to hold data (`0` or `1`).
- Two NMOS access transistors → provide controlled access to the latch during read and write operations.

![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/6T-SRAM-Bitcell.png?raw=true)

### **Circuit Composition**
- **PMOS Transistors (M3, M4):** Pull-up devices of the cross-coupled inverters.  
- **NMOS Transistors (M1, M2):** Pull-down devices of the cross-coupled inverters.  
- **Access Transistors (M5, M6):** Connect internal nodes of the latch to the bitlines (BL, BLB) when wordline (WL) is enabled.  


## **SRAM Bitcell Operations**

### **Hold Operation**
- When Word Line (WL) = 0, the access transistors are OFF.  
- The cross-coupled inverters reinforce each other, maintaining the stored data indefinitely as long as VDD is present.  

### **Read Operation**
- WL = 1, enabling the access transistors.  
- Suppose the cell stores `Q = 0`, `QB = 1`.  
  - `BL` discharges slightly through the pull-down NMOS → sensed as `0`.  
  - `BLB` remains high → sensed as `1`.  
- A critical design metric here is Read Static Noise Margin (Read SNM). If the cell is weakly designed, a read disturb may flip the stored value.  

### **Write Operation**
- WL = 1, enabling access.  
- To write a `0`:  
  - Force `BL = 0` and `BLB = 1`.  
  - This overpowers the existing state and flips the latch.  
- To write a `1`:  
  - Force `BL = 1` and `BLB = 0`.  
- Successful writing requires the write driver strength to dominate the cell’s feedback inverters.  

## **Project Description**

### **Objective**
The objective of this project is to design, simulate, and layout a 6T SRAM bitcell using Cadence Virtuoso, and analyze its static noise margin, read/write functionality, and power dissipation.

### **Tools & Technology**
- **Cadence Virtuoso** – Schematic design, simulation, and layout.  
- **Spectre Simulator** – DC and transient analyses.  
- **180nm CMOS PDK** – For transistor-level implementation.  

## **Project Workflow**

### 1. Schematic Design
- Created a 6T SRAM bitcell schematic using CMOS transistors.  
- Transistor sizing chosen to balance read stability, write ability, and area efficiency. 

![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/Schematic.png?raw=true)

### 2. DC Analysis
- Performed butterfly curve analysis to extract Static Noise Margin (SNM).  
- Evaluated hold SNM and read SNM for cell stability.  

![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/DC%20analysis(1).png?raw=true)

Butterfly curve:
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/DC%20analysis(2).png?raw=true)

### 3. Transient Analysis
- Verified Read ‘0’ and Read ‘1’ operations.  
- Analyzed bitline behavior and wordline timing.  
- (To be completed) Write ‘0’ and Write ‘1’ operations will be simulated to check write margins.  

Read ‘0’:
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/Read%200.png?raw=true)

Read ‘1’:
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/Read%201.png?raw=true)

### 4. Power Analysis
- Used power peak-to-peak measurement to calculate power dissipation during read and write cycles.   

![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/Power.png?raw=true)

peak to peak power:
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/Power%20(peak%20to%20peak).png?raw=true)

### 5. Layout Design
- Designed a compact layout of the 6T SRAM bitcell in Cadence Virtuoso Layout Editor.  
- Placement of NMOS and PMOS transistors optimized for area and symmetry.  
- Routing done for bitlines, wordline, and supply rails.  
- (Pending) LVS and DRC checks will be performed for validation.

## **Results (So Far)**
- **Butterfly curve obtained** → SNM calculated.  
- **Read ‘0’ and Read ‘1’ operations** verified.  
- **Power dissipation (peak-to-peak)** analyzed.  
- **Write operations** under simulation.  
- **Layout LVS verification** to be completed.  

## **Learning Outcomes**
- Understood the internal working of SRAM bitcells at transistor level.  
- Learned to perform DC and transient simulations for memory circuits.  
- Explored power-performance trade-offs in memory design.  
- Gained hands-on experience in schematic design, analysis, and layout in Cadence Virtuoso.

## **Conclusion**

In this project, a 6T SRAM bitcell was designed and analyzed in Cadence Virtuoso. The work included schematic design, DC analysis using butterfly curves for SNM calculation, transient simulations for read operations, and power dissipation measurement. The layout of the bitcell was also implemented, with LVS verification planned as the next step.



