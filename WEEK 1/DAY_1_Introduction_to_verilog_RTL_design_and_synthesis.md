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

## RTL Design
- RTL (Register Transfer Level) design describes the flow of data between registers and the operations performed on that data.
- It is the behavioural representation of specification.

## Why Different Flavors of Gate
- Standard cell libraries contain multiple variants of the same logical gate with different characteristics to optimize for power, performance, and area.

## Faster and Slower Cells
- Capacitor is used as load in digital system.
- The charging and discharging of capacitor determines the delay of design.
- This charging and discharging can be determined by the transistors:
    - WIDE Transistors: provides low delay with more area and power.
    - NARROW Transistors: provides more delay with less area and power.

### Faster Cells (LVT - Low Voltage Threshold)
Advantages:
- Higher switching speed
- Better performance on critical paths
Disadvantages:
- Higher leakage power
- Increased static power consumption
- More sensitive to process variations

### Slower Cells (HVT - High Voltage Threshold)
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
> iverilog design_filename.v testbench_filename.v
> ./a.out
> gtkwave testbench_filename.v
```
<img width="1848" height="346" alt="d1_1" src="https://github.com/user-attachments/assets/5aac1dcd-2292-48e4-8187-b6e409bfe870" />

## Yosys Setup
```bash
> yosys
yosys> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025c_1v80.lib
yosys> read_verilog design_filename.v
yosys> synth -top module_name
yosys> abc -liberty ../lib/sky130_fd_sc_hd__tt_025c_1v80.lib
yosys> show
yosys> write_verilog -noattr design_netlist.v
yosys> !gvim design_netlist.v
```
<img width="1848" height="574" alt="d1_1 - Copy" src="https://github.com/user-attachments/assets/eefc3358-2faf-48b0-8829-d714efce18bc" />
<img width="1848" height="893" alt="d1_2" src="https://github.com/user-attachments/assets/cdfbd839-9e42-4f5f-b184-ebccc388ebaa" />
<img width="1848" height="893" alt="d1_3" src="https://github.com/user-attachments/assets/331153c4-96e7-458d-b6b3-72b269f787e0" />

## Example
### 2x1 Multiplexer

CODE
<img width="1850" height="334" alt="d1_goodmux" src="https://github.com/user-attachments/assets/d2d16066-c101-4bc4-9b69-41d424a43cb2" />

WAVEFORM
<img width="1850" height="895" alt="d1_goodmux_wave" src="https://github.com/user-attachments/assets/0ce299af-ca7d-423d-b819-f475c49e4505" />

SYNTHESIS
<img width="1850" height="895" alt="good_mux" src="https://github.com/user-attachments/assets/27e0d4e0-2d7b-48d3-886c-b9223d731987" />

NETLIST
<img width="1850" height="895" alt="goodmux" src="https://github.com/user-attachments/assets/d98e2347-223d-4935-9028-eb9eac6c9fda" />
