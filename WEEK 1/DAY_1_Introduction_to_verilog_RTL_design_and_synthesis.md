# VERILOG RTL DESIGN
## STIMULATOR
- A simulator is an essential tool in digital design that models the behavior of hardware described using HDL (Hardware Description Language) like Verilog.
- The RTL design is checked for adherence to specification by stimulatinf the design.
- It allows designers to verify functionality before physical implementation.
- Icarus Verilog (iverilog) is used for stimulation of RTL design.

## DESIGN
- A design refers to the hardware description of a digital circuit using HDL constructs.
- It represents the intended functionality of the digital system to meet the specification.
- Design Styles:
    - Behavioral: Algorithmic description without structure
    - RTL (Register Transfer Level): Data flow between registers
    - Structural: Interconnection of components/modules

## TESTBENCH
- A testbench is a Verilog module that instantiates the Design Under Test (DUT) or Unit Under Test (UUT).
- It applies stimulus to verify its functionality.

## HOW STIMULATOR WORKS?
- Looks for changes on output signal with respect to changes in input signal.
- Design may have one or more primary inputs or outputs but testbench should not have any primary input or output.
- dig --

## RTL Design
- RTL (Register Transfer Level) design describes the flow of data between registers and the operations performed on that data.
- It is the behavioural representation of specification.
- dig --

## Why Different Flavors of Gate
- Standard cell libraries contain multiple variants of the same logical gate with different characteristics to optimize for power, performance, and area.
- dig --

## Faster and Slower Cells
- Capacitor is used as load in digital system.
- The charging and discharging of capacitor determines the delay of design.
- This charging and discharging can be determined by the transistors:
    - WIDE Transistors: provides low delay with more area and power.
    - NARROW Transistors: provides more delay with less area and power.

# Faster Cells (LVT - Low Voltage Threshold)
Advantages:
- Higher switching speed
- Better performance on critical paths
Disadvantages:
- Higher leakage power
- Increased static power consumption
- More sensitive to process variations

# Slower Cells (HVT - High Voltage Threshold)
Advantages:
- Lower leakage power
- Better power efficiency
- More robust to variations
Disadvantages:
- Slower switching speed
- Not suitable for timing-critical paths

## Selection of Cells
- We need to guide the synthesizer to select the flavour of cells that is optimum in implementation of logic.
- 'Constraints' play a major part in selectionof cells.
- 'Yosys' is used for the synthesis of RTL design.

## Icarus Verilog (iverilog) Setup
```bash
iverilog design_filename.v testbench_filename.v
./a.out
gtkwave testbench_filename.v
```

## Yosys Setup
```bash
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025c_1v80.lib
read_verilog design_filename.v
synth -top module_name
abc -liberty ../lib/sky130_fd_sc_hd__tt_025c_1v80.lib
show
```
