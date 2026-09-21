> [!Definition]
> Pre-allocated block of memory divided into equal-sized chunks used for fast, deterministic dynamic memory allocation

^db6b2d


## How Fixed Pools Work
- Pre-allocation: Memory is carved out in a **single contiguous block** during system initialization
- Equal Chunks: Total space is **split** into **uniform** memory slots
- Linked List: Unused blocks are typically **tracked** using an internal free-list
- O(1) Operations: Allocating **unchains** a block, freeing puts it **back on the list**. Both executes in constant time



## Key Benefits 
- Deterministic Timing: Allocation and deallocation take a **predictable**, **fixed amount of time**, preventing deadline misses
- No Fragmentation: Because all **blocks** are the **same size**, external memory **fragmentation** is **completely eliminated**
- ISR Safe: Fast execution and thread-safe design allow memory pools to be **safely accessed** inside ISR
- No `malloc` Risks: Avoids standard heap unpredictable delays and out-of-memory crashes.

















































