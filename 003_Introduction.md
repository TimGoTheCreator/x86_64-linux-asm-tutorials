# Introduction To Assembly (ASM) Language

Assembly language is a low-level language that provides direct control over hardware. It serves as an interface between high-level languages (like Python or C) and machine code (the binary code that the CPU understands).

## 1. What Is Assembly Language?
Assembly language consists of human-readable instructions mapped to machine code. Each line in an assembly program corresponds to an instruction the CPU can execute.

### 1.1 Machine Code vs Assembly
- **Machine Code**: Binary instructions directly executed by the CPU (e.g. `11001001 00000001`).
- **Assembly Code**: Human-readable representation of machine code using mnemonics (e.g. `MOV RAX, 1`).

### 1.2 Why Use Assembly?
- **Control**: Fine-grained control over the CPU.  
- **Efficiency**: Enables highly optimized programs.  
- **Learning Architecture**: Helps developers understand CPU, memory, and hardware interactions.  
- **Saying**: "If you know assembly, every piece of software is open source."

## 2. Assembly Language Structure
Assembly programs typically consist of three sections:

### 2.1 Data Section
Initialized data or constants stored in memory.  
Example:  
section .data  
msg db "Hello, world", 0xA

### 2.2 BSS Section
Uninitialized data reserved for later use.  
Example:  
section .bss  
buffer resb 64

### 2.3 Text Section
Executable code, usually starting with `global _start`.  
Example:  
section .text  
global _start

## 3. Assembly Language Syntax
Syntax depends on architecture (x86, ARM, etc). In x86_64:
- **Mnemonics**: CPU instructions (`MOV`, `ADD`, `PUSH`, `JMP`).  
- **Operands**: Registers, memory locations, or immediate values.  
- **Directives**: Instructions for the assembler/linker (`global`, `section`).  

Example: `MOV RAX, 1`

## 4. Registers
Registers are small, fast storage areas inside the CPU. On x86_64, registers are 64-bit.  
Types include: General Purpose (RAX, RBX, RCX, RDX), Index (RSI, RDI, RBP, RSP), Extended (R8–R15), and Instruction Pointer (RIP).  

## 5. Addressing Modes
Defines how operands are accessed: Immediate, Register, or Memory.  
Rules: register→register allowed, memory→register allowed, register→memory allowed, memory→memory not allowed.

## 6. Assembly Syntax Formats
Two common formats: Intel and AT&T.

### Intel Syntax
- Destination before source (`MOV dest, src`)  
- Registers without prefix (`RAX`)  
- Memory with square brackets (`[rax]`)  

### AT&T Syntax
- Source before destination (`MOV src, dest`)  
- Registers prefixed with `%`  
- Immediate values prefixed with `$`  
- Memory with parentheses (`(%rax)`)  

### Key Differences
| Feature          | Intel Syntax        | AT&T Syntax         |
|------------------|---------------------|---------------------|
| Operand order    | Dest, Source        | Source, Dest        |
| Register names   | Plain               | `%` prefix          |
| Memory access    | `[rax]`             | `(%rax)`            |
| Immediate values | No prefix           | `$` prefix          |
| Instruction size | Implied (`mov`)     | Explicit (`movq`)   |

### Switching Syntax
- NASM: Intel syntax only.  
- GAS: Defaults to AT&T, switch with `.intel_syntax` or `-masm=intel`.  
- GDB: Switch with `set disassembly-flavor intel` or `set disassembly-flavor att`.
