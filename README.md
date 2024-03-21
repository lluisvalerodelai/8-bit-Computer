# 8-bit-Computer

8-bit computer implemented completley from scratch in Logisim

Instructions

 - LDA x : 0001xxxx
  -load contents from address x to A register
 - ADD x : 0010xxxx
  -add contents from address x to value in A register
  -sum is stored in A register
 - SUB x : 0011xxxx
  -same as add, but value in address x is instead subtracted from A register
 - JMP x : 0100xxxx
  -set program counter to value X
 -STA x : 0101xxxx
  -store value in A register to RAM location x
 -LDI x : 0110xxxx
  -load x immediatley into A register
  -note that x is limited to max value of 16 (base10) because of bit limit
