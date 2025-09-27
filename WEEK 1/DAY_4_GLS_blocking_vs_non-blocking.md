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
  * Incomplete sensitivity lists in combinational always blocks.
  * Using blocking assignments (=) instead of non-blocking (<=) in sequential logic.
  * Inferring latches unintentionally.
- Reset/initialization differences: Some synthesis tools ignore initial blocks.
- Uninitialized registers: RTL sim may work with X → 0, but GLS keeps X as unknown.
- Tool-specific optimizations: Logic may be simplified differently in synthesis.
Prevention/Best Practices:
- Use proper RTL coding guidelines (non-blocking for sequential, complete sensitivity lists).
- Always reset registers properly.
- Avoid simulation-only constructs (e.g., #delay, $random) in synthesizable code.
- Run GLS with the same testbench used for RTL to detect mismatches early.

## Incomplete Sensitivity Lists in Combinational Logic
- Combinational always blocks should react to all inputs.
- If signals are missing in the sensitivity list, RTL simulation may produce incorrect behavior, though synthesis assumes all inputs are included.

## Blocking (=) vs. Non-Blocking (<=) in Sequential Logic
- **Blocking assignments** - executes the statements in the order it is being written.
- **Non Blocking assignments** - executes and all the RHS and assign to LHS by parallal evaluation.
```c
begin
    y = q & c;
    q = a | b;
end
```
- This example code infers the use of previous value of q. That is it mimic flop for storage as the blocking statements will be evaluated in the order it is written.
```c
begin
    q = a | b;
    y = q & c;
end
```
- But this code uses the latest value of q for evaluaion. Here no flop required.
- These infers that the usage of blocking statements would cause error in the logic.
- Sequential logic must use non-blocking assignments (<=) to ensure all registers update simultaneously at the clock edge.
```c
begin
    q <= a | b;
    y <= q & c;
end
```

## Commands to perform GLS
```bash
yosys> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025c_1v80.lib
yosys> read_verilog design.v
yosys> synth -top top_module
yosys> abc -liberty ../lib/sky130_fd_sc_hd__tt_025c_1v80.lib
yosys> write_verilog -noattr design_netlist.v
iverilog ../my_lib/verilog_models/primitives.v  ../my_lib/verilog_models/sky130_fd_sc_hd.v design_netlist.v testbench.v
gtkwave testbench.vcd
```

## RTL vs GLS results of some codes:
<img width="1850" height="895" alt="d4_terop_badmux" src="https://github.com/user-attachments/assets/9fbe3ff3-ef29-4e78-bbf6-6daad52aeb80" />

### Ternary Operator

RTL Stimulation results:
<img width="1850" height="895" alt="d4_terop" src="https://github.com/user-attachments/assets/18e71c52-443f-48e3-8d98-d1c99f5ad974" />
GLS Stimulation results:
<img width="1850" height="895" alt="d4_terop gls" src="https://github.com/user-attachments/assets/698be286-cf3b-405f-b473-797f3deff5d5" />
Synthesis results:
<img width="1850" height="895" alt="d4_tern op" src="https://github.com/user-attachments/assets/236fff86-c770-46ab-86e0-dab7763579a9" />

### Bad Mux

RTL Stimulation results:
<img width="1850" height="895" alt="d4_badmux" src="https://github.com/user-attachments/assets/1936bb16-6f87-46d1-b5c4-fbd60b7d2cb3" />
GLS Stimulation results:
<img width="1850" height="895" alt="d4_badmux gls" src="https://github.com/user-attachments/assets/94ee1f34-fec3-4492-83f2-cad9b8bc7cef" />
Synthesis results:
<img width="1850" height="895" alt="d4_bad mux" src="https://github.com/user-attachments/assets/6b41809d-9889-44c2-9bf1-375fed078e03" />

### Blocking caveat

<img width="1664" height="863" alt="d4_block caveat" src="https://github.com/user-attachments/assets/84be10e4-b237-4043-8390-f34809979e79" />
RTL Stimulation results:
<img width="1850" height="895" alt="d4_block cav" src="https://github.com/user-attachments/assets/fb27e633-58a9-44f6-a006-5b89498880ea" />
GLS Stimulation results:
<img width="1850" height="895" alt="d4_block cav gls" src="https://github.com/user-attachments/assets/a345e99d-4b12-4235-8ed3-2bafbcb02745" />
Synthesis results:
<img width="1850" height="895" alt="d4_blockcav" src="https://github.com/user-attachments/assets/d1157baf-ebe1-4c34-9316-4d45c0c29ccc" />
