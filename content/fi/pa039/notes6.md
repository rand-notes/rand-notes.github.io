---
url: /pa039/06
title: notes 6
date: 2022-05-05
---


# What makes GPU powerful?

- Parallelism types
 - Task parallelism
  - the problem is decomposed to parallel tasks
  - tasks are typically complex, they can perform different jobs
  - complex synchronization
  - best for lower number of high-performance processors/cores
 - Data parallelism
  - the parallelism on a level of data structures
  - typically the same operation on multiple elements of a data structure
  - can be executed on simpler processors
- Programmer point of view
 - some problems are more task-parallel, some more data-parallel (tree traversal vs. vector addition)
- Hardware designer point of view 
 - processors for data-parallel computations can be simpler
 - so we can get more arithmetic power per square centimeter
 - simpler memory access patterns allows to create a memory with higher bandwidth


# CPU vs GPU

- hundreds ALU in tens of cores vs. tens of thousands ALU in tens of multiprocessors
- out-of-order vs. in-order
- MIMD, SIMD for short vectors vs. SIMT for long vectors
- big cache vs. small cache, often read-only

GPUs use more transistors for ALUs than for cache and instruction control => higher peak performance, less universal

# High-end GPU
- co-processor with dedicated memory
- asynchronous instructions execution
- connected via PCI-E to the rest of the system

# CUDA (Compute Unified Device Architecture)

- architecture for parallel computations developed by NVIDIA
- a programming model allowing to implement general programs on GPUs
- can be used with multiple programming languages

# C for CUDA

- explicit separation of a host (CPU) and a device (GPU) code
- threads hierarchy
- memory hierarchy
- synchronization mechanisms
- API (context manipulation, memory, errors handling etc.)

# Threads hierarchy
- threads are organized into thread-blocks
- thread-blocks creates a grid
- a computational problem is typically decomposed into independent sub-problems, solved by thread-blocks
- subproblems are further parallelized and solved by (potentially collaborating) threads
- ensures good scaling


# Memory hierarchy
Multiple types of memory
- differ visibility
- differ in life-time
- differ in latency and bandwidth

# C for CUDA

The syntax of C is extended by function type quantifiers, determining from where the function can be called and where it is executed
- __device__ function is executed on device (GPU) and called from device code
- __global__ function is executed on device and called from host (CPU)


# Example – vector addition

For complete computation of vector addition, we need to:
- allocate memory for the vectors, and fill it with some data
- allocate GPU memory
- copy vectors a and b to GPU memory
- compute vector addition on GPU
- copy back the result from GPU memory into c

Kernel execution:
- the kernel is called as a C-function; between the name and the arguments, there are triple angle brackets with specification of grid and block size
- we need to know block size and their count
- we will use 1D block and grid with fixed block size
- the size of the grid is determined in a way to compute the whole problem of vector sum

# GPU memory management

We use managed memory, so CUDA automatically copies data between CPU and GPU.
- memory coherency is automatically ensured
- we cannot access managed memory while any GPU kernel is running

# Thread-local memory

Registers:

- the fastest memory, directly used by instructions
- local variables and intermediate results are stored into registers
 - if there is enough registers 
 - if compiler can determine array indexes in compile time
- life-time of a thread

Local memory
 - what cannot fit into registers, goes to the local memory
 - physically stored in global memory, have longer latency and lower bandwidth
 - life-time of a thread

# Block-local memory

Shared memory
- the speed is close to registers
- can have dynamic size (determined during kernel execution), if declared as extern without specification of the array size
- life-time of a thread block

# GPU-local memory
Global memory
- order-of-magnitude lower bandwidth compared to the shared memory
- latency in hundreds of GPU clocks
- coalesced access necessary for efficient access
- life-time of an application
- can be cached (depending on GPU architecture)

# Other memories

- constant memory
- texture memory
- system memory

# Thread-block-scope synchronization

- native barrier
- has to be visited by all threads within a thread-block
- only one instruction, very fast if not reduce parallelism

# Atomic operations

- perform read-modify-write operations using shared or global memory
- no interference with other threads
- arithmetic and bitwise operations

# Synchronization of memory operations

Compiler can optimize access into shared and global memory by placing intermediate results into registers, and it can change order of memory operations

- threadfence() and threadfence block() can be used to ensure data we are storing are visible for others
- variables declared as volatile are always read/written from/to global or shared memory

# Thread-block synchronization
- global memory visible for all blocks
- but weak possibilities to synchronize between blocks
 - in general no global barrier (can be implemented if all blocks are persistent on GPU)
 - using atomic operations can solve some problems
 - generic global barrier only by kernel invocation
 - harder to program, but allows better scaling

# Global synchronization via atomic operations
Alternative implementation of vector reduction
- each thread-block reduces a subvector
- the last running thread-block adds results of all thread-blocks







