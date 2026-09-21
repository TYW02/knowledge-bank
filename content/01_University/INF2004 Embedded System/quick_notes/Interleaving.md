> [!Definition]
> Technique that splits memory or process execution across multiple banks or time slots to speed up data access and simulate parallel processing


## The Problem
The CPU works much faster than standard RAM. Without interleaving, the processor wastes time waiting for a single memory bank to finish a read or write cycle

## How it Works
Sequential memory addresses are distributed across different memory banks in a round-robin pattern.

While one bank is busy finishing a transfer or recharging, the CPU can immediately access the next sequential address in a different bank

### Benefits
Provides higher overall data throughput, lower wait times, and better hardware efficiency













































