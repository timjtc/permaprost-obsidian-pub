---
id: NO-L20240119100338381
aliases:
  - NCP2201 Module 1 - Introduction and Top-level View of Computer Function and Interconnection
---
# Ideas

## Fundamentals of Computer Architecture and Organization

**Computer architecture** refers to attributes of the computer system that directly impacts the logical operation or execution of a program. It answers the question “what?” when creating a functional computer. E.g. What instructions must be implemented? What components (registers, buffers, etc.) must exist or be used for the instructions to work? This is somehow similar to architectural design, it ideates what rooms should be built and what building materials are to be used.
**Computer architecture** is identical with the term **instruction set architecture (ISA)**.

**Computer organization** refers to how an architecture is implemented. It answers the question “how?”. E.g. How is it executed (does it have a multiply instruction or through a looped addition)? How is everything interfaced together? How will the CPU fetch the data on that address? In analogy to architecture, it defines which rooms are adjacent to each other and how are they interconnected with hallways.

In each level of abstraction and whenever you either "zoom in" or "zoom out" to see the individual components that comprise something or vice versa, there will always be a hierarchal pattern of **structure** and **function** in each level in which a designer must be concerned with:
	**Structure**: The way in which the components are interrelated.
	**Function**: The operation of each individual component as part of the structure.
## Control Unit

**Registers** are small fast storage or memory units that holds the data the CPU is currently working on.

**Program counter** (PC) - keeps track of the next instruction to be fetched
**Instruction register** (IR) - temporary memory where the next instruction is loaded
**Memory address register** (MAR) - stores the address that points to where the next read or write operation will occur in memory
**Memory buffer register** (MBR) - stores the data that will be written to memory or the data that was read from memory
**Accumulator** (ACC) - temporary memory where operation results are stored

*MAR and MBR are like key-value pairs.*
## Instruction Cycle (Fetch-Execute)

In each clock tick, the computer goes through one step of the instruction cycle.
	**Fetch**: Load the next instruction specified in PC into the IR.
	**Execute**: Execute the opcode in IR and either read or write to the specified memory address.

The MAR and MBR might come into play when a **Decode** step in-between **Fetch** and **Execute** is visualized, where **Decode** will interpret the opcode and store the address specified after it into the MAR. Now when **Execute** happens, the opcode will be executed, an operation (logical, arithmetic, etc) will happen on the ACC if necessary, and data will be stored into the MBR if there is an output. The component responsible for writing and reading into the memory through a bus will either read whatever the MAR points to and store it into the MBR, or write into wherever the MAR points to with data in the MBR if it's a write operation.

## Bus

Since the bus is shared among many devices, control of the bus must be arbitrated in some way.
	**Centralized arbitration** - a single arbiter (could be a part of the CPU itself) decides who uses the bus to exchange bits and when.
	**Distributed arbitration** - each module or component has independent control logic for taking over the bus with a defined priority.
# Sources

[[NO-F20240118J#^2]] 1500H-1630H lecture by Dr Joan P Lazaro ^lazaroJ-202401181500-icao

[The Fetch-Execute Cycle: What's Your Computer Actually Doing? (youtube.com)](https://www.youtube.com/watch?v=Z5JC9Ve1sfI) ^tomscott-20190729-Z5JC9Ve1sfI