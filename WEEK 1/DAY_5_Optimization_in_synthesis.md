# OPTIMIZATIONS IN SYNTHESIS

## If-Else Constructs
- The if-else construct is used to describe decision-making logic in Verilog.
- Simple and intuitive for priority-based decisions.
- Suitable when only one condition should be true at a time.
Example:
```verilog
always @(*) begin
  if (a > b)
    y = a;
  else
    y = b;
end
```
## If–ElseIf–Else Constructs
- The if–elseif–else construct is used when multiple conditions need to be checked in priority order.
- The first condition that evaluates to true is executed. Remaining conditions are skipped.
Example:
```verilog
always @(*) begin
  if (sel == 2'b00)
    y = a;
  else if (sel == 2'b01)
    y = b;
  else if (sel == 2'b10)
    y = c;
  else
    y = d;   // default assignment
end
```

## Dangers with If-Else Usage
While if-else is useful, improper use can lead to synthesis problems:
- Priority Encoding:
  - Nested if-else statements imply priority logic (first condition has highest priority).
  - May lead to longer critical paths and poor timing.
- Latch Inference:
  - If not all branches assign a value, a latch may be inferred.
- Simulation vs Synthesis mismatch:
  - Using incomplete conditions may behave differently in RTL vs synthesized design.
Example:
```verilog
always @(*) begin
  if (sel == 2'b00) y = a;
  else if (sel == 2'b01) y = b;
  // Missing else → latch inferred
end
```

## Case Statements
The case statement is preferred when multiple conditions are mutually exclusive.
- Easier to read and maintain compared to long if-else chains.
- Describes parallel decisions (no implied priority unless using casez/casex).
- Always include a default case to avoid latch inference.
Example:
```verilog
always @(*) begin
  case (sel)
    2'b00: y = a;
    2'b01: y = b;
    2'b10: y = c;
    default: y = d;
  endcase
end
```

## For Loop Constructs
The for loop in Verilog is a generate-time construct used for writing repetitive structures concisely.
- Commonly used in FSMs, counters, and parameterized designs.
- Loop unrolling is done at compile/synthesis time → no runtime overhead.
Dangers:
- Avoid infinite loops or loops with non-constant bounds.
- Ensure loop indices are bounded and deterministic.
