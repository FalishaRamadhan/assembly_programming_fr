# Program 04
##  Program Execution

Execution begins at `_start`:

```asm
_start:
    call work
```

The CALL instruction transfers execution to the `work` procedure.

Before transferring control, CALL pushes the return address onto the stack.

Since this is a 32-bit program, the return address occupies 4 bytes.

ESP decreases by 4 bytes.

##  Creating the Stack Frame

Inside the `work` procedure:

```asm
push ebp
mov ebp, esp
sub esp, 8
```

**Step 1: PUSH EBP**

The previous value of EBP is saved onto the stack.

ESP decreases by 4 bytes.

**Step 2: MOV EBP, ESP**

EBP is updated to point to the current stack position.

It becomes the reference point for accessing local variables.

**Step 3: SUB ESP, 8**

The program reserves 8 bytes of memory for two local variables.

ESP decreases by another 8 bytes.

## 4. Storing and Accessing Local Variables

The program executes:

```asm
mov dword [ebp - 4], 100
mov dword [ebp - 8], 200
```

- The value 100 is stored at EBP - 4.
- The value 200 is stored at EBP - 8.

Each variable occupies 4 bytes.

The values are then retrieved:

```asm
mov eax, [ebp - 4]
mov ebx, [ebp - 8]
```

- EAX receives 100.
- EBX receives 200.

The EBP register remains unchanged during these operations.

##  Restoring the Stack

The program executes:

```asm
mov esp, ebp
pop ebp
ret
```

**MOV ESP, EBP**

ESP is restored to the position held by EBP, releasing the 8 bytes reserved for local variables.

**POP EBP**

The previous EBP value is retrieved from the stack.

ESP increases by 4 bytes.

**RET**

RET retrieves the return address saved by CALL and transfers execution back to `_start`.

ESP returns to its original position.


##  Observations From Testing

- CALL saves the return address on the stack.
- PUSH EBP saves the previous frame pointer.
- EBP provides a stable reference for accessing local variables.
- SUB ESP, 8 reserves memory for two 4-byte variables.
- ESP decreases as stack space is allocated.
- MOV ESP, EBP releases the allocated local memory.
- POP EBP restores the previous frame pointer.
- RET returns execution to the calling section.
- The program produces no terminal output.
