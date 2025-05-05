# RV32I Pipelined Datapath (Branch Resolution in ID Stage)

## Overview

This project implements a 5-stage pipelined RISC-V RV32I processor with a key architectural enhancement:
**branch target address computation and branch outcome resolution have been moved to the Instruction Decode (ID) stage**.

This modification improves pipeline efficiency by reducing the branch resolution delay, helping mitigate control hazards without requiring deeper prediction mechanisms.

---

## Features

- ✅ Standard 5-stage pipeline: IF, ID, EX, MEM, WB
- ✅ Fully supports base RV32I instruction set
- ✅ Branch resolution and target address calculation in **ID stage**
- ✅ Integrated hazard handling and forwarding logic
- ✅ Modular design for extensibility

---

## Key Modification (Task 4)

### What Changed?

- **Branch outcome (`taken` or `not taken`)** is now computed using the instruction in the `IF/ID` stage.
- **Branch target address** is also calculated in the ID stage using `IF_ID_PC + (imm << 1)`.

### Why?

This reduces the number of wasted cycles due to branch misprediction, improving overall pipeline efficiency.

### Modified Files/Lines:

- `pc_branch_adder` now uses `IF_ID_PC`
- Branch condition logic (`Branchcntrl`) uses `IF_ID_Inst`
- `pc_next` decision logic now checks `id_stage_branch`

---

## Files

- `Datapath.v`: Main module coordinating all pipeline stages
- `Branchcntrl.v`: Branch decision unit
- `Register.v`: Parameterized register module for pipeline latches
- `ClockDiv.v`: Generates slow clock from input clock
- `defines.v`: Global constants like opcodes and control flags

---

## How to Run

1. Simulate using a Verilog simulator (e.g., ModelSim, Vivado, or Icarus Verilog).
2. Provide appropriate testbench to drive the `clk_in` and `rst` signals.
3. Monitor PC updates and instruction flow to verify correct branch handling.

---

## Future Enhancements

- Add branch prediction (2-bit dynamic predictor)
- Add support for compressed instructions (RV32C)
- Add RV32M extension for multiplication/division

---

## Author

Youssef – May 2025  
AUC | Embedded Systems & Computer Architecture
