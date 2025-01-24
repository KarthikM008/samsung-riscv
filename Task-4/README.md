# TASK-4 :- Functional Simulation of RISC-V Core
In this task, we will perform functional simulation of RISC-V instructions modeled as a Verilog netlist and observe the output waveforms using GTKWave.


# RISC-V rv32i
This project provides an insight into the working of a few important instructions of the instruction set of a Single cycle Reduced Instruction Set Computer - Five(RISC-V) Instruction Set Architecture suitable for use across wide-spectrum of Applications from low power embedded devices to high performance Cloud based Server processors. The base RISC-V is a 32-bit processor with 31 general-purpose registers, so all the instructions are 32-bit long. Some Applications where the RISC-V processors have begun to make some significant threads are in Artificial intelligence and machine learning, Embedded systems, Ultra Low power processing systems etc.


# BLOCK DIAGRAM OF rv32i
![181293948-beb8622c-7696-4b06-b6c9-eeab9b8ab9d3](https://github.com/user-attachments/assets/c5a5d53c-fab6-44a5-b82e-d5dce90834c8)

# How it works?
You write Verilog code and run simulations using Icarus Verilog. The simulator generates a Value Change Dump (VCD) or other waveform file formats. These waveform files are then loaded into GTKWave for graphical analysis of the signal behavior, helping you verify your design's functionality and timing.

Installing iverilog using command sudo apt install iverilog gtkwave

# installation of iverilog & gtkwave
![installation of iverilog   gtkwave](https://github.com/user-attachments/assets/1e2771dd-6eaf-45bb-badc-6f6ae2c0c761)

# GTK wave
![GTK wave](https://github.com/user-attachments/assets/9be6660a-3a18-4c38-91e2-aecc57ad86fe)


# The output waveform
The output waveform showing the instructions performed in a 5-stage pipelined architecture.



# 1 ADD
ADD R6, R2, R1
![ADD](https://github.com/user-attachments/assets/0dee9cde-7e6d-4417-9501-4c776d6a6c2e)



# 2 SUB
SUB R7, R1, R2
![SUB](https://github.com/user-attachments/assets/7ce94474-a6a7-4025-8342-eae247159888)



# 3 ADDI R12, R4,5

![ADDI](https://github.com/user-attachments/assets/b89bda16-221d-4039-8207-6f4fdd24b255)

# 4 OR R9, R2, R5

![OR](https://github.com/user-attachments/assets/f6c4147b-0b55-4cee-ac6d-56f027012b4e)


# 5 AND R8, R1, R3

![AND](https://github.com/user-attachments/assets/94a39419-9215-4ec0-a386-fd2c45c569be)


# 6 XOR R10, R1, R4

![XOR](https://github.com/user-attachments/assets/925c049f-9a16-4b81-b95e-c1e7527e559f)


# 7 SLT R1, R2, R4

![SLT](https://github.com/user-attachments/assets/e613cc6c-8013-4720-ad98-d91346290d8a)


# 8 SRL R16, R11, R2

![SRL](https://github.com/user-attachments/assets/a417820a-5b46-4375-b07a-1676af8a1e1d)

# 9 BEQ R0, R0, 15

![BNE](https://github.com/user-attachments/assets/74c9e354-2e8a-4a20-8ba8-33373d7aa73b)


# 10 SW R3, R1, 2

![SW](https://github.com/user-attachments/assets/80a53091-a314-435c-bc35-2079b655fb43)


# 11 BNE R0, R1, 15

![BNE](https://github.com/user-attachments/assets/2493cd23-67ba-4e13-900a-15d333f24f0c)



# operations & description 

Operation              | Description                                          | Standard RISC-V instruction | 32 bit Instruction
-----------------------|------------------------------------------------------|---------------------|-------------------
ADD R6, R2, R1          | Adds the values in R2 and R1, stores result in R6    | 32'h00110333        | 32'h02208300
SUB R7, R1, R2          | Subtracts the value in R2 from R1, stores result in R7 | 32'h402083b3        | 32'h02209380
AND R8, R1, R3          | Performs bitwise AND between R1 and R3, stores in R8 | 32'h0030f433        | 32'h0230a400
OR R9, R2, R5           | Performs bitwise OR between R2 and R5, stores in R9 | 32'h005164b3        | 32'h02513480
XOR R10, R1, R4         | Performs bitwise XOR between R1 and R4, stores in R10 | 32'h0040c533        | 32'h0240c500
SLT R1, R2, R4          | Sets R1 to 1 if R2 < R4, else sets to 0             | 32'h0045a0b3        | 32'h02415580
ADDI R12, R4, 5         | Adds immediate value 5 to R4, stores result in R12  | 32'h004120b3        | 32'h00520600
BEQ R0, R0, 15          | Branches to offset 15 if R0 equals R0               | 32'h00000f63        | 32'h00f00002
SW R3, R1, 2            | Stores word from R3 to memory address (R1 + 2)      | 32'h0030a123        | 32'h00209181
LW R13, R1, 2           | Loads word from memory address (R1 + 2) into R13    | 32'h0020a683        | 32'h00208681
SRL R16, R14, R2        | Shifts R14 right by the value in R2, stores in R16  | 32'h0030a123        | 32'h00271803
SLL R15, R1, R2         | Shifts R1 left by the value in R2, stores in R15    | 32'h002097b3        | 32'h00208783
