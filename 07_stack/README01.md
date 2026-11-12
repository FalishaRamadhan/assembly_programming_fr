# Program 01



## Program Execution

Execution begins at the `_start` label.

First, two values are loaded into registers:

```asm
mov rax, 100
mov rbx, 200
```

- RAX stores 100.
- RBX stores 200.

Next, the values are pushed onto the stack:

```asm
push rax
push rbx
```

Each PUSH operation decreases RSP by 8 bytes because this is a 64-bit program.

Assuming the initial stack pointer is S:

- After `push rax`, RSP = S - 8.
- After `push rbx`, RSP = S - 16.

The stack now contains:
- Top of stack: 200
- Next value: 100

The `nop` instruction executes without changing registers or the stack.

##  Retrieving Values From the Stack

The program then executes:

```asm
pop rcx
pop rdx
```

The first POP retrieves 200 into RCX.

The second POP retrieves 100 into RDX.

Each POP increases RSP by 8 bytes.

Therefore:

- After `pop rcx`, RSP = S - 8.
- After `pop rdx`, RSP = S.

The original stack pointer is restored.



## Observations From Testing

- The program demonstrates the LIFO principle.
- PUSH decreases RSP by 8 bytes per operation.
- POP increases RSP by 8 bytes per operation.
- The last value pushed (200) is retrieved first.
- After both POP operations, RSP returns to its original position.
- The program does not display output because it contains no printing instructions.

