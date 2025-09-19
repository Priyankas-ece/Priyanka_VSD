# Week 0 — Digital VLSI SoC Design and Planning

## Overview
The video explains the complete flow of designing a processor, starting from code specification, moving through RTL, synthesis, physical design, SoC integration, and ending with verification and tape-out.

## About SoC (System-on-Chip)
- Combines **processor core + memory elements + peripherals** (e.g., UART, SPI, GPIO).  
- Peripherals can include **macros** (synthesizable RTL) and **analog IP** (functional RTL).  
- SoC enables integration of millions of transistors on a single die.  
- Benefits: smaller physical size, reduced power, lower cost, improved performance.  
- Examples: smartphones, tablets, laptops.  

## Flow of Work
**Specs → RTL design → Processor → Peripherals → SoC Integration**
- Specifications define functional requirements.  
- RTL development for processor core.  
- Add peripherals (timers, GPIO, UART).  
- Integrate into SoC bus/interconnect.  
- Verify at each level with test benches.  

## Key Takeaways
1. Processor design follows a structured flow: **specifications → RTL → synthesis → GDS → tape-out**.  
2. SoC integrates processor cores with peripherals to form a complete system.  
3. Verification is critical at every stage:  
   - Specs vs. RTL design  
   - SoC integration vs. RTL  
   - Final chip vs. SoC  

<img width="361" height="285" alt="soc_w1 drawio" src="https://github.com/user-attachments/assets/5f401d0b-64c7-4634-94de-8fcbf6907dca" />
