---
url: /pa039/05
title: notes 5
date: 2022-05-05
---

# Parallel programming

- Data parallelism
 - Identical instructions on different processors process different data
 - In principle the SIMD model (Single Instruction Multiple Data) - e.g. loop parallelization
- Task parallelism
 - MIMD model (Multiple Instruction Multiple Data)
 - Independent blocks (functions, procedures, programs) run in parallel
- SPMD
 - No synchronization at the level of individual instructions
 - Equivalent to MIMD
- Message passing targets SPMD/MIMD

# Before MPI
- Many competing message passing libraries:
 - Vendor specific/proprietary libraries
 - Academic, narrow specific implementations
- Different communication models
 - Difficult application development 
 - Need for “own” communication model to encapsulate the specific models
- MPI an attempt to define a standard set of communication calls


# Message Passing Interface

- Communication interface for parallel programs
- Defined through API
 - Standardized
 - Several independent implementations

# Programming model

- MPI designed originally for distributed memory architectures
- Currently supports hybrid models

# MPI Design Goals
- Portability
 - Define standard APIs
 - Define bindings for different languages
 - Independent implementations
- Performance
 - Independent hardware specific optimization
 - Libraries, potential for changes in algorithms
- Functionality
 - Goal to cover all aspects of inter-processor communication
- Library for message passing
- Designed for use on parallel computers, clusters and even Grids
- Make parallel hardware available for
 - users
 - library authors
 - tools and app developers

# MPI Initialization
- Create an environment
- Specify that the program will use the MPI libraries
- No explicit work with processes

# Identity
- Any parallel (distributed) program needs to know
 - How many processes are participating on the computation
 - Identity of “own” process
- MPI Comm size and MPI Comm rank 

# Work with messages

- Naive/primitive model
 - Process A sends a message: operation send
 - Process B receives a message: operation receive
- Lot of questions
 - How to properly specify (define) the data?
 - How to specify (identify) process B (the receiver)?
 - How the receiver recognises that the data are for it?
 - How a successful completion is recognised?

# Classical approach

- We send data as a byte stream
 - It is left to sender and receiver to properly setup and recognize data
- Each process has a unique identifier
 - We have to know identity of sender and receiver 
 - Broadcast operation
- We can specify some tag for the better recognitione.g. the message sequence number)
- Synchronization
 - Explicit collaboration between a sender and a receiver
 - It defines order of messages
- send and recv

# Deficiencies of the classical approach

- Insufficient level of data specification/definition
 - Heterogeneity between sender and receiver (incompatible representation)
 - Too many copies
 - Too much relies on a programmer
- Tags are global
 - Complication when you want to write independent libraries
- Collective operations
 - too many send/receive operations + not optimized, inefficient 


# MPI extensions
- Processes are grouped
- Each message is defined within a specific context (not only a tag)
 - Messages could be sent and received only within the same context
- Group and context jointly define communicator 
 - Tag is local to a specific communicator
- Default communicator MPI COMM WORLD
- Process identity (rank) is always defined within a specific context


# Data types

- Data are described by a triple (address, number, datatype)
- MPI Datatype is recursively defined as:
 - Pre-defined data type of the used language
 - Continuous array of MPI datatypes
 - Strided array of MPI datatypes
 - Indexed array of datatype blocks
 - Arbitrary datatype structure
- MPI provides functions to define own datatypes (row of a matrix which is stored column-wise)


# Tags

- Each message has an associated tag
 - Simplifies message recognition by the receiver
 - Tag is always defined within the used context (it is scoped)
- Receiver could specify which tag it expects
 - Alternatively it could ignore the tags (through MPI ANY TAG specification) 


# Point-to-point Communication

- Passing of a message between two processes
- Blocking / Non-blocking call (transmission)
 - Blocking – the call waits till the operation is finished
 - Non-blocking – the call just initiates the operation but does not wait till completion; the state of the data transfer must be tested independently
- Buffered / Un-buffered message passing
 - No buffer – message is passed directly without a buffer
 - MPI buffer – “transparent”, controlled directly by MPI
 - User buffer – controlled by the application (programmer)


# Communication modes
- Standard mode (Send)
 - Blocking call
 - MPI “decides”, if the MPI buffer is used
  - used → Send finishes when all data are in the buffer
  - not used → Send finishes when the data are accepted by the receiver
- Synchronous mode
 - Blocking call
 - Send finishes when the data were accepted by the receiver (processes synchronization)
- Buffered mode
 - Buffer provided by the application(programmer) 
 - Blocking or non-blocking – the operation finishes when the data are in the user buffer
- Ready mode
 - Receive must precede the actual send (Receive prepares the buffer), otherwise error

# Basic send operation

- Blocking send
 - MPI SEND
 - Triple (start, count, datatype) defines the message
 - dest identifies the receiver process, always relative to the used communicator comm
- Finishing the operation successfully means
 - All data were accepted by the system
 - The buffer is available for re-use
 - The receiver may not yet receive the data

# Basic receive operation
- Blocking operation
 - MPI RECV(start, count, datatype, source, tag, comm, status) 
 - The operation waits till a message with a corresponding tuple (source, tag) is not received
 - source identifies the sending process, relative to the used communicator comm) or MPI ANY SOURCE
 - status contains info about the result of the operation
 - Reception of more than count block is an error

# Asynchronous communications

- Non-blocking send operation 
 - Buffer can be re-used only after the completion of the whole transfer
- The send and receive operations create a request
 - Afterwards it is possible to check the status of the request


# Persistent Communication Channels

- Non-blocking
- Created by combining two “half”-channels
- Life cycle
 - Create (Start Complete)* Free
 - Creation, followed by repetitive use, destroyed afterwards
- Channel destruction equivalent to the destruction of the corresponding request

# Collective operations

- Operation performed by all processes within a group
 - Broadcast: MPI BCAST
  - One process (root) will send data to all other processes 
 - Reduction: MPI REDUCE
  - Joins data from all processes in a group (communicator) and makes it available (as an array) to the calling process 
 - Often a group of send/receive operations can be replaced by a single bcast/reduce operation
  - Higher efficiency/performance: bcast/reduce optimized for a particular hardware 
- Other operations
 - alltoall: exchange of messages among all processes in a group 
- Special reduction: min, max, sum, or User defined additional collective operations


# Virtual topology

- MPI can define communication patterns that directly corresponds to the application needs
- These are (in a next step) mapped to the actual hardware ad its communication operations
 - Transparent
- Higher efficiency when writing programs
- Portability
 - Program is not directly associated with a concrete topology of used hardware
- Potential for independent optimizations


# Datatype constructions

- Strided data types
 - They can include “holes
 - Implementation may optimize some datatypes
 - Example: every second element of a vector

# Operations over files

- Support since MPI-2
- File “parallelization”

# MPI and optimizing compilers

- Asynchronous use of memory can lead to data changes (within arrays) that a complier knows nothing about







