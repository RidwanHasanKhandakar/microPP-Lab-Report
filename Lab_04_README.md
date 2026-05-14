# Lab Experiment 04 — 8086 Microprocessor: Printing a Name in an Emulator

## Student Information

| Field | Details |
|---|---|
| **Name** | Ridwan Hasan Khandakar |
| **ID** | 2310604 |
| **Section** | 03 |
| **Course Code & Title** | CSE216L — Microprocessor, Interfacing, and Assembly Language Lab |
| **Course Instructor** | Noor-E-Sadman |
| **Experiment No** | 04 |
| **Experiment Title** | 8086 Microprocessor: Printing "Ridwan-Hasan-Khandakar" in an Emulator |

---

## Objective

Use BIOS interrupts in an 8086 emulator to display a string (student's name) on the screen using assembly language.

---

## Tools Used

- 8086 Emulator (e.g., emu8086 or similar)
- BIOS Interrupt `INT 10h` with `AH = 13h` (Write String)

---

## Experiment Code

```asm
name: DB "Ridwan-Hasan-Khandakar"

start:
    mov ah, 0x13    ; BIOS interrupt function: Write String
    mov cx, 22      ; Length of the string
    mov bx, 0       ; Page number / attribute
    mov es, bx      ; Set ES segment
    mov bp, offset name ; Pointer to the string
    mov dl, 0       ; Column position
    int 0x10        ; Call BIOS video interrupt
    hlt             ; Halt the program
```

---

## Key Concepts

| Concept | Description |
|---|---|
| `INT 10h` | BIOS video service interrupt |
| `AH = 13h` | Write string function |
| `CX` | Holds the length of the string to display |
| `ES:BP` | Segment:Offset pointer to the string in memory |
| `HLT` | Halts CPU execution |

---

## Conclusion

This experiment demonstrated how BIOS interrupts can be used in an 8086 emulator to display a string on the screen. The program was modified to print the name "Ridwan-Hasan-Khandakar" by updating the data string and setting the `CX` register to the correct string length (22 characters). The experiment provided practical understanding of register usage, memory addressing with `ES:BP`, and how assembly programs interact with BIOS services to perform output operations.
