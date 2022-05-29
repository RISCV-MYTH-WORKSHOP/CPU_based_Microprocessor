# Basic RISC-V CPU micro-architecture 

This section will cover the implementation of a simple 3-stage RISC-V Core / CPU.
### The 3-stages broadly are: 

* Fetch
* Decode
* Execute. 


### Basic block of the CPU/RISC-V core

![riscv_block_diagram](https://user-images.githubusercontent.com/88897605/170861561-0fb3a68c-7d2f-4fd6-ad00-3370fc5af3e9.jpeg)

## Fetch

##### Program Counter 
* (```Instruction Pointer```) is a block which contains the address of the next instruction to be executed.
 
* It is feed to the instruction memory, which in turn gives out the instruction to be executed
* In Short ```Program Counter (PC)```: Holds the address of next Instruction


##### Instruction Memory (IM)
* ```IM``` :Holds the set of instructions to be executed
* The instruction memory gives out a 32-bit instruction depending upon the input address

During Fetch Stage, processor fetches the instruction from the IM pointed by address given by PC

The below Snippet shows the Program Counter and Instruction Fetch Implementation in Makerchip

![fetch](https://user-images.githubusercontent.com/88897605/170862029-7dfb3d17-eaed-4f93-90e0-db4e84c7ea93.png)


## Decode
6 types of Instructions:

 * R-type - Register
 * I-type - Immediate
 * S-type - Store
 * B-type - Branch (Conditional Jump)
 * U-type - Upper Immediate
 * J-type - Jump (Unconditional Jump)
 
Decode Function - The 32-bit fetched instruction has to be decoded first to determine the operation to be performed and the source / destination address. Instruction Type is first identified on the opcode bits of instruction. The instruction type can R, I, S, B, U, J. Every instruction has a fixed format defined in the RISC-V ISA. Depending on the formats, the following fields are determined:

* ```opcode``` funct3, funct7 -> Specifies the Operation
* ```imm``` -> Immediate values / Offsets
* ```rs1```,```rs2``` -> Source register index
* ```rd``` -> Destination register index

The Below snippet shows the Decode in Makerchip
![decode](https://user-images.githubusercontent.com/88897605/170862239-b991fd07-e9ad-4c93-9fcc-3e98521b2dbc.png)


## Register file Read and Write

Here the Register file is 2 read, 1 write means 2 read and 1 write operation can happen simultanously.

Inputs:

Read_Enable - Enable signal to perform read operation
Read_Address1 - Address1 from where data has to be read
Read_Address2 - Address2 from where data has to be read
Write_Enable - Enable signal to perform write operation
Write_Address - Address where data has to be written
Write_Data - Data to be written at Write_Address
Outputs:

Read_Data1 - Data from Read_Address1
Read_Data2 - Data from Read_Address2

The Below Snippet shows the Write and Read Register Implementation in Makerchip.

### Read

The Below Snippet shows the Read Register Implementation in Makerchip. 

![Read](https://user-images.githubusercontent.com/88897605/170862394-43614149-e49d-405e-be2f-e3255b1e489a.png)

### Write

The Below Snippet shows the Write Register Implementation in Makerchip.

![write](https://user-images.githubusercontent.com/88897605/170862405-e8acd752-7be2-4d74-a2e5-e0f81d665c18.png)

# Execute

* Operation- During the Execute Stage, both the operands perform the operation based on Opcode

Below is Snippet shows Excute stage in Makerchip.

![excute](https://user-images.githubusercontent.com/88897605/170862589-020c4532-77cc-4761-809b-8db593f060d1.png)

# Control logic

* Operation- During Decode Stage,branch target address is calculated and fed into PC mux. Before Execute Stage, once the operands are ready branch condition is checked.

Below is Snippet shows Control logic stage in Makerchip.

![control_logic](https://user-images.githubusercontent.com/88897605/170862720-abfb3e8d-d69d-4f6b-abfc-262da9aae44a.png)

