# Subtraction Programs

## sub1.asm

This program performs an 8-bit subtraction:

50 - 80 = -30

The results observed in GDB were:

- AL before subtraction = 50
- AL after subtraction = -30
- Stored result (unsigned) = 226
- EFLAGS = [CF PF SF IF]

The stored value is 226 when interpreted as unsigned because -30 is represented as 11100010 (0xE2) in 8-bit two's complement.

### Flag Explanation

- **CF = 1 (set):** A borrow was required because 50 is smaller than 80 in unsigned arithmetic.
- **PF = 1 (set):** The result 11100010 contains four 1 bits, giving even parity.
- **AF = 0 (cleared):** No borrow occurred from bit 4 during the subtraction.
- **ZF = 0 (cleared):** The result is not zero.
- **SF = 1 (set):** The most significant bit of the result is 1, indicating a negative signed result.
- **OF = 0 (cleared):** The signed result -30 is within the 8-bit signed range of -128 to 127.

## sub2.asm

This program performs a 16-bit subtraction:

1000 - 2000 = -1000

The results observed in GDB were:

- AX before subtraction = 1000
- AX after subtraction = -1000
- Stored result (unsigned) = 64536
- Stored result (signed) = -1000
- EFLAGS = [CF PF SF IF]

### Flag Explanation

- **CF = 1 (set):** A borrow was required because 1000 is smaller than 2000 in unsigned arithmetic.
- **PF = 1 (set):** The least significant byte of the result has an even number of 1 bits.
- **AF = 0 (cleared):** No borrow occurred from bit 4 during the subtraction.
- **ZF = 0 (cleared):** The result is -1000, so it is not zero.
- **SF = 1 (set):** The most significant bit of the 16-bit result is 1, indicating a negative signed result.
- **OF = 0 (cleared):** The result -1000 is within the signed 16-bit range of -32768 to 32767.

The IF flag was also displayed by GDB, but it is not an arithmetic result flag produced by the subtraction.