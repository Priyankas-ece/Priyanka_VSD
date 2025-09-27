# Logic Optimization in Digital Design
Optimization is the process of improving a design’s area, power, and timing while maintaining functional correctness. It is typically performed during the synthesis stage. Optimizations can be broadly classified into combinational and sequential optimizations.

## Combinational Optimization
Combinational optimization focuses on reducing redundant logic in purely combinational circuits.

### Constant Propagation
If an input signal is tied to a constant (0 or 1), the synthesis tool simplifies the logic accordingly.
Example:
```verilog
assign y = ! ( a | b ( & C ));  // Always !c
assign z = b | 1'b1;  // Always 1
```
After optimization:
```veriog
assign y = !c;
assign z = 1'b1;
```

### Boolean Logic Simplification
- Tools apply Boolean algebra rules (like De Morgan’s, absorption, redundancy elimination).
- Reduces gate count and critical path.
Example:
```verilog
assign y = a ? ( b ? c : ( c ? a : o ) ) : ( !c ) 
```
After optimization:
```verilog
assign y = a ^~ c; 
```

### Examples
<img width="1664" height="863" alt="d3_optcheck123" src="https://github.com/user-attachments/assets/dee397b4-e87d-4f08-ab3c-dde29b8f4754" />
<img width="1850" height="895" alt="opt check 1" src="https://github.com/user-attachments/assets/4b44c75d-a953-4f6c-9245-8cf88f189cb8" />
<img width="1850" height="895" alt="opt check 2" src="https://github.com/user-attachments/assets/9cb1f8c9-bc7f-421c-a235-0e7587dfe63e" />
<img width="1850" height="895" alt="opt check 3" src="https://github.com/user-attachments/assets/379c6b53-1a6e-4cbc-98de-4913388c6044" />

## Sequential Optimization
Sequential optimization deals with circuits containing flip-flops/registers.

### Constant Propagation in Sequential Logic
- Registers driven by constants are optimized away.
- After optimization, q is tied directly to 0 (no flip-flop needed).
Example:
```verilog
always @(posedge clk)
begin
    q <= 1'b0;
end
```

### State Cloning
- In Finite State Machines (FSMs), if two states behave identically for all inputs, one can be eliminated and replaced by the other.
- Reduces number of states and hardware cost.

### Cloning
- Replicating logic elements (like registers or gates) to reduce fanout delay.
- Example: Instead of one register driving 100 loads, synthesis may clone it into 2 registers each driving 50 loads.
- This helps meet timing closure.

### Retiming
- Moving registers across combinational logic to balance delays.
- Goal: Improve clock frequency by redistributing logic across pipeline stages.

### Examples
<img width="1850" height="895" alt="d3_dffcont123" src="https://github.com/user-attachments/assets/e239d8d0-adb7-4c29-b6bf-da7a23b6efdf" />
<img width="1850" height="895" alt="d3_dffcont45" src="https://github.com/user-attachments/assets/bd4b0c2e-9c54-48cf-bb23-f87094acfdda" />

<img width="1850" height="895" alt="d3_dff const 1" src="https://github.com/user-attachments/assets/d74a2e14-9c56-4013-a16a-36de8e2beea8" />
<img width="1850" height="895" alt="d3_dff const1" src="https://github.com/user-attachments/assets/1574bd1d-aa89-43af-a129-28ca1b2e3f3c" />

<img width="1850" height="895" alt="d3_dff const 2" src="https://github.com/user-attachments/assets/3c75a4f2-e528-49aa-b83c-5b5c27d6a160" />
<img width="1850" height="895" alt="d3_dff const2" src="https://github.com/user-attachments/assets/d8eb181e-cbc2-4b3a-bf7e-63a475d0390e" />

<img width="1850" height="895" alt="d3_dff const 3" src="https://github.com/user-attachments/assets/51764ee9-e1b4-462a-9f56-482a85639db3" />
<img width="1850" height="895" alt="d3_dff const3" src="https://github.com/user-attachments/assets/697dd198-604d-4c9f-9d57-c989c450eb68" />

<img width="1850" height="895" alt="d3_dff const 4" src="https://github.com/user-attachments/assets/5c073dbc-329a-4bf7-b018-e9cf486c8e1d" />
<img width="1850" height="895" alt="d3_dff const4" src="https://github.com/user-attachments/assets/31424fe8-a4e6-4ad2-b94d-85503602f81b" />

<img width="1850" height="895" alt="d3_dff const 5" src="https://github.com/user-attachments/assets/c01354b6-17f2-4a40-962d-00aef30cc68b" />
<img width="1850" height="895" alt="d3_dff const5" src="https://github.com/user-attachments/assets/340689ba-5142-4a13-921e-abf1e7abd818" />

## Sequential Optimization of Unused Outputs
- If certain flip-flop outputs are unused, synthesis tools remove them.
- Prevents unnecessary storage and reduces area/power.

### Examples
<img width="1850" height="400" alt="counter opt1" src="https://github.com/user-attachments/assets/2dcccfa1-5437-4090-8b94-a6187629d7e5" />
<img width="1850" height="895" alt="counter opt 1" src="https://github.com/user-attachments/assets/f3020de5-dbf9-4e07-875b-f845c51c748c" />

<img width="1850" height="400" alt="counter opt2" src="https://github.com/user-attachments/assets/0d60d20b-f413-432e-9062-a4225b69b75b" />
<img width="1850" height="895" alt="counter opt 2" src="https://github.com/user-attachments/assets/cef50d80-2149-453d-aa55-3c29541610e4" />
