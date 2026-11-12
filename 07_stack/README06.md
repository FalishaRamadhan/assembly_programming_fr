# Program 06

##  Program Execution

Execution begins at `_start`.

The program initializes two registers:

```asm
mov eax, 0x11223344
mov ebx, 0x1234
```

- EAX receives 0x11223344.
- EBX receives 0x1234.

These values are stored in the CPU registers before being transferred to the stack.

##  Pushing Values Onto the Stack

The program executes:

```asm
push eax
push ebx
```

The first PUSH stores the value in EAX onto the stack.

ESP decreases by 4 bytes.

The second PUSH stores the value in EBX.

ESP decreases by another 4 bytes.

Assuming the original stack pointer is S:

- After PUSH EAX: ESP = S - 4.
- After PUSH EBX: ESP = S - 8.

The stack now contains:

- Top of stack: 0x1234.
- Next value: 0x11223344.

The NOP instruction executes without changing the stack.

## Popping Values From the Stack

The program executes:

```asm
pop ebx
pop eax
```

The first POP retrieves the most recently pushed value into EBX.

EBX receives 0x1234.

ESP increases by 4 bytes.

The second POP retrieves the earlier value into EAX.

EAX receives 0x11223344.

ESP increases by another 4 bytes.

The original stack pointer is restored.

## Program Termination

The program executes:

```asm
mov eax, 1
xor ebx, ebx
int 0x80
```

These instructions invoke the Linux 32-bit exit system call with status zero.

##  Observations From Testing

- The program uses 32-bit registers.
- Each PUSH operation decreases ESP by 4 bytes.
- Each POP operation increases ESP by 4 bytes.
- The stack follows the LIFO principle.
- EBX receives its original value first because it was pushed last.
- EAX receives its original value second.
- ESP returns to its original position after both POP operations.
- The program produces no terminal output.