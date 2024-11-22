# risc_pipeline_mips32_processor

MIPS32 Pipelined Processor

This repository contains the Verilog implementation of a MIPS32 Pipelined Processor along with three testbenches designed to demonstrate the processor's functionality.
The processor supports a basic instruction set and features a 5-stage pipeline: Instruction Fetch (IF), Instruction Decode (ID), Execute (EX), Memory Access (MEM), and Write Back (WB).

Features
32-bit Processor: Supports 32-bit registers and memory.
5-Stage Pipeline: Implements all stages of the classic MIPS architecture.
Instruction Set:
  Arithmetic: ADD, SUB, MUL, ADDI, SUBI.
  Logical: AND, OR, SLT, SLTI.
  Memory Access: LW (load word), SW (store word).
  Branching: BEQZ (branch if equal to zero), BNEQZ (branch if not equal to zero).
  HALT: Terminates execution.
Hazard Handling: Supports basic hazard handling and branch instructions with a control flag.

Repository Structure
Files Included:
pipe_MIPS32.v => The Verilog implementation of the pipelined MIPS processor.

Testbenches:
testbench1.v: Demonstrates addition of three numbers stored in registers.
testbench2.v: Demonstrates loading a word from memory, performing arithmetic, and storing the result back to memory.
testbench3.v: Computes the factorial of a number stored in memory.

Processor Design Details
The processor consists of the following major components:

Registers and Memory:
32 General Purpose Registers (32-bit each).
1024 x 32-bit memory.

Pipeline Registers:
Between pipeline stages to store intermediate results (e.g., IF_ID_IR, ID_EX_A, etc.).

Instruction Types:
R-type and I-type instructions supported.

Control Signals:
HALTED: Indicates if the processor has completed execution.
TAKEN_BRANCH: Manages control hazards for branch instructions.

Parameter Definitions:
Opcodes for different instructions are defined for ease of extension.

Testbench Details
Each testbench validates the functionality of the processor with specific use cases.

Testbench 1: Addition of Three Numbers
Objective: Add the numbers 10, 20, and 30 stored in registers and store the sum in a destination register.

Steps:
Initialize registers R1, R2, and R3 with 10, 20, and 30 respectively.
Perform the addition and store the results in R4 and R5.
Validate the final values of registers.

Key Instructions:
ADDI, ADD, HLT.

Testbench 2: Memory Operations
Objective: Load a word from memory, add a constant, and store the result back in memory.

Steps:
Load a value from memory location 120 into R2.
Add 45 to R2 and store the result in memory location 121.
Validate memory contents post-execution.

Key Instructions:
ADDI, LW, SW, HLT.

Testbench 3: Factorial Computation
Objective: Compute the factorial of a number stored in memory location 200 and store the result in memory location 198.

Steps:
Initialize R10 with the base address (200).
Use a loop to multiply and decrement values stored in R3.
Store the final factorial result in memory location 198.

Key Instructions:
ADDI, LW, MUL, SUBI, BNEQZ, SW, HLT.

Simulation and Usage

Clone the repository:
bash
git clone https://github.com/samidhachari/risc_pipeline_mips32_processor.git
cd risc_pipeline_mips32_processor

Run the Verilog simulations using a tool like ModelSim or Verilator:
iverilog -o mips32_sim pipe_MIPS32.v testbench1.v
vvp mips32_sim

View the waveform (optional):
gtkwave mips.vcd

Future Enhancements
Implement advanced hazard detection and forwarding.
Add support for floating-point operations.
Optimize branch prediction.
