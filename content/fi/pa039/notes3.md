----
url: pa039/03
title: notes 03
date 2022-05-05
---


# Optimizing Compiler

- Translation to the Intermediate language
- Optimization
 - intra-procedural analysis
 - cycle optimization
 - global optimization (inter-process optimization)
- Code generation
 - use of all superscalar units 

# Intermediate Language

- Quadruple (generally n-tuple)
- Memory: accessible through temporary variables
- Branches: condition calculated separately
- Branches: jumps to absolute addresses


# Basic blocks

- Program is represented as a flow graph
- Block – a code segment without branches/jumps
 - One entry and one exit point
 - Block as a DAG (Directed Acyclic Graph)
- Optimization within blocks
 - Removal of repeated (sub)expressions
 - Removal of redundant variables


# Additional concepts

Variables
 - definition and place of use
Cycles
Target code generation

# Classical optimizations

Copy propagation:  
X = Y
Z = X + 1 ==> Z = Y + 1

Constants processing
 - constants propagation
 - constants folding
Dead-code elimination
- inaccessible code
- saving cache capacity for instructions
- Strength reduction:
 - K**2 ==> K*K
- Variable renaming
- Common subexpressions elimination: important especially for evaluation of array indices
- Move of invariant code from cycles
- Simplification of induction variables (expressions with them)
- Register allocation


# Garbage elimination

- Procedures, macros: Inlining
- Conditional expressions:
 - Comples expressions reorganization
 - Excessive/redundant tests (if vs case)
- Conditional expressions within cycles
 - Cycle (induction variable) independent
 - Cycle (induction variable) dependent
- Branches (jumps)
- Type conversion
- Manual optimization
 - Common subexpressions
 - code move 
 - array processing

# Cycle optimization

- Overhead reduction
- Better access to memory (efficient use of caches)
- Parallelism increase


# RAW, WAR and WAW dependencies

- Read after Read (RAR): Benign” (in fact no) dependency
- Read after Write (RAW): “True” dependency, Most problematic, order cannot be changed
- Write after Read (WAR): “Antidependency”, Can be dealt with by renaming
- Write after Write (WAW): “Output” dependency, Order cannot change unless checked for other dependencies


# Data dependencies

- Flow dependencies (backward dependencies)
- Anti-Dependencies (Variable renaming as a default solution)
- Output Dependencies: Several values of a variable are computed during the cycle execution, but only the “last” is to be written
- Not always easy to recognize, which value is “the last”

# Loop unrolling
- Cycle body copies several times within the cycle
- Major purpose:
 - Overhead reduction: Reduction of number of iterations (=number of branches)
 - Parallelism increase (also within a single superscalar processor): Software pipelining
- Pre- a postconditioning loops: Actual number of iterations adaptation


Unsuitable loops:
- Small number of iterations −→ full loop unrolling
- “Fat” (=too large)) cycles: already include sufficient number of opportunities for parallelization
- Loops with procedure calls: see also the procedure inlining
- Loops with conditional expressions: more important for older processors
- “Recursive” loops: with internal dependencies (cross iterations)

# Loop unrolling problems

- Unrolling with a bad number of iterations
- Register clogging
- Misses of instruction cache (too long cycle)
- Hardware problems
- esp. on multiprocessors with shared memory (cache coherency, bus overload, ...)
- Special cases: external loops unrolling, loops combination

# Loops combination

- Repeated use of data (cache efficiency)
- Large loop body
- Compiler can do the combination if there is no code between loops

# Memory access optimization

- Optimal: smallest step (cache optimization
- Work with arrays – C vs. Fortran

# Cache optimization – Blocking

- A general technique to split loops working with arrays to loops that work on a block of arrays

# Memory Access Optimization

- Indirect addressing
- Use of pointers
- Insufficient memory capacity
 - "Manual” processing
 - Virtual memory




















