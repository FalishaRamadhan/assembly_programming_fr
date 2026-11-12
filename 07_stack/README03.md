# Program 03


##  Program Execution

Execution starts at `_start`:

```asm
_start:
    mov rax, 10
    call calculate
```

First, the value 10 is loaded into RAX.

The CALL instruction then transfers execution to the `calculate` procedure.

Before transferring control, CALL pushes the return address onto the stack.

The return address identifies the instruction immediately following CALL.

Because this is a 64-bit program, the return address occupies 8 bytes.

RSP decreases by 8 bytes.

##  Executing the Procedure

Execution continues at:

```asm
calculate:
    add rax, 5
    ret
```

The ADD instruction adds 5 to the existing value in RAX.

Therefore:

RAX = 10 + 5 = 15.

The RET instruction retrieves the saved return address from the stack.

RSP increases by 8 bytes, and execution returns to the instruction immediately following CALL.

##  Returning to the Main Program

Execution continues at the `after_call` label:

```asm
after_call:
    nop
```

At this point, RAX contains 15.

The NOP instruction performs no operation and does not change the stack pointer.

The program then executes:

```asm
mov rax, 60
xor rdi, rdi
syscall
```

These instructions terminate the program using the Linux 64-bit exit system call.

##  Observations From Testing

- CALL pushes a return address onto the stack.
- RSP decreases by 8 bytes when CALL executes.
- The calculate procedure adds 5 to RAX.
- RAX changes from 10 to 15.
- RET retrieves the saved return address.
- RSP returns to its original position after RET.
- Execution resumes immediately after the CALL instruction.
- The program produces no terminal output.
