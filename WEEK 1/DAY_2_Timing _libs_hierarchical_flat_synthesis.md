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
