
# 8-bit computer architecture

8-bit computer implemented completley from scratch in Logisim. 

## Architecture
The computer uses a Simple As Possible (SAP) architecture, it consists of 
* 8-bit bus
* Program Counter
* A & B Registers
    * Store 8 bit values each
* Address Register
* ALU capable of adding, subtracting and bitwise operations
* 16x8 RAM module
* Instruction Register

## Instructions
 * LDA x : 0001xxxx
    * load contents from address x to A register
 * ADD x : 0010xxxx
    * add contents from address x to value in A register
    * sum is stored in A register
 * SUB x : 0011xxxx
    * same as add, but value in address x is instead subtracted from A register
 * JMP x : 0100xxxx
    * set program counter to value X
 * STA x : 0101xxxx
    * store value in A register to RAM location x
 * LDI x : 0110xxxx
    * load x immediatley into A register
    * note that x is limited to max value of 16 (base10) because of bit limit


## Microcode Instructions
The control signals for each microcode instruction are generated with a ROM which contains each sub-instruction for each sub-pulse of the clock

Instruction     Step    Control Work (hexadecimal representation)
                                        AI AO BI BO ΣO SU RI RO CO JMP CE MI II IO xx xx
Fetch - xxxx    000     0x0090          0  0  0  0  0  0  0  0  1  0   0  1  0  0  0  0
                001     0x0128          0  0  0  0  0  0  0  1  0  0   1  0  1  0  0  0

LDA   - 0001    000     0x0090          0  0  0  0  0  0  0  0  1  0   0  1  0  0  0  0
 -arg: addr     001     0x0128          0  0  0  0  0  0  0  1  0  0   1  0  1  0  0  0  
                010     0x0014          0  0  0  0  0  0  0  0  0  0   0  1  0  1  0  0
                011     0x8100          1  0  0  0  0  0  0  1  0  0   0  0  0  0  0  0
                
ADD   - 0010    000     0x0090          0  0  0  0  0  0  0  0  1  0   0  1  0  0  0  0
 -arg: addr     001     0x0128          0  0  0  0  0  0  0  1  0  0   1  0  1  0  0  0
                010     0x0014          0  0  0  0  0  0  0  0  0  0   0  1  0  1  0  0
                011     0x2100          0  0  1  0  0  0  0  1  0  0   0  0  0  0  0  0
                100     0x8800          1  0  0  0  1  0  0  0  0  0   0  0  0  0  0  0

SUB   - 0011    000     0x0090          0  0  0  0  0  0  0  0  1  0   0  1  0  0  0  0
 -arg: addr     001     0x0128          0  0  0  0  0  0  0  1  0  0   1  0  1  0  0  0
                010     0x0014          0  0  0  0  0  0  0  0  0  0   0  1  0  1  0  0
                011     0x2100          0  0  1  0  0  0  0  1  0  0   0  0  0  0  0  0
                100     0x8C00          1  0  0  0  1  1  0  0  0  0   0  0  0  0  0  0

JMP   - 0100    000     0x0090          0  0  0  0  0  0  0  0  1  0   0  1  0  0  0  0
 -arg: value    001     0x0128          0  0  0  0  0  0  0  1  0  0   1  0  1  0  0  0
                010     0x0014          0  0  0  0  0  0  0  0  0  0   0  1  0  1  0  0
                011     0x0140          0  0  0  0  0  0  0  1  0  1   0  0  0  0  0  0

STA   - 0101    000     0x0090          0  0  0  0  0  0  0  0  1  0   0  1  0  0  0  0
 -arg: addr     001     0x0128          0  0  0  0  0  0  0  1  0  0   1  0  1  0  0  0
                010     0x0014          0  0  0  0  0  0  0  0  0  0   0  1  0  1  0  0
                011     0x4200          0  1  0  0  0  0  1  0  0  0   0  0  0  0  0  0

LDI   - 0110    000     0x0090          0  0  0  0  0  0  0  0  1  0   0  1  0  0  0  0
 -arg: value    001     0x0128          0  0  0  0  0  0  0  1  0  0   1  0  1  0  0  0
                010     0x8004          1  0  0  0  0  0  0  0  0  0   0  0  0  1  0  0
