
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
The objective of this project is to design, simulate, and layout a 6T SRAM bitcell using Cadence Virtuoso, and analyze its static noise margin, read/write functionality, and power dissipation and post-layout verification.

### **Tools & Technology**
- **Cadence Virtuoso** – Schematic design, simulation, and layout.  
- **Spectre Simulator** – DC and transient analyses.  
- **180nm CMOS PDK** – For transistor-level implementation.  

## **Project Workflow**

### 1. Schematic Design
- Designed a 6T SRAM bitcell schematic using CMOS transistors.  
- Created a **Symbol** for easy instantiation in higher-level designs (memory design).  
- Transistor sizing chosen to balance read stability, write ability, and area efficiency. 

*Schematic*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/Schematic.png?raw=true)

*Symbol*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/SRAM%20bitcell%20symbol.png?raw=true)

### 2. DC Analysis
- Performed butterfly curve analysis to extract Static Noise Margin (SNM).  
- Evaluated hold SNM and read SNM for cell stability.  

*Parameter Sweep - Q*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/DC%20Analysis-1.png?raw=true)

*Butterfly curve (Q v/s Qbar)*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/DC%20Analysis-2.png?raw=true)

*ADE L window*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/DC%20Analysis-3.png?raw=true)

### 3. Transient Analysis
- Verified Read/Write ‘0’ and ‘1’ operations.  
- Analyzed bitline behavior and wordline timing.  

*Read ‘0’*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/Read%200.png?raw=true)

*Read ‘1’*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/Read%201.png?raw=true)

### 4. Power Analysis
- Performed DC sweep to analyze static power dissipation across different logic states of the SRAM bitcell."
- Measured peak-to-peak variation in static power consumption using Virtuoso calculator.

*Power signal plot*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/Power.png?raw=true)

*Peak-to-Peak Power*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/Power%20(Peak%20to%20Peak).png?raw=true)

### 5. Layout Design
- Designed a compact layout of the 6T SRAM bitcell in Virtuoso Layout Editor.  
- Transistor placement optimized for symmetry and matching.  
- Routing done for bitlines, wordline, and power rails (VDD, GND).

*Layout*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/Layout.png?raw=true)

### 6. DRC and LVS Verification
- **DRC (Design Rule Check)** performed → No violations found.  
- **LVS (Layout vs Schematic)** → Netlists successfully matched.  

*DRC and LVS report screenshots*

*(1)*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/DRC-1.png?raw=true)

*(2)*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/DRC-2.png?raw=true)

*(3)*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/LVS-1.png?raw=true)

*(4)*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/LVS-2.png?raw=true)


### 7. RC Extraction & Post-Layout Simulation
- Extracted parasitics from layout using RC Extraction.  
- Generated **extracted layout view**.  
- Ensured functional verification matches schematic-level results.  

*Layout (after extraction)*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/Layout%20(after%20extration).png?raw=true)

*DRC and LVS report (after extraction) screenshots*

*(1)*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/DRC_LVS%20(after%20extraction)-1.png?raw=true)

*(2)*
![App Screenshot](https://github.com/itsharshschoice/Design-and-Layout-of-a-6T-SRAM-Bitcell/blob/main/Screenshots/DRC_LVS%20(after%20extraction)-2.png?raw=true)

## **Results**
- **Butterfly curve** obtained → SNM successfully calculated.  
- **Read ‘0’ and Read ‘1’ operations** verified.  
- **Write ‘0’ and Write ‘1’ operations** verified.  
- **Power dissipation** analyzed (peak-to-peak).  
- **Layout designed and verified** through DRC and LVS.  
- **Post-layout extracted view** created and validated.  

## **Learning Outcomes**
- Understood the internal working of SRAM bitcells at transistor level.  
- Learned to perform DC and transient simulations for memory circuits.  
- Learned layout design flow with DRC, LVS, and RC extraction.  
- Acquired hands-on experience with Cadence Virtuoso and Spectre simulations.

## **Conclusion**

In this project, a complete **6T SRAM bitcell** was designed and verified in Cadence Virtuoso. The work included schematic design, symbol creation, DC analysis for SNM, transient simulations for read and write operations, and power dissipation analysis. A compact layout was implemented, followed by DRC and LVS verification, and RC extraction to generate an extracted view. The results confirm correct operation of the SRAM bitcell both at schematic and layout levels.

This 6T SRAM bitcell can be used as a fundamental building block for designing larger memory circuits, such as cache memory, register files, and on-chip buffers in processors.



