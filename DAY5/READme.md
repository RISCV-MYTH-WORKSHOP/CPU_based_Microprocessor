
# Pipelined RISC-V Core

* Pipelining processes increases the overall performance of the system. Thus, the previously designed cores can be pipelined. 
* The "Timing Abstraction" feature of TL-Verilog makes it easy.
* Converting non-piepleined CPU to pipelined CPU using timing abstract feature of TL-Verilog. This allows easy retiming wihtout any risk of funcational bugs. 
* More details reagrding Timing Abstract in TL-Verilog can be found in IEEE Paper ["Timing-Abstract Circuit Design in Transaction-Level Verilog" by Steven Hoover.](https://ieeexplore.ieee.org/document/8119264)

## Pipelining the Core

* Pipelining the CPU with branches still having 3 cycle delay rest all instructions are pipelined

Pipelining the CPU in TL-Verilog can be done in following manner:
```
|<pipe_name>
@<pipe_stage>
   Instructions present in this stage
@<pipe_stage>
   Instructions present in this stage
```
There are various hazards to be taken into consideration while implementing a pipelined design. Some of hazards taken under consideration are:

* Improper Updating of Program Counter (PC)
* Read-before-Write Hazard

Below is Snippet of pipelined CPU with a test case of assembly program which does summation from 1 to 9 then stores to r10 of register file

In Snippet r10 = 45 Test case: ```*passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9);```

![piplining_cpu](https://user-images.githubusercontent.com/88897605/170863136-854575e8-bf0d-4dfa-beed-914eb8d62e71.png)

# Load and Store Data

Similar to branch, load will also have 3 cycle delay. So, added a Data Memory 1 write/read memory.

Inputs:

* Read_Enable - Enable signal to perform read operation
* Write_Enable - Enable signal to perform write operation
* Address - Address specified whether to read/write from
* Write_Data - Data to be written on Address (Store Instruction)
Output:

 * Read_Data - Data to be read from Address (Load Instruction)
 
Added test case to check fucntionality of load/store. Stored the summation of 1 to 9 on address 4 of Data Memory and loaded that value from Data Memory to r17.



* A Data memory can be added to the Core. The Load-Store operations will add up a new stage to the core.Thus,making it now a 4-Stage Core/CPU.

The proper functioning of the RISC-V core can be ensured by introducing some testcases to the code.
* For example, if program for summation of positive integers from 1 to 9 and storing it to specific register can be verified by:

   * ```*passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9);``` 

Below is Snippet from Makerchip IDE after including load/store instructions in Makerchip

![load$store](https://user-images.githubusercontent.com/88897605/170863238-7f5f164b-11f1-4712-be84-b9e12d56d9e0.png)

# FINAL RISC-V CPU

* After pipelining is proved in simulations, the operations for Jump Instructions are added. 
* Also, added Instruction Decode and ALU Implementation for RV32I Base Integer Instruction Set.

The Snippet below shows the successful implementation of 4-stage RISC-V Core

![final_cpu](https://user-images.githubusercontent.com/88897605/170863583-6a18307d-570c-4be4-bb6e-aecd1cc10305.png)
