# COA

**Software:** MASM and DOSBox

## Quick Navigation

1. [Addition: 3 + 4](#1-addition-3--4)
2. [Addition: 2 + 6](#2-addition-2--6)
3. [Subtraction: 8 - 3](#3-subtraction-8---3)
4. [Subtraction: 9 - 4](#4-subtraction-9---4)
5. [Multiplication: 2 × 3](#5-multiplication-2--3)
6. [Multiplication: 2 × 4](#6-multiplication-2--4)
7. [Division: 8 ÷ 2](#7-division-8--2)
8. [Division: 9 ÷ 3](#8-division-9--3)
9. [Bitwise AND: 6 AND 3](#9-bitwise-and-6-and-3)
10. [Bitwise AND: 7 AND 5](#10-bitwise-and-7-and-5)
11. [Bitwise OR: 4 OR 3](#11-bitwise-or-4-or-3)
12. [Bitwise OR: 2 OR 5](#12-bitwise-or-2-or-5)
13. [Bitwise XOR: 5 XOR 3](#13-bitwise-xor-5-xor-3)
14. [Bitwise XOR: 7 XOR 3](#14-bitwise-xor-7-xor-3)
15. [Bitwise NOT: FC hex](#15-bitwise-not-fc-hex)
16. [Bitwise NOT: FA hex](#16-bitwise-not-fa-hex)
17. [Check whether 6 is even](#17-check-whether-6-is-even)
18. [Check whether 7 is odd](#18-check-whether-7-is-odd)
19. [Smaller of 3 and 7](#19-smaller-of-3-and-7)
20. [Smaller of 8 and 4](#20-smaller-of-8-and-4)
21. [Greater of 3 and 7](#21-greater-of-3-and-7)
22. [Greater of 8 and 4](#22-greater-of-8-and-4)

---

## 1. Addition: 3 + 4

**Aim:** To add three and four and display the sum.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AX, 3
    ADD AX, 4
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
7
```

**Result:** The sum is 7.

## 2. Addition: 2 + 6

**Aim:** To add two and six and display the sum.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AX, 2
    ADD AX, 6
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
8
```

**Result:** The sum is 8.

## 3. Subtraction: 8 - 3

**Aim:** To subtract three from eight and display the difference.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AX, 8
    SUB AX, 3
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
5
```

**Result:** The difference is 5.

## 4. Subtraction: 9 - 4

**Aim:** To subtract four from nine and display the difference.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AX, 9
    SUB AX, 4
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
5
```

**Result:** The difference is 5.

## 5. Multiplication: 2 × 3

**Aim:** To multiply two by three and display the product.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 2
    MOV BL, 3
    MUL BL
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
6
```

**Result:** The product is 6.

## 6. Multiplication: 2 × 4

**Aim:** To multiply two by four and display the product.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 2
    MOV BL, 4
    MUL BL
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
8
```

**Result:** The product is 8.

## 7. Division: 8 ÷ 2

**Aim:** To divide eight by two and display the quotient.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AX, 8
    MOV BL, 2
    DIV BL
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
4
```

**Result:** The quotient is 4.

## 8. Division: 9 ÷ 3

**Aim:** To divide nine by three and display the quotient.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AX, 9
    MOV BL, 3
    DIV BL
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
3
```

**Result:** The quotient is 3.

## 9. Bitwise AND: 6 AND 3

**Aim:** To perform a bitwise AND operation on six and three.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 6
    AND AL, 3
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
2
```

**Result:** The AND result is 2.

## 10. Bitwise AND: 7 AND 5

**Aim:** To perform a bitwise AND operation on seven and five.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 7
    AND AL, 5
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
5
```

**Result:** The AND result is 5.

## 11. Bitwise OR: 4 OR 3

**Aim:** To perform a bitwise OR operation on four and three.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 4
    OR AL, 3
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
7
```

**Result:** The OR result is 7.

## 12. Bitwise OR: 2 OR 5

**Aim:** To perform a bitwise OR operation on two and five.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 2
    OR AL, 5
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
7
```

**Result:** The OR result is 7.

## 13. Bitwise XOR: 5 XOR 3

**Aim:** To perform a bitwise XOR operation on five and three.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 5
    XOR AL, 3
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
6
```

**Result:** The XOR result is 6.

## 14. Bitwise XOR: 7 XOR 3

**Aim:** To perform a bitwise XOR operation on seven and three.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 7
    XOR AL, 3
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
4
```

**Result:** The XOR result is 4.

## 15. Bitwise NOT: FC hex

**Aim:** To perform a bitwise NOT operation on the eight-bit hexadecimal number FC and display the result in decimal.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 0FCH
    NOT AL
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
3
```

**Result:** The NOT result is 3 in decimal (03H).

## 16. Bitwise NOT: FA hex

**Aim:** To perform a bitwise NOT operation on the eight-bit hexadecimal number FA and display the result in decimal.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 0FAH
    NOT AL
    ADD AL, 30H
    MOV DL, AL
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
5
```

**Result:** The NOT result is 5 in decimal (05H).

## 17. Check whether 6 is even

**Aim:** To check whether six is even. Display one if even; otherwise, display zero.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 6
    TEST AL, 1
    JZ EVEN

    MOV DL, '0'
    JMP DISPLAY

EVEN:
    MOV DL, '1'

DISPLAY:
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
1
```

**Result:** Six is even.

## 18. Check whether 7 is odd

**Aim:** To check whether seven is odd. Display one if odd; otherwise, display zero.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 7
    TEST AL, 1
    JNZ ODD

    MOV DL, '0'
    JMP DISPLAY

ODD:
    MOV DL, '1'

DISPLAY:
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
1
```

**Result:** Seven is odd.

## 19. Smaller of 3 and 7

**Aim:** To compare three and seven and display the smaller number.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 3
    MOV BL, 7
    CMP AL, BL
    JBE SMALLER

    MOV DL, BL
    JMP DISPLAY

SMALLER:
    MOV DL, AL

DISPLAY:
    ADD DL, 30H
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
3
```

**Result:** The smaller number is 3.

## 20. Smaller of 8 and 4

**Aim:** To compare eight and four and display the smaller number.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 8
    MOV BL, 4
    CMP AL, BL
    JBE SMALLER

    MOV DL, BL
    JMP DISPLAY

SMALLER:
    MOV DL, AL

DISPLAY:
    ADD DL, 30H
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
4
```

**Result:** The smaller number is 4.

## 21. Greater of 3 and 7

**Aim:** To compare three and seven and display the greater number.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 3
    MOV BL, 7
    CMP AL, BL
    JAE GREATER

    MOV DL, BL
    JMP DISPLAY

GREATER:
    MOV DL, AL

DISPLAY:
    ADD DL, 30H
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
7
```

**Result:** The greater number is 7.

## 22. Greater of 8 and 4

**Aim:** To compare eight and four and display the greater number.

**Program:**

```asm
.MODEL SMALL
.STACK 100H
.CODE
MAIN PROC
    MOV AL, 8
    MOV BL, 4
    CMP AL, BL
    JAE GREATER

    MOV DL, BL
    JMP DISPLAY

GREATER:
    MOV DL, AL

DISPLAY:
    ADD DL, 30H
    MOV AH, 02H
    INT 21H

    MOV AH, 4CH
    INT 21H
MAIN ENDP
END MAIN
```

**Output:**
```text
8
```

**Result:** The greater number is 8.

---

## How to Execute in MASM and DOSBox

1. Save each program in a separate `.ASM` file, for example `P01.ASM`.
2. Open DOSBox and mount the folder containing your files.
3. Assemble the program:

   ```text
   MASM P01.ASM;
   ```

4. Link the object file:

   ```text
   LINK P01.OBJ;
   ```

5. Run the executable:

   ```text
   P01.EXE
   ```

**Note:** All programs display a single decimal digit, so adding `30H` converts the result to its ASCII digit. For the NOT programs, the result is first complemented as an eight-bit value; `FC` becomes `03H`, and `FA` becomes `05H`.
