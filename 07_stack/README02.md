# Program 02


## Program Execution

Execution begins at `_start`:

```asm
_start:
    call work
```

The CALL instruction transfers execution to the `work` procedure.

Before transferring control, CALL pushes the return address onto the stack.

Since this is a 64-bit program, the return address occupies 8 bytes.

Therefore:

RSP = S - 8

where S represents the original stack pointer.

## 3. Creating the Stack Frame

Inside the `work` procedure, the following instructions execute:

```asm
push rbp
mov rbp, rsp
sub rsp, 16
```

**Step 1: PUSH RBP**

The previous value of RBP is saved on the stack.

RSP decreases by 8 bytes.

**Step 2: MOV RBP, RSP**

RBP is updated to point to the current stack position.

This establishes the base of the new stack frame.

**Step 3: SUB RSP, 16**

The program reserves 16 bytes of memory for local variables.

RSP decreases by another 16 bytes.

##  Storing Local Variables

The program stores two values:

```asm
mov qword [rbp - 8], 100
mov qword [rbp - 16], 200
```

- The value 100 is stored at RBP - 8.
- The value 200 is stored at RBP - 16.

Each variable occupies 8 bytes.

The values are then retrieved:

```asm
mov rax, [rbp - 8]
mov rbx, [rbp - 16]
```

- RAX receives 100.
- RBX receives 200.

RBP remains unchanged while these variables are accessed.

## Restoring the Stack Frame

The program executes:

```asm
mov rsp, rbp
pop rbp
ret
```

**MOV RSP, RBP**

This releases the 16 bytes reserved for local variables by restoring RSP to the frame pointer position.

**POP RBP**

The previous RBP value is restored from the stack.

RSP increases by 8 bytes.

**RET**

RET retrieves the return address saved by CALL and transfers execution back to `_start`.

RSP returns to its original position.

## Program Termination

After returning from `work`, execution continues with:

```asm
mov rax, 60
xor rdi, rdi
syscall
```

This invokes the Linux 64-bit exit system call with status zero.

## Observations From Testing

- CALL automatically saves the return address on the stack.
- PUSH RBP saves the previous frame pointer.
- RBP provides a stable reference for accessing local variables.
- SUB RSP, 16 reserves space for two 8-byte local variables.
- MOV RSP, RBP releases the reserved local memory.
- POP RBP restores the previous frame pointer.
- RET returns execution to the calling location.
- The program produces no terminal output.
