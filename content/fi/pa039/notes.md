----
url: pa039/01
title: notes 01
date 2022-05-05
---


# CISC
Size and speed of memory
CISC directly supports compilers
Rich addressing modes
Complex instruction == microprogram
Microinstructions: decomposition to simpler instructions

Disadvantages:
 - too complex instructions
 - increasingly complex
 - instruction analysis
 - cross instruction relationships
 - backward compatibility cost (within a family)


# Performance increase

Clock cycles define processor’s performance
Solution: parallelization

# Pipelining

five-stage pipelining:
 - Instruction Fetch instruction is loaded from a memory
 - Instruction Decode instruction is decoded (recognized)
 - Operand Fetch operands are ready (fetched from registers and/or memory)
 - Execute instruction is executed
 - Writeback results are written back

Individual stages are processed in parallel, shifted by one stage


# Pipelines and memory

“Invisible” pipelines: Reading (writing) from (to) memory is moved ahead of the actual instruction that works with the data

“Visible” pipelines: Explicit instructions, with know number of cycles to complete e.g.g intel 80860

# RISC

Architecture removed the speed of memory access bottleneck

- Introduction of caches
- Dramatic decrease in the memory cost paralleling increase of memory size
- Better pipelining
- Improved compilers
- All instructions of the same size/length
- Simple addressing
- Load/Store architecture
- Sufficient number of internal registers
- “Delayed’ branches

Problem: stall when waiting for a next instruction execution finalization (too complex relationship between instructions, microcode, ...)

First generation RISC ideal: One instruction finished per each clock tick

Reality nowadays: Several instructions graduated in a single clock tick

# Superscalar processors

- Multiple processing units: Arithmetic (ALU), Floating point (FPU) and other
- Parallelism in a hardware: Sequential programs, “Automatic” parallelization, MADD (Multiply Add)


# Superpipeline

- Another circuits simplification
 - More extensive pipeline decomposition
 - Faster execution of individual stages
- resulting in faster processing
 - A different form of parallelism
- These pipelines also called deep pipelines
 - 16 and more stages
 - instructions use only some of the whole set of stages

# VLIW

- Analogy of superscalar processors (many units)
- Parallelization under compiler control
 - Increased complexity of compilers
 - Simplified hardware leads to higher performance
 - Decision which instructions can be run in parallel taken by the compiler
- Advantages:
 - Simpler instructions
 - No complex control hardware needed
 - Lower energy consumption (at least a potential for it)


# RISC – additional features
- Register’s bypass
- Register’s renaming
- Branches
 - null operation
 - conditional assignment `(a = b<c ? d : e;)`
 - multiple pre-fetch from memory
 - buffer of potential branch targets
 - branch prediction: static (compiled) or dynamic


# ANDES

Architecture with Non-sequential Dynamic Execution Scheduling

Also called out-of-order execution (OoOE) or dynamic execution

Foundations:
 - Waiting for data causes a slowdown
 - Dynamic parallelism can help

Multiple instructions queues:
- a queue for fixed point (arithmetic and logic) instructions
- an address queue for Load/Store instructions
- a queue for floating point instructions

Independent pipeline for each queue

Features:
 - readiness decides which instructions are executed
 - the original order of instructions in the program is not kept
 - instruction graduation guarantees restoration of the original order


## Additional properties

- Speculative branches
 - execution continues through predicted branch
 - does not wait for the result of the actual branch instruction
- Non-blocking Load/Store instructions
- Register renaming
 - Just part revealed (to a complier)
 - Multiple versions of the “same” register
 - Allows new data to be taken to a register “blocked” by a not yet finished execution of another instruction

## Summary

- Instead of waiting for memory access, other instructions are executed
- Internally changes the program order of instructions to the data order
 - instructions are executed when their operands are ready (in registers)
 - the original program order is not relevant

Avoids (or at least reduces) stalling of execution

Speculates on branches or even takes both branches in parallel (Only one branch graduates)

Complex circuitry, higher power consumptions


# Memory

Memory organization:
 - rows and columns (a 2D matrix)
 - address has two parts
 - page mode – a block or continuous bytes (the “row”) is read in one shot
 
## Memory Features
 - Memory access time - access row plus access column plus access (read or write) data
 - Memory cycle time - defines how often we can read data from a memory
 - Both depends on type of the memory (static or dynamic)
 

# Virtual Memory

Physical vs. logical address: More address spaces

Translation Lookaside Buffer (TLB):
- translates logical addresses to their physical equivalent
- a part of processor hardware
- TLB can have misses like any other cache

Virtual memory and supercomputers
- usually not used in specialized architectures
- now common due to the synergic architecture (clusters)


# Cache

- Size: several kB to tens of MB
- Organization: fixed length rows (16–128 bytes)
- Types: direct mapped, set-associative, fully-associative
- Hit ratio

# Memory Architectures

Harvard Memory Architecture: separated memory for data and instructions
Programmable cache: cache directly controlled at some superscalar processors


# Direct mapped cache 

- Static mapping: each cache row can keep only pre-defined memory rows
- Fast
- Simple circuits
- Potentially inefficient: used data may map to a single cache row

# Fully associative cache

Dynamic mapping
 - associative memory
 - each row in a cache knows where data lie in the main memory
 - access to cache goes to all rows
 - need to select a row for invalidation
Very efficient
Very complex circuits – expensive

# Set associative cache

- Sets of direct addressable caches
- Combination of positive properties of the previous cases
- Not full associativity (cheaper)
- Still options where a memory row can be stored

# Width of data flow

Bandwidth = maximal throughput of a memory system Bps
Throughput is not the same among all components
 - Processor – registers – cache – main memory – external memory

Latency: Time between the request and the actual data delivery (Extremely important esp. when moving small data chunks)

# Interleaved Memory

- The whole memory split to smaller blocks
  - Consecutive addresses mapped to different blocks
  - Allows immediate access
- 2–8 way interleaved memories common
- Higher latency

# Re-ordering of memory accesses

- ANDES predecessor
- Minimization of consecutive accesses to the same memory bank
- Run-time check on Load and Store interdependencies


# Multiprocessor systems

- Scaling ratio (number of sockets) for symmetric memory
- Distributed memory
- Clusters with huge number of multiprocessor nodes















