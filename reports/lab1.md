# Lab 1

## Question 1

`RustSBI`: `0.3.0-alpha.4`
`RISC-V SBI`: `v1.0.0`

`Bad Address`

When the program goes to U-mode, and tries to access nullptr, PageFault will be raised.

`Bad Instruction`

When the program is in U-mode and tries to access a restricted instruction (here is a S-mode instruction),
IllegalInstruction will be raised.

`Bad Register`

When the program is in U-mode and tries to access a restricted register, IllegalInstruction will be raised.

## Question 2

1. `sp` refers to the stack pointer pointed to the kernal stack. `__restore` can be called to init an app, or goes back
   to U-mode after handling trap.
2. Loads the `sstatus`, `sepc`, `sscratch`. `sstatus` is the cpu status, `sepc` is the program counter, `sscratch` is
   the backup of the kernal stack pointer. They are saved to go back to the kernal when next trp is triggered.
3. `x2` is already saved by `sscratch` and `x4` is not used.
4. After this instruction, `sp` is the kernal stack pointer and `sscratch` is the user stack pointer.
5. `sret`. This instruction sets the privilege bit of `sstatus.spp` to U-mode.
6. After this instruction, `sp` is the user stack pointer and `sscratch` is the kernal stack pointer.
7. When trap or interrupt occurs.
