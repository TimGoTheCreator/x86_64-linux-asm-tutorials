# Hello World In X86_64 Assembly

Before we start writing our Hello World program in Assembly, we need to find out how to call system calls in Linux.
Assembly programs usually use syscalls to communicate with the Kernel (OS), syscalls have calls for writing, reading, exiting the program,
and more.


# Linux X86_64 Assenbly Syscall Structure
| Instruction       | Syscall #     | Return value  | arg0  | arg1  | arg2 | arg3 | arg4 | arg5 |
|-------------------|---------------|---------------|-------|-------|------|------|------|------|
|SYSCALL            | RAX           | RAX           | RDI   | RSI   | RDX  | R10  | R8   | R9   |

### Structure
- `RAX` - To store system call number and return value (if there is a value).
- `RDI` - To store 0th argument to pass while **invoking a syscall**.
- `RSI` - To store 1st argument to pass while **invoking a syscall**.
- `RDX` - To store 2nd argument to pass while **invoking a syscall**.
- `R10` - To store 3rd argument to pass while **invoking a syscall**.
- `R8`  - To store 4th argument to pass while **invoking a syscall**.
- `R9`  - To store 5th argument to pass while **invoking a syscall**.

Syscalls and arguements are very complex, so you would need to refer to the Linux Syscall Table:
    [Linux System Call Table](https://filippo.io/linux-syscall-table/)

Hello World in X86_64 Linux Assembly:

```asm
BITS 64

section .data
  msg db "Hello World", 0xA
  len equ $ - msg

section .text

global _start

_start:
  mov rax, 1
  mov rdi, 1
  mov rsi, msg
  mov rdx, len
  syscall
  mov rax, 60
  xor rdi, rdi
  syscall
```

Its also located in `code-snippets/hello-world.asm` if you want to run it yourself.

# Explanation of the Above code (by line number)

- 1. `BITS 64`- specifies to nasm how many bits our system is.
- 2. `section .data` - Defines the **data section**,
        - In there, we can put static data, like strings or constants that we will use in the program.
- 3. `msg db "Hello World", 0xA` - Makes a data type called msg with "Hello World" in it, 0xA means 0x0A (Newline, aka \n).
        `- ` stands for `Define Byte`, used to allocate a sequence of bytes or a single Byte in memory.
- 4. `len equ $ - msg` - Automatically determines the length of the datatype, the last specified arguement `msg` calls the `msg` variable we made earlier.
- 5. `section .text` - This is where we write code, _start: (like C's main() ) has to be inside it.
- 6. `global _start` - Declares `_start` as global.
- 5. `_start:` - Definition of the `_start:` label.
   - A `label` defines a location in the code and are used to name specific points in the code.
   - The label itself, infact, does not execute any code at all. the code following it does.
- 6. `mov rax, 1` - Moves value 1 (system call number for `sys_write`) into rax register.
- 7. `mov rdi, 1` - Moves value 1 (file descriptor for `stdout`) into rdi register.
    - 0 for `stdin, standard input`
    - 1 for `stdout, standard output`
    - 2 for `stderr, standard error output`
- 8. `mov rsi, msg` - Moves the base address of the data we want to write into rsi, `msg` in this case.
- 9. `mov rdx, len` - Moves the base of the adress of the data we want to write into rdx, which is `len` in this case
    - Aka the length of "Hello World"
- 10. `syscall` - Sends the Syscall to the Kernel/OS, from what we defined earlier.
- 11. `mov rax, 60` - Moves value 60 (system call number for `sys_exit`) into rax register.
- 12. `xor rdi, rdi` - Moves value 0 into rdi, the xor instruction sets rdi to 0.
    - Alternative is: `mov rdi, 0`
    - Optional information about 'mov rdi, 0' and 'xor rdi, rdi':
      
          The difference between 'mov rdi, 0' and 'xor rdi, rdi' is 'mov rdi, 0' stores a bigger value (64bit)
            and 'xor rdi, rdi' stores a shorter instruction (less binary size)
              example 'mov rdi, 0' bytes:
                                  '48 C7 C7 00 00 00 00'
                example 'xor rdi, rdi' bytes:
                                  '48 31 FF'
                in general x86, 'xor rdi, rdi' is preferred.
- 13. `syscall` - Sends the Syscall to the Kernel/OS, from what we defined earlier.

# Assembling And Linking The Program

To assemble the file we made, `hello-world.asm` we convert it to an object file `hello-world.o`
```bash
nasm -f elf64 hello-world.asm -o hello-world.o
```

To link the object file `hello-world.o` into an executable file `hello-world`
```bash
ld hello-world.o -o hello-world
```
