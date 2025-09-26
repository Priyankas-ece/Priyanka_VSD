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

## Why GLS?
Gate-Level Simulation is required because synthesis tools may introduce changes not present in the original RTL.
- Validation after synthesis: Ensures synthesized netlist matches RTL behavior.
- Check for issues:
    - Uninitialized signals
    - X-propagation problems
    - Clock/reset glitches
- Timing verification: With SDF back-annotation, designers can check timing violations.
- Confidence before tape-out: Helps confirm that the design works correctly in terms of functionality and timing before physical design.
- In short, GLS provides an extra layer of functional and timing assurance beyond RTL simulation.

## Synthesis and Simulation Mismatch
A synthesis-simulation mismatch occurs when the behavior of the RTL during simulation does not match the behavior of the synthesized gate-level netlist.
Causes:
- Coding style issues:
  * Using blocking assignments (=) instead of non-blocking (<=) in sequential logic.
  * Incomplete sensitivity lists in combinational always blocks.
  * Inferring latches unintentionally.
- Reset/initialization differences: Some synthesis tools ignore initial blocks.
- Uninitialized registers: RTL sim may work with X → 0, but GLS keeps X as unknown.
- Tool-specific optimizations: Logic may be simplified differently in synthesis.
Prevention/Best Practices:
- Use proper RTL coding guidelines (non-blocking for sequential, complete sensitivity lists).
- Always reset registers properly.
- Avoid simulation-only constructs (e.g., #delay, $random) in synthesizable code.
- Run GLS with the same testbench used for RTL to detect mismatches early.

