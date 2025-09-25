# TIMING LIBS, HIERARCHIAL Vs FLAT SYNTHESIS AND EFFICIENT FLOP CODING STYLES

## Library sky130_fd_sc_hd__tt_025c_1v80
- The SkyWater SKY130 PDK provides an open-source standard cell library for digital design.
- Library Name: sky130_fd_sc_hd__tt_025c_1v80.lib
- Meaning:
  * sky130 → 130nm cells
  * fd_sc_hd → foundry, standard cells, high-density variant
  * tt → Typical process corner (variations in manufacturing process like Process, Voltage, Temperature)
  * 025c → Operating temperature (25 °C)
  * 1v80 → Supply voltage (1.8 V)
- Use:
  - Provides timing, power and area information for synthesis, placement and routing.
  - It is essential for technology mapping in Yosys and other digital design tools.

## Hierarchical Synthesis using Yosys
Hierarchical synthesis preserves the design hierarchy during synthesis.
- Each Verilog module is synthesized independently.
- The hierarchy is maintained, enabling modular verification and reusability.
- Useful when working on large SoC projects or when modules need to be optimized separately.
```bash
yosys> read_verilog design_file.v
yosys> synth -top top_module
yosys> abc -liberty ../lib/sky130_fd_sc_hd__tt_025c_1v80.lib
yosys> write_verilog -noattr module_hier.v
```
<img width="1328" height="797" alt="d2_mul_mod_hier" src="https://github.com/user-attachments/assets/cc6c9937-04cd-426b-8d5f-60c4e95743e7" />
<img width="842" height="383" alt="d2_mul_mod_heir1" src="https://github.com/user-attachments/assets/8b0d299b-78b3-4929-83b3-6c171e4cb9d1" />
<img width="1850" height="895" alt="d2_mul_mod" src="https://github.com/user-attachments/assets/da31d6d4-3142-4d91-b2bc-c336e2d27bd0" />

## Flat Synthesis using Yosys
Flat synthesis flattens the entire design into a single-level netlist.
- Eliminates module boundaries.
- Enables global optimizations across the design.
- May increase synthesis runtime and memory usage, but results in better performance and area optimization.
```bash
yosys> read_verilog top.v
yosys> synth -top top_module
yosys> flatten
yosys> abc -liberty ../lib/sky130_fd_sc_hd__tt_025c_1v80.lib
yosys> write_verilog -noattr module_hier.v
```
<img width="1850" height="895" alt="d2_mul_mod_hierflat" src="https://github.com/user-attachments/assets/fe4f30ec-8f2b-48bf-b3f3-a56846ebd12d" />

## Multiple Module Verilog Design File
A typical design may contain multiple Verilog modules in a single file.
- The top module instantiates sub-modules.
- Helps in structured design and code reuse.
<img width="1850" height="895" alt="d2_mul_mod_code" src="https://github.com/user-attachments/assets/3053ce31-eda6-4b6e-95b4-b82c7773e199" />
<img width="1850" height="895" alt="d2_mul_mod hier" src="https://github.com/user-attachments/assets/eef92664-9b31-4272-ab47-29963c733e0b" />

## Module-Level Synthesis in Yosys
Module-level synthesis allows targeting a specific module for synthesis instead of the full design.
- Useful for debugging and incremental synthesis.
- Helps reduce runtime when working on complex designs.
<img width="1850" height="895" alt="d2_mul_mod_submod" src="https://github.com/user-attachments/assets/eece0220-f1e1-45fe-a5a3-fbdb8e4d29d8" />

## Why Flops?
Flip-flops (flops) are the fundamental storage elements in digital circuits.
- They store state information between clock cycles.
- Essential for sequential logic (FSMs, counters, pipelines).
- Enable synchronous design methodology, ensuring predictable timing and reliable operation.
Without flops, digital designs would be purely combinational, lacking memory or sequential behavior.

## D Flip-Flop
A D Flip-Flop stores one bit of data at each clock edge.
- Synchronous Reset/Set:
  - Reset/Set action occurs only on a clock edge.
  - Timing predictable, better for synthesis.
- Asynchronous Reset/Set:
  - Reset/Set action occurs immediately, independent of the clock.
  - Useful for initialization, but may cause timing hazards if not handled carefully.
<img width="1850" height="895" alt="d2_dff_asynres" src="https://github.com/user-attachments/assets/c373acb4-3436-4434-b3b3-459d7c2af6aa" />
<img width="1850" height="895" alt="d2_dff asyn rest" src="https://github.com/user-attachments/assets/4e01ad77-561a-4dfe-959e-f68d0340e52c" />
<img width="1850" height="895" alt="d2_dff_asynset" src="https://github.com/user-attachments/assets/39f8231e-ca6e-4548-b656-cfe4dc7bd432" />
<img width="1850" height="895" alt="d2_dff_asyn set" src="https://github.com/user-attachments/assets/05e84d0b-c9a9-48f1-92a3-0bc3cbbd5274" />

## Optimization
Optimization in digital design refers to improving area, power, and timing without altering functionality.
- Logic Optimization: Removing redundant gates, constant propagation.
- Technology Mapping: Mapping logic to efficient standard cells.
- Sequential Optimization: Retiming, clock gating.
<img width="1265" height="306" alt="d2_mul 2" src="https://github.com/user-attachments/assets/7fdd2948-83e0-4b3d-8b05-f5b2ae962758" />
<img width="1850" height="895" alt="d2_mult 2" src="https://github.com/user-attachments/assets/a87b54db-312b-4e55-8348-727d0256a8d1" />
<img width="1273" height="284" alt="d2_mul 8" src="https://github.com/user-attachments/assets/ab7db59a-09a9-4ada-8777-0c31b7b983b7" />
<img width="1848" height="920" alt="d2_mult 8" src="https://github.com/user-attachments/assets/212dcf8f-29be-4c13-bf92-5ae0fbf6fdb4" />
