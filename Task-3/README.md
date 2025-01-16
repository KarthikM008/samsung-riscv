# Instruction Types and Fields:- Of factorial of a number

The RISC-V instructions are categorized into types based on their field organization. Each type has specific
fields like opcode, func3, func7, immediate values, and register numbers. The types include:

R-type: Register type

I-type: Immediate type

S-type: Store type

B-type: Branch type

U-type: Upper immediate type

J-type: Jump type







# 10184:-
Instruction: addi sp, sp, -48

Type: I-type

Opcode: 0010011 (7 bits)

Immediate: 1111111111000000 (12 bits)

Source Register (rs1): 00000 (x0, 5 bits)

Destination Register (rd): 00000 (x0, 5 bits)

Function (funct3): 000 (3 bits)





# 10188:
Instruction: sd ra, 40(sp)

Type: S-type

Opcode: 0100011 (7 bits)

Immediate: 0000000001010000 (12 bits)

Source Register (rs1): 10010 (x18, 5 bits)

Destination Register (rd): 10001 (x17, 5 bits)

Function (funct3): 010 (3 bits)



# 10194:
Instruction: lui a0, 0x2b

Type: U-type

Opcode: 0110111 (7 bits)

Immediate: 0000000001011011 (20 bits)

Source Register (rs1): N/A

Destination Register (rd): 01000 (x10, 5 bits)



# 1019C:
Instruction: jal ra, 10490 <printf>

Type: J-type

Opcode: 1101111 (7 bits)

Immediate: 00000000010001001111010000000000 (20 bits)

Source Register (rs1): N/A

Destination Register (rd): 10010 (x18, 5 bits)



# 101B0:
Machine Code: 00c12483

Instruction: lw s1, 12(sp)

Type: I-type

Function: Load the word-sized value from the memory location 12 bytes above the current stack pointer into
register s1.



# 101B4:
Machine Code: 0404c863

Instruction: bltz s1, 10204 <main+0x80>

Type: B-type

Function: Branch to the address 10204 (which corresponds to the label main+0x80) if the value in register s1 is
less than zero.



# 101B8:
Machine Code: 00100413

Instruction: li s0, 1

Type: I-type

Function: Load the immediate value 1 into register s0.



# 101F0:
Machine Code: 02813083

Instruction: ld ra, 40(sp)

Type: S-type

Function: Restores the return address from the stack.



# 101D0:
Machine Code: 0004079b

Instruction: sext.w a5, s0

Type: I-type

Function: Sign-extends the counter (s0) to 64 bits.





# 101D4:
Machine Code: fef4d8e3

Instruction: bge s1, a5, 101C4 <main+0x40>

Type: B-type

Function: Checks if the inner loop condition is met.




# 101D8:
Machine Code: 00050613

Instruction: mv a2, a0

Type: R-type

Function: Prepares for the printf call



# 101F0:

Machine Code: 02813083

Instruction: ld ra, 40(sp)

Type: S-type

Function: Restores the return address from the stack.



# 10200:

Instruction: ret

Type: Special

Opcode: 1100011

rs2: N/A

rs1: N/A

funct3: 000

Function: Returns from the current subroutine.


# 10210:

Instruction: j   101ec <main+0x68>

Type: J-type

rs2: N/A

rs1: N/A

Opcode: 1101111


Function: Unconditionally jumps to the address 101ec (which corresponds to the label main+0x68).
