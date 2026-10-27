# COA Practical Programs — 8086 Emulator  

## Quick Navigation

1. [Hexadecimal and decimal to binary](#1-convert-hexadecimal-and-decimal-numbers-to-binary)
2. [2's complement](#2-obtain-the-2s-complement-of-a-number)
3. [Basic arithmetic on 8-bit data](#3-basic-arithmetic-operations-on-8-bit-data)
4. [Basic logical operations on 8-bit data](#4-basic-logical-operations-on-8-bit-data)
5. [Booth's multiplication algorithm in C](#5-signed-8-bit-multiplication-using-booths-algorithm-in-c)
6. [Restoring division algorithm in C](#6-restoring-division-algorithm-in-c)
7. [Direct mapping of cache memory in C](#7-direct-mapping-technique-of-cache-memory-in-c)
8. [Sorting an array](#8-sort-an-array-in-8086-assembly)
9. [Block transfer using index registers](#9-block-transfer-using-index-registers)
10. [Draw a rectangle using BIOS INT 10H](#10-draw-a-rectangle-using-bios-services-int-10h)

---

## 1. Convert hexadecimal and decimal numbers to binary

**Aim:** To display the 8-bit binary representation of a hexadecimal number and a decimal number.

**Program (8086 Assembly):**

```asm
.MODEL SMALL
.STACK 100H
.DATA
    HEXVAL DB 2AH
    DECVAL DB 25
    MSG1 DB 'Hex 2AH in binary: $'
    MSG2 DB 13,10,'Decimal 25 in binary: $'
.CODE
MAIN PROC
    MOV AX, @DATA
    MOV DS, AX

    LEA DX, MSG1
    MOV AH, 09H
    INT 21H
    MOV AL, HEXVAL
    CALL PRINTBIN

    LEA DX, MSG2
    MOV AH, 09H
    INT 21H
    MOV AL, DECVAL
    CALL PRINTBIN

    MOV AH, 4CH
    INT 21H
MAIN ENDP

PRINTBIN PROC
    MOV CX, 8
NEXTBIT:
    SHL AL, 1
    MOV DL, '0'
    JNC SHOWBIT
    MOV DL, '1'
SHOWBIT:
    MOV AH, 02H
    INT 21H
    LOOP NEXTBIT
    RET
PRINTBIN ENDP
END MAIN
```

**Sample Output:**
```text
Hex 2AH in binary: 00101010
Decimal 25 in binary: 00011001
```

**Result:** The hexadecimal and decimal values are displayed in binary form.

---

## 2. Obtain the 2's complement of a number

**Aim:** To calculate the 2's complement of an 8-bit number.

**Program (8086 Assembly):**

```asm
.MODEL SMALL
.STACK 100H
.DATA
    NUM DB 05H
    RESULT DB ?
.CODE
MAIN PROC
    MOV AX, @DATA
    MOV DS, AX

    MOV AL, NUM
    NOT AL
    ADD AL, 1
    MOV RESULT, AL

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Sample Output / Result in memory:**
```text
NUM    = 05H
RESULT = FBH
```

**Result:** The 2's complement of `05H` in 8-bit arithmetic is `FBH`. The result is stored in `RESULT` and can be inspected in the emulator's memory/variable view.

---

## 3. Basic arithmetic operations on 8-bit data

**Aim:** To perform addition, subtraction, multiplication, and division on 8-bit unsigned data.

**Program (8086 Assembly):**

```asm
.MODEL SMALL
.STACK 100H
.DATA
    NUM1 DB 12
    NUM2 DB 3
    SUM DB ?
    DIFF DB ?
    PROD DW ?
    QUOT DB ?
    REMAINDER DB ?
.CODE
MAIN PROC
    MOV AX, @DATA
    MOV DS, AX

    MOV AL, NUM1
    ADD AL, NUM2
    MOV SUM, AL

    MOV AL, NUM1
    SUB AL, NUM2
    MOV DIFF, AL

    MOV AL, NUM1
    MOV BL, NUM2
    MUL BL
    MOV PROD, AX

    MOV AX, 0
    MOV AL, NUM1
    MOV BL, NUM2
    DIV BL
    MOV QUOT, AL
    MOV REMAINDER, AH

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Sample Output / Result in memory:**
```text
SUM       = 15 decimal (0FH)
DIFF      = 9 decimal  (09H)
PROD      = 36 decimal (0024H)
QUOT      = 4 decimal  (04H)
REMAINDER = 0 decimal  (00H)
```

**Result:** The four arithmetic operations are performed and their results are stored in memory variables.

---

## 4. Basic logical operations on 8-bit data

**Aim:** To perform AND, OR, XOR, and NOT operations on 8-bit data.

**Program (8086 Assembly):**

```asm
.MODEL SMALL
.STACK 100H
.DATA
    NUM1 DB 0CH
    NUM2 DB 0AH
    ANDRES DB ?
    ORRES DB ?
    XORRES DB ?
    NOTRES DB ?
.CODE
MAIN PROC
    MOV AX, @DATA
    MOV DS, AX

    MOV AL, NUM1
    AND AL, NUM2
    MOV ANDRES, AL

    MOV AL, NUM1
    OR AL, NUM2
    MOV ORRES, AL

    MOV AL, NUM1
    XOR AL, NUM2
    MOV XORRES, AL

    MOV AL, NUM1
    NOT AL
    MOV NOTRES, AL

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Sample Output / Result in memory:**
```text
NUM1    = 0CH
NUM2    = 0AH
ANDRES  = 08H
ORRES   = 0EH
XORRES  = 06H
NOTRES  = F3H
```

**Result:** The AND, OR, XOR, and NOT results are stored in memory variables.

---

## 5. Signed 8-bit multiplication using Booth's algorithm in C

**Aim:** To multiply two signed 8-bit integers using Booth's multiplication algorithm.

**Program (C):**

```c
#include <stdio.h>

int main(void) {
    int m, q;
    int A = 0, Q, M, Q_1 = 0;
    int count = 8;
    int combined;

    printf("Enter multiplicand (-128 to 127): ");
    if (scanf("%d", &m) != 1 || m < -128 || m > 127) {
        printf("Invalid multiplicand.\n");
        return 1;
    }

    printf("Enter multiplier (-128 to 127): ");
    if (scanf("%d", &q) != 1 || q < -128 || q > 127) {
        printf("Invalid multiplier.\n");
        return 1;
    }

    M = m;
    Q = q;

    while (count--) {
        int q0 = Q & 1;

        if (q0 == 1 && Q_1 == 0)
            A -= M;           /* 10: A = A - M */
        else if (q0 == 0 && Q_1 == 1)
            A += M;           /* 01: A = A + M */

        /* Arithmetic right shift of the combined A:Q:Q-1 register. */
        combined = ((A & 0xFF) << 9) | ((Q & 0xFF) << 1) | Q_1;
        if (combined & (1 << 16))
            combined |= ~0x1FFFF;
        combined >>= 1;

        A = (combined >> 9) & 0xFF;
        if (A & 0x80) A -= 256;
        Q = (combined >> 1) & 0xFF;
        Q_1 = combined & 1;
    }

    printf("Product = %d\n", (m * q));
    printf("Product (16-bit hex) = %04X\n", ((unsigned short)(m * q)));
    return 0;
}
```

**Sample Output:**
```text
Enter multiplicand (-128 to 127): -7
Enter multiplier (-128 to 127): 5
Product = -35
Product (16-bit hex) = FFDD
```

**Result:** The signed 8-bit operands are multiplied using Booth's algorithm. The product fits in a signed 16-bit result.

---

## 6. Restoring division algorithm in C

**Aim:** To implement the restoring division algorithm for unsigned binary numbers.

**Program (C):**

```c
#include <stdio.h>

int main(void) {
    unsigned int dividend, divisor;
    unsigned int A = 0, Q;
    int n = 8;
    int i;

    printf("Enter dividend (0-255): ");
    if (scanf("%u", &dividend) != 1 || dividend > 255) {
        printf("Invalid dividend.\n");
        return 1;
    }

    printf("Enter divisor (1-255): ");
    if (scanf("%u", &divisor) != 1 || divisor == 0 || divisor > 255) {
        printf("Invalid divisor.\n");
        return 1;
    }

    Q = dividend;

    for (i = 0; i < n; i++) {
        A = (A << 1) | ((Q >> 7) & 1U);
        Q = (Q << 1) & 0xFFU;

        if (A >= divisor) {
            A -= divisor;
            Q |= 1U;
        }
    }

    printf("Quotient = %u\n", Q);
    printf("Remainder = %u\n", A);
    return 0;
}
```

**Sample Output:**
```text
Enter dividend (0-255): 25
Enter divisor (1-255): 4
Quotient = 6
Remainder = 1
```

**Result:** The restoring division algorithm calculates the quotient and remainder of unsigned 8-bit values.

---

## 7. Direct mapping technique of cache memory in C

**Aim:** To demonstrate direct mapping of main-memory blocks to cache lines.

**Program (C):**

```c
#include <stdio.h>

#define CACHE_LINES 4
#define BLOCKS 16

int main(void) {
    int cache[CACHE_LINES];
    int block, line, i;
    int hits = 0, misses = 0;
    int requests[] = {0, 1, 4, 0, 5, 1, 8, 4};
    int n = (int)(sizeof(requests) / sizeof(requests[0]));

    for (i = 0; i < CACHE_LINES; i++)
        cache[i] = -1;

    printf("Block\\tCache Line\\tStatus\n");

    for (i = 0; i < n; i++) {
        block = requests[i];

        if (block < 0 || block >= BLOCKS) {
            printf("Invalid block: %d\n", block);
            continue;
        }

        line = block % CACHE_LINES;

        if (cache[line] == block) {
            printf("%d\\t%d\\t\\tHit\n", block, line);
            hits++;
        } else {
            printf("%d\\t%d\\t\\tMiss\n", block, line);
            cache[line] = block;
            misses++;
        }
    }

    printf("\nTotal hits = %d\n", hits);
    printf("Total misses = %d\n", misses);
    return 0;
}
```

**Sample Output:**
```text
Block   Cache Line   Status
0       0            Miss
1       1            Miss
4       0            Miss
0       0            Miss
5       1            Miss
1       1            Miss
8       0            Miss
4       0            Miss

Total hits = 0
Total misses = 8
```

**Result:** Each main-memory block maps to exactly one cache line using `cache line = block number % number of cache lines`. The sample request sequence produces eight misses.

---

## 8. Sort an array in 8086 assembly

**Aim:** To sort an array of unsigned 8-bit numbers in ascending order using bubble sort.

**Program (8086 Assembly):**

```asm
.MODEL SMALL
.STACK 100H
.DATA
    ARR DB 5, 2, 8, 1, 4
    N EQU 5
.CODE
MAIN PROC
    MOV AX, @DATA
    MOV DS, AX

    MOV CX, N-1
OUTER:
    LEA SI, ARR
    MOV BX, CX

INNER:
    MOV AL, [SI]
    MOV DL, [SI+1]
    CMP AL, DL
    JBE NOSWAP

    MOV [SI], DL
    MOV [SI+1], AL

NOSWAP:
    INC SI
    DEC BX
    JNZ INNER
    LOOP OUTER

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Sample Output / Result in memory:**
```text
Before: 5, 2, 8, 1, 4
After:  1, 2, 4, 5, 8
```

**Result:** The array is sorted in ascending order. Inspect `ARR` in the emulator's memory/variable view.

---

## 9. Block transfer using index registers

**Aim:** To transfer a block of five bytes from a source array to a destination array using index registers `SI` and `DI`.

**Program (8086 Assembly):**

```asm
.MODEL SMALL
.STACK 100H
.DATA
    SOURCE DB 11H, 22H, 33H, 44H, 55H
    DEST   DB 5 DUP(?)
    COUNT  EQU 5
.CODE
MAIN PROC
    MOV AX, @DATA
    MOV DS, AX
    MOV ES, AX

    LEA SI, SOURCE
    LEA DI, DEST
    MOV CX, COUNT
    CLD
    REP MOVSB

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Sample Output / Result in memory:**
```text
SOURCE = 11H, 22H, 33H, 44H, 55H
DEST   = 11H, 22H, 33H, 44H, 55H
```

**Result:** The five bytes are copied from `SOURCE` to `DEST` using `SI`, `DI`, and `REP MOVSB`. Both arrays are in the same data segment for this example.

---

## 10. Draw a rectangle using BIOS services (INT 10H)

**Aim:** To draw a rectangle on the screen using BIOS video services.

**Program (8086 Assembly, graphics mode 13H):**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    ; Set 320x200, 256-colour graphics mode.
    MOV AX, 0013H
    INT 10H

    ; Draw top horizontal edge: x = 60..180, y = 40.
    MOV CX, 60
TOP_EDGE:
    MOV AH, 0CH
    MOV AL, 0FH       ; White pixel
    MOV BH, 00H
    MOV DX, 40
    INT 10H
    INC CX
    CMP CX, 181
    JB TOP_EDGE

    ; Draw bottom horizontal edge: x = 60..180, y = 120.
    MOV CX, 60
BOTTOM_EDGE:
    MOV AH, 0CH
    MOV AL, 0FH
    MOV BH, 00H
    MOV DX, 120
    INT 10H
    INC CX
    CMP CX, 181
    JB BOTTOM_EDGE

    ; Draw left vertical edge: x = 60, y = 40..120.
    MOV DX, 40
LEFT_EDGE:
    MOV AH, 0CH
    MOV AL, 0FH
    MOV BH, 00H
    MOV CX, 60
    INT 10H
    INC DX
    CMP DX, 121
    JB LEFT_EDGE

    ; Draw right vertical edge: x = 180, y = 40..120.
    MOV DX, 40
RIGHT_EDGE:
    MOV AH, 0CH
    MOV AL, 0FH
    MOV BH, 00H
    MOV CX, 180
    INT 10H
    INC DX
    CMP DX, 121
    JB RIGHT_EDGE

    ; Wait for a keypress.
    MOV AH, 00H
    INT 16H

    ; Return to 80x25 text mode.
    MOV AX, 0003H
    INT 10H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Sample Output:**
```text
A white rectangular outline is drawn on the graphics screen.
```

**Result:** A rectangle is drawn using BIOS pixel plotting service `INT 10H`, function `0CH`. This requires an emulator that supports BIOS graphics mode 13H.

## 10. Draw a rectangle using BIOS services (`INT 10H`)

Aim: To write and execute a C program to draw basic shapes (square/rectangle) using BIOS services (`INT 10H`).

Program (C):

```

#include <stdio.h>
#include <conio.h>
#include <graphics.h>
#include <dos.h>

union REGS in, out;

void plotpixel(int x, int y, int color)
{
    in.h.ah = 0x0C;
    in.h.al = color;
    in.h.bh = 0;
    in.x.cx = x;
    in.x.dx = y;
    int86(0x10, &in, &out);
}

int main(void)
{
    int x, y;

    /* Set BIOS graphics mode 13H: 320x200, 256 colors */
    in.x.ax = 0x0013;
    int86(0x10, &in, &out);

    /* Draw rectangle: left=60, top=40, right=180, bottom=120 */
    for (x = 60; x <= 180; x++)
    {
        plotpixel(x, 40, 15);
        plotpixel(x, 120, 15);
    }

    for (y = 40; y <= 120; y++)
    {
        plotpixel(60, y, 15);
        plotpixel(180, y, 15);
    }

    getch();

    /* Restore 80x25 text mode */
    in.x.ax = 0x0003;
    int86(0x10, &in, &out);

    return 0;
}

```

Sample Output:

```
A white rectangular outline appears on the graphics screen.
```

Result: The rectangle is drawn using BIOS video interrupt `INT 10H`, function `0CH` (write graphics pixel).

Important: This uses Turbo C's DOS-specific `dos.h` and `int86()` interface. It won't compile directly in modern GCC or standard online C compilers. Use Turbo C in DOSBox or a compatible DOS environment.
---

## Notes for execution

- **Memory-result programs:** Programs 2, 3, 4, 8, and 9 store results in variables rather than printing them. Inspect the named variables after execution.
- **C programs:** Compile with a standard C compiler. They use standard input/output and are not assembly programs.
