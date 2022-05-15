---
url: /pa039/04
title: notes 04
date 2022-05-05
---


# Measurement of processing/compute time

- Optimization impossible without knowledge what to optimize
- We need to know data about program run
 - Processing/run time of the whole program: time command
 - Processing/run time of individual program components: profiling
 - Run time comparison: benchmarking

## time command

- User time: Processor time consumed by user’s processes
- System time: Processor time consumed by the kernel services
- Elapsed time: Total run time (wall clock time)

# Profiling

- Attempt to get timing information about program parts
- Emphasis on dynamic (run time) behavior: static analysis is a part of software engineering
- Profiling shows a result of an interaction between program and the computing system it runs on
 - Time spent in individual blocks
 - Time spent in individual commands
 - Number of repetition of blocks/commands 
- Primary interest on procedures
- Profile: graph
 - X axis: individual procedures
 - Y axis: run time


# Basic principles

- Uses software tools for collection of data needed for the profile construction
- Usually some operating system support
 - access to information available to kernel only
- Examples of usual profiling tools: gprof, oprofile, valgrind, pin
- Profile collected during the run time – **dynamic profile**
- **Performance Engineering** is the name of the profile data analysis

# Types of data collected

- Call graph at the procedures and functions level
- Call graph at the basis blocks level
- Memory performance
- Events related to the architecture, e.g. incorrect branch predictions, exemptions, cache performance (hit/miss), ...
- Performance counters values

# Profile types

- Sharp profile
 - Peaks related to the dominating blocks/procedures
 - Numerical applications, technical computing with matrices etc
 - “Easily” optimizable
- Flat profile
 - Program spends its run time uniformly in all blocks/procedures
 - Usually databases, information systems, operating systems
 - Difficult to optimize
- Amdahl rule is valid here, too


# Profilers

- Tools for profile construction
 - Naturally possible also “manually”
- Procedure oriented: gprof
- Block (line) oriented: pixie, lprof


# Profilers’ use

Two phases:
- Instrumented program execution (with or without a need for re-compiling)
- Profile Analysis Report
Access to the source code
- Knowledge of program structure

It is possible to profile a program even without an access to the source code


# Procedure oriented profilers

- Typical representative: gprof
- Instrumentation
  - Re-compiling of the program
  - Usually available through a special compiler key (
- Run time
 - Instrumented program creates a compute (processing) trail, file e.g. gmon.out 
- Report construction
 - gprof run over the previously generated gmon.out file


# Measurement precision

Time measurement
- Absolute time of a procedure entry/exit: Nested vs Short procedures 
- Instruction counter value read in uniform intervals: Sampling interval influences the precision of the measurement


# Block oriented profilers

- Provides information about basic block’s processing
- Number of executions per command (program line)
- Number of processor cycles spent in each command

# Benchmarking

- Attempt to compare performance of whole systems
 - Jointly hardware and software 
- No “silver bullet” solution
- Basic approaches
 - Professional benchmarks: Comparability, vendor independence
 - “Private” benchmarks: Specific requirements (deeper knowledge what you need)


# Mysterious MIPS and MFLOPS

- Comparison based on number of instructions per second
- MIPS – million instructions per second
- MFLOPS – million floating point instructions per second
- Problems
 - Which instructions
 - Which order
- Artificial, not adequate

# Fixed point benchmarks

- VAX MIPS
- Dhrystones

# Floating point benchmarks

- Whetstone (artificial mix, scalar)
- Linpack (daxpy, vectorization)


# SPEC benchmarks

- Independent organization: Standard Performance Evaluation Corporation
- Standardized benchmarks for different architectures
- Based on the so called kernel codes
 - Part or a whole existing program
 - Available in the source code


# SPEC groups

- Open Systems Group (OSG)
- High Performance Group (HPG)
- Graphics Performance Characterization Group (GPC)

# Transaction benchmarks

Database performance
- TPC-A
- TPC-B
- TPC-C

# Network benchmarks

- End to end measurements
- Be aware, what you are actually measuring in the network: Not so difficult if within a parallel computer interconnect


# Own benchmarks

- Concrete (specific) requirements
- Important parameters
 - What/how long to test 
 - memory requirements
- Benchmark types
 - single stream
 - throughput

# Checks

- Mandatory part of any benchmarking activity
 - Are we actually measuring what we want to? 
- Potential influencers:
 - Used complier optimization
 - Memory size
 - Other process served by the operating system 
- What must be controlled explicitly
 - CPU time and wall clock time
 - Results!
 - Comparison with “a known” standard









