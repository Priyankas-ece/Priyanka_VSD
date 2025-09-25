# GLS, BLOCKING Vs NON-BLOCKING AND SYNTHESIS-STIMULATION MISMATCH

## Gate-Level Simulation (GLS)
Gate-Level Simulation (GLS) is the process of simulating the synthesized gate-level netlist instead of the RTL design.
- The netlist is generated after synthesis, mapped to standard cells from the target library (e.g., sky130_fd_sc_hd__tt_025c_1v80).
- GLS includes timing information (delays from the library) if Standard Delay Format (SDF) is back-annotated.
- Used to validate:
    - Correct functionality after synthesis.
    - Effects of timing, setup, and hold.
    - Reset and initialization conditions.
- Typical Flow:
    1. Write RTL design in Verilog.
    2. Perform synthesis (using Yosys or other tools).
    3. Generate gate-level netlist mapped to standard cells.
    4. Run simulation on the netlist using the same testbench.
    5. Compare results with RTL simulation.
