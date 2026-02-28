# Setting Up The Environment For Assembly Programming

Before we start coding in Assembly, we need to set up our enviromnent.
This section will guide you through the process of installing the neccesary tools required to write and assemble a assembly program.
We will use 'NASM', short for 'Netwide Assembler' and 'GNU LD' linker to link it.

The Netwide Assembler (NASM) is a popular and widely used assembler for x86 and x86_64 assembly programming.
To install it, you need to open Bash which is usually opened with ctrl-alt-c on Linux distros.

```bash
sudo apt install nasm binutils
```

After you've installed it, you can verify it with:

```bash
nasm -v
```

# Installing a Debugger

To install a assembly debugger, you can download 'GNU gdb', to install it:
```bash
sudo apt install gdb
```

After you've installed it, you can vrrify it with:

```bash
gdb -v
```