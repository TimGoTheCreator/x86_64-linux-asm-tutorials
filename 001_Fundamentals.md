# Introduction To Computer Architecture

In this tutorial, we will go over the basics of computer architecture, starting from fundamental concepts like:

- Processors (CPU - Central Processing Unit)
- Memory
- Endianness

# What is computer architecture?
Computer architecture refers to the structure of the computer, it defines the systems performance, capabilities, and other interactions
The key three important components is:
- Processor
- Memory (Storage / RAM)
- IO/OS

# What is Memory?

Memory in a system categorized in two types:
- Primary ram (Random Memory Access - RAM)
    - Temporarily stores data that is being used.
    - Fast to access (Slower than registers but faster than storage).
    - It is Volatile.
    - All the data that is stored in RAM will be lost after the system shuts down, as it is temporary.
    - When we say "Memory" we often mean RAM, unless we are talking about Reading/Writing on Disk.

- Secondary Memory (Storage)
    - Stores data permanently.
    - Slow to access.
    - It is Non-Volatile compared to RAM.
    - All the data persists even after turning off the system.
    - All the data that is currently being used is loaded into RAM from secondary storage.
    - Example of Secondary storage programs being loaded in RAM:
        The program is on the Secondary storage.
        When the program is run, it puts itself into RAM, as well it's assets
    - Example of Secondary Memory:
        HDD, SSD, Compact Drives, Flash Drives, ETC.

# What is Endianness?

Endianness refers the order in which bytes (or 8 bits, (byte = 8 bits)) are stored or transmitted in memory.
It is crucial to understand how data is represented in assembly and how the CPU accesses/handles multiple-byte types.
There are two key types of Endianness:

### Big-Endian
- The least significant byte (small-end) is located at the highest memory address.
- The most significant byte (big-end) is located at the smallest memory address.
- For example: if we have a 32 bit integer 0x12345678 it would be stored in the memory as:

        | memory address | value stored at the address |
        |----------------|-----------------------------|
        |0x00            | 12                          |
        |0x01            | 34                          |
        |0x02            | 45                          |
        |0x03            | 56                          |
        |0x04            | 78                          |

### Little-Endian
- The least significant byte (small-end) is located at the smallest memory address.
- The most significant byte (big-end) is located at the highest memory address.
- For example: if we have a 32 bit integer 0x12345678 it would be stored in the memory as:

        | memory address | value stored at the address |
        |----------------|-----------------------------|
        |0x00            | 78                          |
        |0x01            | 56                          |
        |0x02            | 34                          |
        |0x03            | 12                          |
