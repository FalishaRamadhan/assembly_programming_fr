# Program 05
##  Program Execution

Execution begins at `_start`.

The program first initializes two registers:

```asm
mov rax, 0x1122334455667788
mov rbx, 0x1234
```

- RAX receives the 64-bit hexadecimal value 0x1122334455667788.
- RBX receives the hexadecimal value 0x1234.

These values are initially stored in CPU registers.

##  Pushing Values Onto the Stack

The program executes:

```asm
push rax
push rbx
```

The first PUSH stores the value in RAX on the stack.

RSP decreases by 8 bytes.

The second PUSH stores the value in RBX.

RSP decreases by another 8 bytes.

Assuming the original stack pointer is S:

- After PUSH RAX: RSP = S - 8.
- After PUSH RBX: RSP = S - 16.

The stack now contains:

- Top of stack: 0x1234.
- Next value: 0x1122334455667788.

The NOP instruction executes without changing the stack.

##  Popping Values From the Stack

The program executes:

```asm
pop rbx
pop rax
```

The first POP retrieves the most recently pushed value into RBX.

RBX receives 0x1234.

RSP increases by 8 bytes.

The second POP retrieves the earlier value into RAX.

RAX receives 0x1122334455667788.

RSP increases by another 8 bytes.

The original stack pointer is restored.

## Program Termination

The program executes:

```asm
mov rax, 60
xor rdi, rdi
syscall
```

This invokes the Linux 64-bit exit system call with status zero.

##  Observations From Testing

- The program uses 64-bit registers.
- Each PUSH operation decreases RSP by 8 bytes.
- Each POP operation increases RSP by 8 bytes.
- The stack stores values in LIFO order.
- RBX receives its original value first because it was pushed last.
- RAX receives its original value second.
- The original stack pointer is restored after both POP operations.
- The program produces no terminal output.
